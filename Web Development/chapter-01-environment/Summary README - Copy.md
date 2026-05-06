# Chapter 1: Setting Up Your Web Development Environment

The internet is a vast network of connected computers that hosts over a billion websites. Originally used by researchers to share information, it’s now used for nearly everything, whether it be for socializing, sharing photos, planning trips, reading news, and learning.

Websites are built using three main languages: 
- HTML (structure/content)
- CSS (design/style), and 
- JavaScript (interactivity) 


Websites are delivered by remote computers called servers and viewed on devices called clients (like phones or laptops) through web browsers (e.g. Chrome or Firefox). Because users access websites on many different devices and browsers, sites need to work across all of them. We'll come back to this later, but first it helps to understand how a simple HTML website works so those ideas make more sense afterward.

### HTML
HTML (HyperText Markup Language) is the basic structure of every web page.

HTML organizes content like text, images, and videos on a website. If you inspect any webpage, you’ll see HTML behind it. 

HTML is:
- a Markup language that tells a computer how to structure and display content using elements.
- HyperText that is simply text that links to other content through hyperlinks.

Learning HTML is the first step to building websites. Even basic knowledge lets you edit content in blogs, emails, or site templates. Later, you can combine HTML with CSS and JavaScript to create more advanced, styled, and interactive pages. For now, we'll focus on adding simple content like text, images, and videos.

### Getting Started on Creating a Basic Web Page

HTML (HyperText Markup Language) is used to define the structure and content of a web page.

A basic web page includes:
- Document structure (`<!DOCTYPE html>`)
- Root element (`<html>`)
- Head section (`<head>`)
- Body section (`<body>`)

The browser reads this structure and renders the visible content.

Key idea:
> HTML defines what content exists on the page, not how it looks.

---

### 8. 🧪 Local Files vs Server Testing

> NOTE: HTML does NOT runs on the server (it runs in the browser)

#### Open files directly:
- Fast and simple
- Works for static HTML

#### Use a server:
- Required for dynamic content (PHP, databases)

💡 Rule:
> If it needs a server → use localhost  
> If not → open file directly  

If the .html file is already stored on your computer, the browser loads it directly rather than fetching it from the internet. When you open a local .html file, your browser acts as an interpreter that reads the stored code and translates it into a visible webpage, including layout, text, and images



### 🌐 How the Web Works (Architecture)
Every website involves three main parts:

- **Users** are the people who visit the website  
- **Web Browsers** are computer applications (e.g. Chrome, Edge, and Firefox) that load & display websites on your screen and are interactive.
- **Web Servers** are remote computers that stores & sends content (e.g. text/files/pictures) to web browsers when requested.

The Basic Flow is:
1. Through a browser, the user enters a URL
2. The Browser sends a request to the server for the page data (which can include pictures, text, videos, etc.).
3. The Server sends back the requested files (if available) to the browser.
4. The Browser assembles & then displays the page.

This is the idea of the Request–Response Cycle and is the **core engine of the web**. This happens multiple times per page (for images, CSS, JS)


- Browser sends a **request** (GET / POST)
- Server sends a **response** (HTML, CSS, JS)

```
For Example:
Say a server contains an html file that looks like:

<img src="a.png">
<img src="b.png">
<img src="c.png">

Here’s the flow:

1. Your browser makes a request:
GET /index.html

2. The server responds with just the HTML file.
3. The browser parses the HTML (builds the Document Object Model). 

Then the browser sees:
“Oh, I need a.png”
“Oh, I need b.png”
“Oh, I need c.png”

The browser makes 3 more requests:

GET /a.png
GET /b.png
GET /c.png

& the server responds to each one separately:
Response 1 → image a.png
Response 2 → image b.png
Response 3 → image c.png
```

> Overall, every website is just a series of requests and responses.


---

### 3. 🖥️ Localhost (Your Development Environment)

You should learn how to set up the tools to build and test websites.
**localhost = your own computer acting as a server**

Instead of uploading files constantly:
- Run a local server (e.g., XAMPP)
- Test instantly in your browser

### ✅ Benefits:
- Faster development
- No internet required
- Safe testing environment

---

### 4. 📄 Static vs Dynamic Content

#### Static Content
- Same every time
- Example: About page

#### Dynamic Content
- Changes based on user or data
- Example: blog, login system

💡 Key Idea:
> Static = fixed  
> Dynamic = generated

---

### 5. 🧰 Essential Development Tools

You only need three tools:

#### 1. Code Editor
- Example: Notepad++, VS Code
- Used to write code

#### 2. Web Browser
- Used to test and view your site

#### 3. Web Server
- Local (XAMPP) or live (hosting)

---

### 6. 🔄 Web Development Workflow

Typical process:

1. Plan (what are you building?)
2. Design (layout, UI)
3. Code (HTML, CSS, JS)
4. Test (fix bugs)
5. Deploy (publish live)

💡 Reality:
> Developers repeat this loop constantly.

---

### 7. 🧱 Front-End vs Back-End

#### Front-End (Client Side)
- What users see
- HTML → structure  
- CSS → styling  
- JavaScript → interactivity  

#### Back-End (Server Side)
- Handles logic, databases, APIs
---

## ⚠️ Common Beginner Mistakes
- Forgetting to refresh or dealing with cached files
- Confusing file paths vs URLs
- Not understanding how files connect together

---

## 🎯 What Actually Matters (Focus Points)

If students remember only this, they’ll succeed:

1. Browser ↔ Server relationship  
2. Request → Response cycle  
3. Localhost workflow  
4. Static vs dynamic content  

---

## 🚀 Learning Outcome

By the end of this chapter, students should be able to:

- Explain how websites work
- Run a local development server
- Understand how files are delivered to a browser
- Navigate basic development tools

---

## 💡 One-Line Summary

> A website is just files delivered by a server and displayed by a browser through a request-response cycle.