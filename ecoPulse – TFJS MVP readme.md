# **ecoPulse – TFJS MVP**

**Modern, web-based citizen science platform** that detects plants, awards points, sends alerts for rare species, and displays environmental warnings—all via a **slide-up card UI**.

## **Table of Contents**

1. [Introduction](https://chatgpt.com/c/67b360ae-b7d0-8006-a120-d4415a8c49d1#introduction)  
2. [Features](https://chatgpt.com/c/67b360ae-b7d0-8006-a120-d4415a8c49d1#features)  
3. [Tech Stack](https://chatgpt.com/c/67b360ae-b7d0-8006-a120-d4415a8c49d1#tech-stack)  
4. [Prerequisites](https://chatgpt.com/c/67b360ae-b7d0-8006-a120-d4415a8c49d1#prerequisites)  
5. [Installation & Setup](https://chatgpt.com/c/67b360ae-b7d0-8006-a120-d4415a8c49d1#installation--setup)  
6. [Usage](https://chatgpt.com/c/67b360ae-b7d0-8006-a120-d4415a8c49d1#usage)  
7. [Project Structure](https://chatgpt.com/c/67b360ae-b7d0-8006-a120-d4415a8c49d1#project-structure)  
8. [Known Limitations](https://chatgpt.com/c/67b360ae-b7d0-8006-a120-d4415a8c49d1#known-limitations)  
9. [Future Enhancements](https://chatgpt.com/c/67b360ae-b7d0-8006-a120-d4415a8c49d1#future-enhancements)  
10. [License](https://chatgpt.com/c/67b360ae-b7d0-8006-a120-d4415a8c49d1#license)

---

## **Introduction**

**ecoPulse** is a **web-based MVP** that uses **client-side AI** (TensorFlow.js) to detect plants via a user’s camera. It awards points (Firebase gamification), shows environmental alerts, and triggers an email for “Rare Species” detection. The UI is minimalistic and modern, featuring a **slide-up card** that can be **dragged** to minimize or fully open.

This repository contains the final integrated code:

* **Camera-based plant detection**  
* **Rare Species** popup with audio  
* **Firebase** for points and leaderboard  
* **EmailJS** for sending email alerts  
* **Echo3D** for a 3D model viewer  
* **Slide-up** card UI with a “Recapture” button

---

## **Features**

1. **Camera-Based AI Detection**

   * Uses **TensorFlow.js** to load a custom 2-class model (`Neem`, `Rare Species`).  
   * Inference happens entirely on the client side (no backend needed for ML).  
2. **Modern Slide-Up UI**

   * **Minimalist** design with **Poppins** font, **pastel green** background, and **rounded** containers.  
   * A **drag handle** allows users to swipe the card down to 20% or fully open.  
3. **Recapture & Popup**

   * **Recapture** button hides the card and clears the canvas so users can scan again.  
   * **Rare Species** triggers a **popup** with an audio alert awarding **1000 points**.  
4. **Firebase Gamification**

   * **Anonymous sign-in** ensures each user has a unique ID.  
   * Points are updated in **Cloud Firestore**.  
   * A **leaderboard** displays the top 10 users by points.  
5. **EmailJS Alerts**

   * When Rare Species is detected, an **email** is sent automatically (containing location and seed type).  
6. **Environmental Warnings**

   * Uses **Geolocation API** to check if the user is in a specific bounding box (e.g., Maharashtra).  
   * Displays a locust outbreak warning if applicable.  
7. **3D Model Viewer**

   * If `Neem` is detected, an **Echo3D** `<iframe>` is shown in the card, displaying a 3D model.

---

## **Tech Stack**

* **HTML/CSS/JavaScript**  
  * Core front-end, plus custom **drag/swipe** logic for the slide-up card.  
* **TensorFlow.js**  
  * Client-side AI for plant detection.  
* **Firebase**  
  * **Authentication** (anonymous)  
  * **Cloud Firestore** (leaderboard, optional Rare Species scans)  
* **EmailJS**  
  * Sends email alerts for Rare Species detection.  
* **Echo3D**  
  * Embeds a 3D model for visual flair.  
* **Geolocation API**  
  * Accesses user coordinates for environmental alerts.

---

## **Prerequisites**

1. **HTTPS or localhost**

   * Browsers require a secure origin for **camera** and **geolocation** access.  
   * For local testing, use `http://localhost` or a secure environment (e.g., `https://yourdomain.com`).  
2. **Firebase Project**

   * Create a project in the [Firebase Console](https://console.firebase.google.com/).  
   * Enable **Authentication** (anonymous) and **Cloud Firestore**.  
3. **EmailJS Account**

   * Sign up at [EmailJS](https://www.emailjs.com/).  
   * Create a **service** and **template**, note the **public key**.  
4. **Custom TF.js Model**

   * Hosted at a URL (e.g., `model.json`).  
   * By default, the code references `https://virajsh4h.github.io/ecoPulse-model/model.json`.

---

## **Installation & Setup**

**Clone or Download** this repository:

 git clone https://github.com/your-username/ecopulse.git  
cd ecopulse

1.   
2. **Replace Placeholders** in `index.html` (or `ecoPulse.html`, etc.):

**Firebase Config**:  
 const firebaseConfig \= {  
  apiKey: "YOUR\_FIREBASE\_API\_KEY",  
  authDomain: "YOUR\_FIREBASE\_DOMAIN",  
  projectId: "YOUR\_FIREBASE\_PROJECT\_ID",  
  storageBucket: "YOUR\_FIREBASE\_STORAGE\_BUCKET",  
  messagingSenderId: "YOUR\_FIREBASE\_SENDER\_ID",  
  appId: "YOUR\_FIREBASE\_APP\_ID",  
  measurementId: "YOUR\_MEASUREMENT\_ID"  
};

* 

**EmailJS**:  
 emailjs.init("YOUR\_EMAILJS\_PUBLIC\_KEY");  
...  
emailjs.send('YOUR\_SERVICE\_ID', 'YOUR\_TEMPLATE\_ID', templateParams);

* 

**Model URL** (if needed):  
 const modelURL \= 'https://virajsh4h.github.io/ecoPulse-model/model.json';

*   
3. **Serve Locally**

   * Use a simple server (e.g., `npx http-server .` or `python -m http.server 8000`).  
   * Make sure it’s on **HTTPS** or `localhost`.  
4. **Open in Browser**

   * Go to `https://localhost:8000/index.html` (or your domain).  
   * Allow camera & location permissions.

---

## **Usage**

1. **Open the App**

   * The camera feed should appear in the black container.  
   * The **Leaderboard** is initially “empty” until points are added.  
2. **Capture & Analyze**

   * Click the **Capture & Analyze** button.  
   * The code draws the video frame onto the canvas and runs inference via TensorFlow.js.  
   * The slide-up card appears with the detection result.  
3. **Rare Species**

   * If “Rare Species” is detected, the app:  
     * Awards **1000 points**,  
     * Displays a **popup** with an audio alert,  
     * Sends an **EmailJS** alert with user location,  
     * (Optionally) stores a Rare Species scan in Firestore.  
4. **Neem**

   * If “Neem” is detected, the app:  
     * Awards **10 points**,  
     * Displays an **environmental alert** if user is in the bounding box,  
     * Shows a **3D model** from Echo3D.  
5. **Recapture**

   * Tap the **Recapture** button in the slide-up card to close the card and clear the canvas, enabling a new scan.  
6. **Swipe**

   * Drag downward on the card to minimize it to 20%, or drag upward to fully open it.

---

## **Project Structure**

ecopulse/  
├── index.html        \# Main HTML with UI, scripts, and references  
├── README.md         \# This readme  
├── model/            \# (Optional) If you host your TF model locally  
├── assets/           \# (Optional) For images, audio, etc.  
└── ...               \# Other configs or script files

**Note**: This example is a single-page MVP. You can reorganize as needed for larger projects.

---

## **Known Limitations**

1. **Performance**

   * Running TensorFlow.js inference in the browser can be CPU-intensive, especially on low-end devices.  
2. **Camera & Geolocation**

   * Requires **HTTPS** or `localhost`; otherwise, the user’s browser may block access.  
3. **EmailJS Size Limits**

   * If you re-add screenshot attachments, large images may cause emails to fail. For production, consider a backend or smaller images.  
4. **Firebase Storage**

   * Storing large base64 strings in Firestore can bloat your DB. For more images or bigger scans, consider **Firebase Storage**.

---

## **Future Enhancements**

1. **Multiple Classes**

   * Expand the TF model to detect more plant types (e.g., Ashoka Leaves, Tulsi, Basil).  
2. **River Pollution or Water Analysis**

   * Extend environmental alerts to detect water pollution or other anomalies.  
3. **Push Notifications**

   * Integrate **Firebase Cloud Messaging** for real-time push alerts.  
4. **Daily Briefing Dashboard**

   * Provide a daily snapshot of air quality, weather, or local eco-updates.  
5. **Advanced AR**

   * Leverage **WebXR** or **AR.js** for more immersive 3D overlays.

---

## **License**

**ecoPulse** is an MVP/demo. If you need an open-source license, you can choose something like MIT:

MIT License  
Copyright (c) 2023 ...  
Permission is hereby granted, free of charge, ...  
