
# Lesson: HTTP Basics

## 📖 Source
- Platform: TryHackMe
- Lab: HTTP Basics
- Date: 2025-12-10

---

## 🧠 Key Concepts

* **HTTP is a Stateless Protocol:** This is critical. The server treats every **request** as a brand new, independent communication.  The necessary mechanism for maintaining state (like being logged in) is typically handled by **cookies** or **session tokens**, which are sent as headers.
* **The Three Parts of Communication:**
    * **Request:** Contains a **Method** (verb), a **URL** path, **Headers** (metadata), and an optional **Body** (data).
    * **Response:** Contains a **Status Code** (result), **Headers**, and an optional **Body** (content).
* **Common Methods (The Verbs):**
    * **GET:** **Retrieves** data. *Should never modify server state.* (Vulnerable to Cross-Site Request Forgery (CSRF) if it *does* modify state).
    * **POST:** **Submits** data to be processed or stored (e.g., login credentials, form data). Data is typically in the request body.
    * **HEAD:** Same as GET, but the server only returns the **headers**, not the body. Useful for checking file existence/size without downloading.
    * **PUT/PATCH:** Used to **modify** existing resources. PUT replaces the entire resource; PATCH applies partial modifications.
    * **DELETE:** Used to **remove** a resource.
* **Common Status Codes (The Results):**
    * **1xx Informational:** 101 Switching Protocols.
    * **2xx Success:** **200 OK**, 201 Created, 204 No Content.
    * **3xx Redirection:** **301 Moved Permanently**, 302 Found (Temporary). Critical for knowing where user requests are going.
    * **4xx Client Error:** **400 Bad Request**, **401 Unauthorized** (needs authentication), **403 Forbidden** (authenticated, but access denied), **404 Not Found**, 405 Method Not Allowed. *These are common targets for security testing.*
    * **5xx Server Error:** **500 Internal Server Error**, 503 Service Unavailable.

---

## 🛠️ Commands & Tools
- `curl -v http://example.com`: **Inspect request/response headers** and the full communication flow (verbose output).
    * *Security context:* Use `-X POST -d 'data'` to test form submissions or API endpoints.
- `nc -lvnp 8080`: **Listen for raw HTTP traffic** directly on a port (creating a basic server) to observe exactly what the client sends.
    * *Security context:* Great for manually crafting and sending HTTP requests line-by-line to test filtering or unexpected inputs.
- **Browser DevTools (Network Tab):** Analyze request/response flow, view headers, inspect cookies, and observe redirects.
    * *Security context:* The primary tool for understanding the client-side interaction with the server, including hidden form fields and AJAX calls.
- **Burp Suite Community Edition (Proxy):** Intercept and modify requests/responses between the browser and server in real-time.
    * *Security context:* **Essential** for any web application hacking/testing.

---

## 🔑 Details
* **Headers:** Metadata is often a source of security information or vulnerabilities.
    * `Host`: Specifies the domain name. Critical for **Virtual Host/Host Header attacks**.
    * `User-Agent`: Identifies the client software. Often checked/filtered by the server.
    * `Content-Type`: Describes the format of the body (e.g., `application/json`, `text/html`). Important for **XSS** and upload filtering.
    * `Set-Cookie`/`Cookie`: The primary mechanism for **session management** and state maintenance.
    * **Security Headers** (e.g., `Content-Security-Policy`, `X-Frame-Options`): Their presence (or absence) is a key indicator of site security posture.
* **Body:** Carries the payload/data.
    * In a **POST** request, the body is the data being submitted (e.g., login form data).
    * In a **GET** request, data is often in the **query string** of the URL (e.g., `?user=admin`).
* **Statelessness & State Persistence:**
    * Servers don't remember past requests. **Cookies** (small pieces of data stored by the browser) are the common way to send a session token back with every request, allowing the server to maintain state (e.g., "this user is logged in").
    * **Cookie security flags** (`HttpOnly`, `Secure`, `SameSite`) are vital for preventing theft (XSS) and misuse (CSRF).
* **Persistent Connections (Keep-Alive):** HTTP/1.1 introduced reusing the underlying TCP connection for multiple HTTP requests. This improves performance but also changes how firewalls and security tools track connections.

---

## 🚀 Observations
* **Method Difference (GET vs. POST):** Successfully identified resources (GET) versus submitting data that changes state (POST). *Security insight:* Using GET for state-changing operations is a **security flaw** (CSRF risk).
* **Header Manipulation:** Practiced modifying the `User-Agent` to bypass simple filters or using the `Host` header to explore potential virtual host routing issues.
* **Status Code Triaging:** Learned to immediately identify the type of server response:
    * A **200 OK** on a hidden admin page means a security bypass occurred.
    * A **403 Forbidden** on a file means the server is explicitly denying access (testing access controls is necessary).
    * A **500 Internal Server Error** often suggests backend code failure, which can sometimes be exploited via **timing attacks** or used to discover technology stack details.

---

## 📌 References
- [MDN Web Docs: HTTP Overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
- [OWASP Top 10 Web Application Security Risks](https://owasp.org/www-project-top-ten/)
- [PortSwigger Web Security Academy](https://portswigger.net/web-security) (Excellent resource for learning security implications of HTTP)
- [RFC 2616: HTTP/1.1 Specification](https://www.rfc-editor.org/rfc/rfc2616)
