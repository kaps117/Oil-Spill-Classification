## OilSpillNet: AI-Powered Marine Oil Spill Detection & Analysis

### Elevating Environmental Monitoring with AI

**OilSpillNet** is an advanced AI-driven platform designed to detect, analyze, and assess oil spills from satellite and aerial Synthetic-Aperture Radar (SAR) imagery. By combining state-of-the-art computer vision and machine learning, OilSpillNet delivers rapid, actionable insights for environmental agencies, researchers, and first responders—helping to safeguard marine ecosystems worldwide.

## Why Choose OilSpillNet?

- **AI-Powered Detection**: Immediate, high-accuracy identification of oil spills under diverse environmental conditions.
- **Comprehensive Analysis**: Quantitative assessment of spill area, perimeter, spread rate, and severity.
- **Graphical Insights**: Interactive visualizations of spill evolution and affected regions.
- **Environmental Impact Scoring**: AI-driven severity estimation for prioritizing response efforts.
- **Curated Resources**: Access to case studies, best practices, and regulatory guidelines for spill management.
- **Regular Reports**: Customized email updates and PDF reports for stakeholders and authorities.

## Experience OilSpillNet

**Live Deployment:** [https://oilspillnet.vercel.app](#) (placeholder—replace with your deployment link)  
**Watch the Demo:** [YouTube Video](#) (placeholder for demo link)

## Technology

### System Architecture

OilSpillNet is built on a robust, multi-service architecture for performance, scalability, and security:

| Component          | Technologies & Tools                                      |
|--------------------|----------------------------------------------------------|
| **Frontend**       | React, Next.js, Tailwind CSS, Mapbox GL, Chart.js        |
| **Backend**        | FastAPI, Python (OpenCV, scikit-image, scikit-learn), MongoDB, Firestore |
| **AI & Vision**    | TensorFlow/Keras, Hugging Face Transformers (for advanced detection), Google Vision API (optional) |
| **Data Pipeline**  | Celery, Redis (for batch processing), AWS S3 (for image storage) |
| **Deployment**     | Vercel, Google Cloud Run, MongoDB Atlas, Firebase        |

## Local Setup Guide

```bash
git clone https://github.com/yourusername/OilSpillNet.git
cd OilSpillNet
```

### 1. **Firebase Configuration**

- **Create a new Firebase project** and add a Web App.
- **Enable Authentication**: Email/Password, Google.
- **Retrieve** your `firebaseConfig` from Project Settings > Web App.
- **Set up** `.env` in the frontend folder (see `.env.sample` for required variables).
- **Generate a private key** in Firebase Service Accounts and add to backend `.env`.

### 2. **Google Vision API & Gemini Key**

- **Obtain Google Vision API and Gemini API keys** from Google Cloud Console.
- **Add keys** to backend `.env` as per `.env.sample`.

### 3. **MongoDB Atlas**

- **Create a MongoDB Atlas account** and a new cluster.
- **Retrieve your connection URI** and add to backend `.env`.

### 4. **Cloud Storage**

- **Set up AWS S3** (or equivalent) for image storage; add credentials to backend `.env`.

### 5. **Server Connections**

- **Backend URL**: Add to frontend `.env` (e.g., `REACT_APP_API_LINK=http://localhost:8000`).
- **WebSocket URL** (if applicable): Add to frontend `.env` (e.g., `REACT_APP_WS_LINK=ws://localhost:8802`).

### 6. **Installation & Launch**

- **Ensure Python 3.10+ and Node.js 18+ are installed.**
- **Install dependencies**:
  - Backend: `pip install -r requirements.txt`
  - Frontend: `npm install`
  - (Optional) WebSocket server: `npm install` and `node index.js`
- **Launch servers**:
  - **Backend**: `uvicorn main:app --reload`
  - **Frontend**: `npm run dev`
  - **WebSocket Server** (if used): `node index.js`

## Website Preview

| Page       | Key Features                                                     |
|------------|-----------------------------------------------------------------|
| **Home**   | Quick spill detection upload, recent incidents, live map         |
| **Upload** | Drag-and-drop SAR imagery, batch processing, progress tracking   |
| **Analysis** | Spill visualization, severity scoring, historical trends, export reports |
| **Resources** | Case studies, regulations, response guidelines                  |
| **Account**   | User history, saved reports, notification settings              |

## Recognition

**🏆 Recognized at [Relevant Hackathon/Conference Name]** (customize as applicable)

## Ready to Make an Impact

**OilSpillNet** stands out for its seamless blend of cutting-edge AI, environmental science, and user-centric design. Whether you’re a government agency, environmental NGO, researcher, or developer, OilSpillNet delivers a powerful, scalable, and secure platform for marine protection—all with transparent setup and clear best practices.

All instructions, tech stack details, and deployment steps are presented for clarity and ease of use—prioritizing both performance and environmental responsibility.

**Get started today—clone, configure, and deploy.**  
**Contribute, customize, and help protect our oceans for generations to come.**

[1] https://github.com/kaps117/MentalHealthAi
