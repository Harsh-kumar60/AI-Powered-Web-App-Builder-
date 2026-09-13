# NxtBuild — AI-Powered Web App Builder 🚀

An ambitious full-stack application where users can describe their web application ideas in plain English, and AI generates a complete, responsive, and working web app with a real-time live preview and an interactive chat assistant for iterations.

---

## 📌 The Problem & The Idea-to-Code Gap
* **The Reality:** Having a vision ≠ Having a working app. Turning a brilliant layout idea into a fully-functional web page requires setting up HTML structure, writing CSS from scratch, handling JavaScript interactivity, and ensuring cross-browser responsiveness.
* **The Gap:** For an experienced developer, building a simple landing page manually takes around **4-8 hours** from scratch. For non-developers, this gap is an insurmountable wall.
* **Traditional Approaches and Their Limitations:**
  * *Manual Coding:* Extremely time-consuming for rapid prototyping.
  * *Templates:* Rigid customizability that rarely matches your precise vision.
  * *No-Code Builders (Wix/Squarespace):* Severe vendor lock-in and minimal control over the underlying code.
  * *Hiring a Developer:* Expensive with slow turnaround times.

## ✨ Our Solution
**NxtBuild** brings the power of industry-leading AI code agents directly to your browser. Users chat naturally to generate code, preview adjustments instantly, and retain 100% ownership of their clean, standalone source files.

---

## 🌟 Key Features

| Feature | Description |
| :--- | :--- |
| **🔐 User Authentication** | Secure user registration and login using JWT tokens and robust bcrypt password hashing. |
| **📁 Project Management** | Dashboard to seamlessly create, view, rename, and delete independent web app projects. |
| **🤖 AI Code Generation** | Converts natural language descriptions into complete HTML/CSS/JS applications using Google's Gemini AI SDK. |
| **💬 Interactive Chat UI** | An intuitive conversational interface to incrementally update and refine your web app ("make the header blue", "add a contact form"). |
| **👁️ Live Preview Window** | Real-time rendering of generated source code using isolated sandbox environment iframes. |
| **💻 Code Editor & Download**| Clean built-in viewer to inspect generated code and export it instantly as a standalone HTML file. |

---

## 🛠️ Tech Stack & Dependencies

### Backend Engine (`/server`)
- **Express & Node.js** (v5.2.1) — Fast and minimalist web framework for building APIs.
- **Mongoose & MongoDB Atlas** (v9.2.4) — Scalable Object Data Modeling (ODM) for managing users and code projects.
- **BcryptJS & JSONWebToken** — Industry standards for password hashing and secure token-based user sessions.
- **@google/genai** (v1.44.0) — Official SDK integration for Google Gemini models.

### Frontend Application (`/client`)
- **React.js** (v19.0.0) — Component-driven reactive user interface framework.
- **React Router Dom** (v7.1.0) — Modern declarative client-side routing.
- **Axios & JS-Cookie** — Promised-based HTTP requests paired with robust browser cookie session management.
- **Vite** (v6.0.0) — Blazing fast modern development frontend tooling and bundler.

---

## 📁 Project Structure

```text
build-your-own-lovable/
├── server/                          # Express Backend Engine
│   ├── server.js                    # Core Application Entry Point
│   ├── src/
│   │   ├── app.js                   # Express application and Middleware configurations
│   │   ├── config/                  # DB and Gemini AI configurations
│   │   ├── constants/               # AI system prompts and instructions
│   │   ├── controllers/             # Express API controllers
│   │   ├── models/                  # Mongoose data definitions (User, Project)
│   │   ├── routes/                  # API endpoint routing mappings
│   │   ├── services/                # Business & AI logical abstraction layers
│   │   └── utils/                   # JSON parsers and security token utilities
└── client/                          # React Frontend Dashboard
```

---

## ⚙️ Installation & Environment Setup

### 1. Environment Configurations (`server/.env`)
Create a `.env` file in your `server/` directory using the provided sample as a structural blueprint:
```bash
cd server
cp .env.example .env
```
Open `server/.env` and update it with your credentials:
```env
MONGODB_URI=your_mongodb_atlas_connection_string
JWT_SECRET=your_super_secret_session_key_123
GEMINI_API_KEY=your_google_gemini_api_key
```

### 2. Run the Backend Server
```bash
cd server
npm install
npm start
```

### 3. Run the Frontend Client
```bash
cd ../client
npm install
npm run dev
```

---

## 🚀 Core Architecture Flow
1. **Secure Session Validation:** Users register via the `User.model.js` schema configuration. Passwords undergo irreversible salt encryption before database entry, returning signed credentials valid for 7 days via `jwt.utils.js`.
2. **Contextual AI Chat Iteration:** The system builds conversation memory parameters. Instructions are piped into system prompts before passing structural arrays to the Gemini engine.
3. **Regex Markdown Sanitization:** Gemini code block outputs frequently include surrounding markdown code barriers (` ```html `). The `parseGeminiJSON` utility cleanly intercepts, strips, and formats these objects back into isolated standard strings.
