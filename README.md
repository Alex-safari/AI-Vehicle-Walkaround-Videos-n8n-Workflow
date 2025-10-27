# AI-Vehicle-Walkaround-Videos-n8n-Workflow (Veo 3.1 + n8n)
Stop wasting hours filming Car Walkaround Videos for every car in your lot. This workflow handles that automatically. It generates them from just 5 photos... for 93 cents using n8n and Google Veo 3.1

**This template was created by Alex Safari.**
Subscribe to my YouTube channel for more AI automation tutorials:
👉 https://www.youtube.com/@alexsafari1

📺 **Watch the Full Tutorial Video:**
https://youtu.be/c5nlH_J9wUc

## Overview
This workflow is the complete system behind the **AI Vehicle Walkaround Video Generator**. It transforms **5 simple photos** (3 of a car, 1 of a dealership, 1 of a salesperson) into a complete, 3-scene, 24-second video advertisement—for a total cost of **$0.93 per video**.

It uses an "AI Salesperson" agent to analyze all visual data, write a unique script, and generate a high-quality video with a **consistent character** using **Google Veo 3.1**.

## Workflow Breakdown

*This workflow is designed to be triggered in two ways:*
1.  **Form Trigger:** A form to upload the 5 images and car details (Make, Model), which populates a Google Sheet with a "Pending" status.
2.  **Schedule Trigger:** Runs daily, reads the Google Sheet, and processes the first "Pending" job it finds.

### 1. Read Database
- **Trigger:** Reads a Google Sheet (`Car Dealership Promo Video`) to find the first row with a "Status" of "Pending".
- **Output:** Fetches all 5 image URLs and the vehicle metadata (Make, Model, ID).

### 2. Parallel AI Vision (Gemini 2.5 Pro)
- The workflow runs 5 separate **Gemini 2.5 Pro** vision nodes in parallel.
- Each node analyzes one of the 5 reference images (Scene 1, Scene 2, Scene 3, Dealership, Character) using an advanced YAML prompt.
- **Result:** Generates 5 exhaustive YAML descriptions detailing everything from car paint color to the salesperson's clothing and the dealership's architecture.

### 3. Log Descriptions
- The 5 YAML descriptions are aggregated and updated back to the Google Sheet. This provides a clear log of the AI's "vision" step.

### 4. "AI Salesperson" Agent (GPT-4.1)
- **Node:** `Veo Creative Director and Scriptwriter`
- This is the "brain" of the operation. It receives all 5 YAML descriptions and the car's Make/Model.
- **Action:** The GPT-4.1 agent writes a unique, persuasive 3-scene script (Intro, Features, CTA) designed for an 8-second clip.
- **Output:** It structures all this data into a JSON object with 3 separate, highly-detailed prompts, one for each scene, ensuring a **consistent character in Veo 3 n8n**.

### 5. Generate 3 Video Scenes (Google Veo 3.1)
- The 3-scene JSON is split into 3 separate items.
- Each item is passed to the `Kie.ai VEO3.1 fast image to video subworkflow`.
- This is the core of the **Google Veo 3.1 image to video n8n** process, generating three 8-second video clips.

### 6. Stitch Final Video (FFMPEG)
- The 3 video URLs from Veo 3.1 are aggregated into a single array.
- This array is sent to the `Fal.ai FFMPEG Merge Videos` subworkflow.
- **Result:** A single, seamless 24-second **Veo 3 advertisement n8n** video.

### 7. Upload & Finalize
- **Download:** The final merged video is downloaded from the FFMPEG URL.
- **Upload:** The video file is uploaded to Google Drive ("Car Promo Videos" folder).
- **Update Database:** The final Google Drive link is saved to the original Google Sheet row, and the "Status" is updated to "Done".

## ⚙️ Tech Stack
- **n8n** – Workflow orchestration & automation logic
- **Google Veo 3.1 (Kie.ai)** – Video generation engine
- **Gemini 2.5 Pro (Google)** – AI vision & image analysis
- **GPT-4.1 (OpenRouter)** – "AI Salesperson" agent (scripting & prompting)
- **Google Sheets** – Database / Job queue
- **Google Drive** – Final video storage
- **Cloudinary** – (Used in Form) Image hosting
- **Fal.ai FFMPEG** – Video merging

## 💸 Cost Breakdown
- **Veo 3.1:** $0.90 ($0.30 per 8-second scene x 3)
- **Gemini 2.5 Pro:** ~$0.02 (for 5 image analyses)
- **GPT-4.1 Agent:** ~$0.0113 per run
- **FFMPEG:** ~$0.004 per video
- **Total: ~$0.935 per video**

---

📧 **Email me directly**: contact@loopsera.com
For quick questions, customisation requests, or workflow troubleshooting.

🌐 **Visit my website**: [https://loopsera.com](https://loopsera.com)
Explore more automation templates, services, and case studies.

📞 **Book a Discovery Call**: [https://cal.com/loopsera/discoverycall](https://cal.com/loopsera/discoverycall)
For businesses that need a custom AI agent built around their Instagram and ecommerce setup.

🎓 **1-on-1 Coaching Session**: [https://cal.com/loopsera/n8n-ai-agent-coaching-session](https://cal.com/loopsera/n8n-ai-agent-coaching-session)
Personalised coaching to help you build, troubleshoot, or optimise n8n AI workflows. Perfect for both beginners and advanced users.

💬 **Join the AI Builder’s Boardroom (Skool Community)**: [https://www.skool.com/ai-builders-boardroom-1717](https://www.skool.com/ai-builders-boardroom-1717) — a professional community for builders creating AI agents that talk, listen, and sell, focused on deploying the digital workforce of the future.
