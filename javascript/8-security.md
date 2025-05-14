Here are clear, concise, and security-focused answers to **JavaScript Security** interview questions—particularly around **XSS** and **CSRF**, which are essential for modern web apps.

---

### ✅ **1. What is XSS and how do you prevent it in a JS app?**

#### 🔐 What is XSS (Cross-Site Scripting)?

XSS is a vulnerability where attackers inject **malicious JavaScript** into webpages viewed by other users.

#### 🧨 Example:

If an app allows users to enter names and injects this into HTML without sanitizing:

```html
<div>Hello, <span id="username"></span></div>
```

```javascript
document.getElementById("username").innerHTML = location.search; // attacker can inject <script>
```

#### ✅ How to Prevent XSS:

| Strategy                                     | Explanation                                                   |
| -------------------------------------------- | ------------------------------------------------------------- |
| **Escape output**                            | Escape HTML before injecting user input (`<`, `>`, `"` etc.)  |
| **Use `textContent`** instead of `innerHTML` | Prevents script execution                                     |
| **Sanitize inputs**                          | Use libraries like `DOMPurify` to sanitize user-provided HTML |
| **Content Security Policy (CSP)**            | Limit sources of scripts/styles/images in HTTP headers        |
| **Avoid inline scripts**                     | Helps enforce CSP and reduce risk                             |

#### ✅ Secure Example:

```javascript
// BAD: vulnerable to XSS
element.innerHTML = userInput;

// GOOD: safe
element.textContent = userInput;
```

---

### ✅ **2. What is CSRF and how can it be mitigated?**

#### 🔐 What is CSRF (Cross-Site Request Forgery)?

CSRF tricks a logged-in user into unknowingly submitting actions (e.g. transferring money) on a web app **without their intent**.

#### 🧨 Example Attack:

* User is logged into `bank.com`
* Visits `evil.com` which has:

  ```html
  <img src="https://bank.com/transfer?amount=1000&to=hacker" />
  ```

The browser **sends cookies automatically**, making the request look valid.

#### ✅ How to Prevent CSRF:

| Method                                         | Description                                                                               |
| ---------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **SameSite cookies**                           | Set `SameSite=Strict` or `Lax` on cookies to block cross-origin requests                  |
| **CSRF tokens**                                | Include a random, per-request token in forms or headers that must match server validation |
| **Double Submit Cookies**                      | Send CSRF token as both cookie and header – must match                                    |
| **Use custom headers (like X-Requested-With)** | Only allow requests with trusted headers                                                  |
| **Disable credentials for cross-origin**       | Set `credentials: 'same-origin'` in `fetch()`                                             |
| **CORS with strict origin validation**         | Limit allowed origins for APIs                                                            |

#### ✅ Example Secure CSRF Token Flow:

1. Server generates a random token → embeds in page/form.
2. Client sends token with POST request (e.g. in headers).
3. Server checks if token matches session → if not, rejects.

---

### 🛡️ Summary Table

| Threat        | XSS (Cross-Site Scripting)         | CSRF (Cross-Site Request Forgery)             |
| ------------- | ---------------------------------- | --------------------------------------------- |
| Type          | User injects malicious JS          | Attacker exploits user session                |
| Attack Vector | Via HTML/JS input                  | Via browser auto-submitting credentials       |
| Prevention    | Sanitize output, CSP, escape input | CSRF tokens, SameSite cookies, custom headers |

---

Let me know if you want real-world examples of XSS/CSRF in React or Node.js apps and how to implement these protections practically.
