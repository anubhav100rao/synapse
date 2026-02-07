# Product Definition: Synapse (Micro-Learning Platform)

## Executive Summary
**Synapse** is a dual-mode social network designed to bridge the gap between passive consumption (Instagram-style "Sparks") and active understanding (X-style "Logs"). By solving the content friction problem with AI and the retention problem with Spaced Repetition, it positions itself as the "Anti-Doomscrolling" app.

### Core Philosophy: "The Knowledge Graph Feed"
Unlike social networks where the connection is "Person-to-Person," Synapse's primary connection is **"User-to-Topic."**
*   **The Problem**: Users want to learn but are trapped in dopamine loops. Existing learning tools are high-friction.
*   **The Solution**: A "Trojan Horse" for education. Use high-signal visual hooks to capture attention, then immediate deep-text threads to convert that attention into knowledge.

---

## 1. The Atomic Unit: "The Spark & The Log"
The fundamental unit of content is a **"Learning Unit."**

### A. The Spark (Visual Hook)
*   **Format**: 60-second vertical video, precise infographic, or code snippet image.
*   **Goal**: Grabs attention and introduces the concept.
*   **UI Interaction (Dock & Scroll)**: Instead of a cramped split-screen or a jarring flip-card, the user **swipes up**. The video **docks** to the top (becoming a mini-player) while the text thread slides up. This allows simultaneous listening and reading.

### B. The Log (Deep Dive)
*   **Format**: A structured, thread-based deep dive attached *directly* to the Spark.
*   **Content**: Nuance, citations, debate, and technical details.
*   **Engagement**: To mark a Unit as "Complete", the user must interact with the Log (e.g., answer a micro-quiz).

---

## 2. Key Features & Innovations

### A. Synapse Studio (AI Co-Pilot)
Solves the "Content Friction" problem (creating video + text is hard).
*   **Video-to-Thread**: AI transcribes video chunks and auto-generates structured, cited threads.
*   **Thread-to-Visual**: AI suggests title cards/infographics for text-first creators.
*   **Impact**: Drastically lowers the barrier to entry.

### B. Verification: The "Peer Review" Protocol
Solves the "Trust" problem without centralized gatekeeping.
*   **Mechanism**: Users earn "Reputation Points" in specific domains (e.g., "Level 5 in Python").
*   **Weighted Endorsements**: High-reputation users can endorse others, accelerating their credibility.
*   **Integration**: Bootstrap via LinkedIn/GitHub APIs.

### C. Active Tutor (AI Copilot)
Solves the "Passive Consumption" problem.
*   **Implementation**: An LLM (RAG-based) that "watches" the video with the user.
*   **Context Aware**: Knows the transcript, thread, and comments.
*   **Proactive**: Generates floating prompts like *"Explain 'Event Horizon'?"* during playback.

### D. Engagement: Spaced Repetition (SRS)
The "Killer Feature" for retention.
*   **Mechanism**: When a user "Saves" a fact, the system schedules a review.
*   **The Feed**: Intersperses "Review Quizzes" (20% of content) into the daily feed.
*   **Metric**: "Insight Score" tracks *retained* knowledge, not just clicks.

---

## 3. Audience Segmentation
To avoid "Feed Pollution", users select modes:
1.  **Kids (Discovery Mode)**: Heavily visual, gamified, strict safety. "TikTok for Science."
2.  **Professionals (Deep Dive Mode)**: Text-heavy. Industry news, architectural debates.
3.  **Hobbyists (How-To Mode)**: Mix of step-by-step carousels and Q&A threads (Cooking, Woodworking).

---

## 4. Monetization Strategy
*   **Tokenized Knowledge**: Free viral consumption. Creators charge for "Mastery Extensions" (PDFs, Code, Deep Dives).
*   **Corporate Sponsorship**: Brands sponsor entire "Curriculum Tracks" (e.g., AWS sponsors Cloud Computing).

---

## 5. Technical Stack Summary
To support the unique requirements (Real-time Video, Graph Data, Vector Search):

| Component | Technology | Why? |
| :--- | :--- | :--- |
| **Frontend** | **Flutter** | High-performance "Dock & Scroll" animations. |
| **Backend** | **FastAPI (Python)** | Async support for AI/Video processing. |
| **Graph DB** | **Neo4j** | Essential for Knowledge Graph (Prerequisites) & Reputation. |
| **Vector DB** | **Pinecone/Weaviate** | **Critical** for AI Tutor (RAG) and Semantic Search. |
| **Video** | **Cloudflare Stream** | Cost-effective global delivery. |
