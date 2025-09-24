# Smart Email Assistant

*This project was inspired by wanting to save time on email responses while learning full-stack development.*

I built this project to learn how to create a complete full-stack application from scratch. It's an AI-powered tool that helps you write email replies faster by integrating directly with Gmail.
## What I Created

This project has three main parts that all work together:

**Spring Boot Backend API** (`http://localhost:8080`)
- Handles the AI magic by connecting to Google's Gemini API
- Takes your email content and returns smart replies
- Built with Java 23 using Spring Boot from start.spring.io

**React Frontend** (`http://localhost:5173`) 
- A clean web interface where you can paste any email and get AI-generated responses
- Uses Material-UI for a professional look
- Talks to the backend API to get the generated replies

**Chrome Extension**
- The coolest part - adds an "AI Reply" button directly inside Gmail
- When you're writing an email, it automatically generates a reply for you
- Works by injecting itself into Gmail's interface using some JavaScript magic

## How to Get This Running on Your Computer

### First, Get Your Google Gemini API Key
1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Create a free API key (it's free for limited use)
3. Keep this key safe - you'll need it later

### Setting Up the Backend
```bash
cd backend
# Open src/main/resources/application.properties
# Add this line: gemini.api.key=YOUR_ACTUAL_API_KEY_HERE
mvn spring-boot:run
```

The backend will start on http://localhost:8080
 ### Setting Up the Web Interface
```bash
cd frontend
npm install
npm run dev
```

The React app will open on http://localhost:5173

### Installing the Chrome Extension
- Open Chrome and go to chrome://extensions/

- Turn on "Developer mode" in the top-right

- Click "Load unpacked" and select the chrome-extension folder

- The extension will install and work automatically when you use Gmail

## How It Actually Works
### The AI Part
When you give it an email, my Spring Boot service sends it to Google's Gemini AI with a prompt like: "Generate a professional email reply for this content..." The AI sends back a nicely formatted reply.

### The Gmail Integration
This was tricky to figure out. The Chrome extension uses something called MutationObserver to watch for when Gmail opens a reply window. When it detects one, it adds a custom button that matches Gmail's style. When you click it, it grabs the email text, sends it to my backend, and puts the AI response right into your reply.

### The Web Interface
The React app is simpler - it's just a text box where you paste email content and a button to generate replies. It uses Axios to call my Spring Boot API.

## Challenges I Ran Into
**CORS Issues** - At first, my React app couldn't talk to the Spring Boot API because browsers block requests between different ports (5173 → 8080). I fixed it by adding @CrossOrigin to my Spring Boot controller.

**Gmail Button Injection** - Gmail's interface changes dynamically, so my extension had to be smart about when and where to add the AI button. It took some trial and error to get it working reliably.

**AI Response Formatting** - The Gemini API returns JSON with the reply buried deep inside. I had to write code to extract just the text part I needed.

## What I Learned From This Project
- **Spring Boot**: How to create REST APIs and handle CORS configuration

- **React**: Component state management and making API calls

- **Chrome Extensions**: How to interact with existing websites and modify their UI

- **AI Integration**: Working with third-party APIs and processing their responses

- **Full-Stack Development**: How frontend, backend, and extensions communicate

## Technologies I Used
- **Backend**: Java 23, Spring Boot 3.x, Maven, Gemini API

- **Frontend**: React, Material-UI, Axios, Vite

- **Extension**: Vanilla JavaScript, Chrome Extension API

- **Tools**: Git, Postman (for testing APIs)

## Ideas for Making This Better
- Let users choose different tones (friendly, casual, professional)

- Remember frequently used email patterns

- Support for multiple languages

- Add a history of generated replies
##
*This was my first time building something that combines a web app with a browser extension. It was challenging but really satisfying when all the pieces finally worked together! If you try it out and have suggestions, I'd love to hear them.*
