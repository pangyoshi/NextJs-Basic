# How the Web Works (Overview)

  What happens when a user enters a website?

- The user types a URL like www.facebook.com into the browser.

- The browser contacts a DNS server to convert the domain name to an IP address.

- The browser uses HTTP/HTTPS sends a request to the web server at that IP.

- The server gathers all the necessary resources

- The server sends responds with files and HTTP response code to the browser.

<br>

## 📡 Technologies Involved: 

DNS – Translates domain to IP.

IP Address – Locates server.

HTTP/HTTPS – Protocol to communicate between browser and server.
---

## 🖥️ From Server to Screen
What happens on the client (browser):
The HTML is rendered into a visual page.

- Browser receives the response and starts to build the visual page.

- Browser reads HTML, applies CSS, runs JavaScript to render page.

- Browser shows the fully formed web page on your screen.

## ⚙️ Behind the Scenes:
- Browser builds DOM Tree from HTML.

- CSS applied for design/layout.

- JavaScript adds interactivity.
---

## 🔑 Key concepts:
Client: The user's browser that displays the web page.

Server: The machine that processes requests and sends back data.

Database: Stores data like users, content, etc.

Frontend & Backend: Frontend is what users see backend is the behind-the-scenes logic.
<img src="/assets/how-the-web-works.png" class="mt-5 w-[75%] mx-auto" />
