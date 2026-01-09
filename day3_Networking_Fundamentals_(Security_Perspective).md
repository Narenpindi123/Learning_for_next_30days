# Day 3 — Task 3  
## What Happens When I Type `google.com`

This task explains, step by step, what happens behind the scenes when a user types `google.com` into a web browser and presses Enter.  
The explanation focuses on **DNS resolution**, **TCP connection establishment**, and **encryption (HTTPS/TLS)**.

---

## Step 1: Browser Interprets the Input

When `google.com` is typed into the browser:

- The browser recognizes it as a **domain name**, not a search query
- Since no protocol is specified, modern browsers default to:
https://google.com


This means the browser will attempt a **secure HTTPS connection**.

---

## Step 2: DNS Resolution (Domain Name to IP Address)

Computers communicate using IP addresses, not domain names.  
DNS (Domain Name System) is used to translate `google.com` into an IP address.

### 2.1 Local Cache Checks
Before querying the network, the system checks:
- Browser DNS cache
- Operating system DNS cache

If the IP is found, DNS resolution stops here.

---

### 2.2 DNS Resolver Query
If the IP is not cached, the system sends a DNS query to its configured DNS resolver (ISP DNS, router, or public DNS).

The query asks:
> “What is the IP address for `google.com`?”

---

### 2.3 DNS Hierarchy Lookup
If the resolver does not have the answer cached, it performs a hierarchical lookup:

1. **Root DNS servers** – Identify the `.com` TLD servers  
2. **`.com` TLD servers** – Identify Google’s authoritative DNS servers  
3. **Authoritative DNS server** – Return the IP address for `google.com`

---

### 2.4 DNS Response
The resolver returns the IP address to the system, which:
- Caches the result for a defined TTL (Time To Live)
- Provides the IP address to the browser

At this point, the browser knows **where** to connect.

---

## Step 3: TCP Connection (Three-Way Handshake)

Since HTTPS is used, the browser must connect to **port 443** using TCP.

TCP establishes a reliable connection using a **three-way handshake**:

1. **SYN** – Client requests a connection  
2. **SYN-ACK** – Server acknowledges and agrees  
3. **ACK** – Client confirms

After this handshake:
- A reliable communication channel is established
- No application data has been sent yet

---

## Step 4: TLS Handshake (Encryption Setup)

TCP alone does not provide encryption.  
Because HTTPS is used, a **TLS handshake** is performed.

### 4.1 Client Hello
The browser sends:
- Supported TLS versions
- Supported encryption algorithms
- Random values for key generation

---

### 4.2 Server Hello and Certificate
The server responds with:
- Selected encryption method
- Digital certificate
- Server public key

---

### 4.3 Certificate Verification
The browser verifies that:
- The certificate is trusted
- The certificate matches `google.com`
- The certificate is valid and not expired

If verification fails, the browser displays a security warning.

---

### 4.4 Session Key Creation
Once verified:
- The browser and server generate shared session keys
- All further communication is encrypted using these keys

---

## Step 5: Encrypted HTTP Request (HTTPS)

The browser sends an HTTP request such as:

GET /
Host: google.com

yaml
Copy code

This request is:
- Encrypted using TLS
- Invisible to anyone intercepting the traffic

---

## Step 6: Server Processing

Google’s server:
- Receives the request
- Processes it
- Prepares an HTTP response (status code, headers, and content)

---

## Step 7: Encrypted HTTP Response

The server sends back:
- Encrypted HTML
- Encrypted headers
- Encrypted cookies (if applicable)

Only the browser can decrypt this data.

---

## Step 8: Browser Rendering

After decrypting the response, the browser:
1. Parses HTML
2. Builds the page structure
3. Requests additional resources (CSS, JavaScript, images)
4. Executes scripts and renders the page

Each additional resource may trigger its own DNS and TCP/TLS processes.

---

## Step 9: Page Load Completion

Once all required resources are loaded:
- The Google homepage is displayed
- Connections may remain open for reuse
- DNS and TLS data may be cached for performance

---

## Summary Flow

1. **DNS** – Resolve `google.com` to an IP address  
2. **TCP Handshake** – Establish a reliable connection  
3. **TLS Handshake** – Set up encryption  
4. **HTTPS Request** – Request webpage securely  
5. **HTTPS Response** – Receive encrypted content  
6. **Rendering** – Display the webpage

---

## Key Takeaways

- DNS resolves names before any connection is made
- TCP ensures reliable data transfer
- TLS provides confidentiality and integrity
- HTTPS is HTTP traffic encrypted with TLS
- A simple browser action triggers multiple layered network processes

---
