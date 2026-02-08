# Synapse Feed Architecture Guide

This document defines the architecture for Synapse's short-form video feed. It combines **industry-standard engineering practices** (latency, scale, pre-fetching) with **Synapse-specific product requirements** (Knowledge Graphs, Spaced Repetition).

---

## 1. Core Philosophy: The "Hybrid" Engine

Synapse operates differently from entertainment-only platforms (TikTok).
*   **TikTok:** Optimizes for *Time Spent* & *Virality*.
*   **Synapse:** Optimizes for *Knowledge Retention* & *Insight*.

### The Hybrid Generation Model
We use a weighted mix for candidate generation:
1.  **Interest Graph (60%)**: Collaborative filtering + Content-based retrieval (Vector Similarity).
2.  **Social Graph (20%)**: Content from followed "Experts" or "Peers".
3.  **SRS Queue (20%)**: *Unique to Synapse.* Mandatory "Review Cards" injected based on the Spaced Repetition Schedule (SM-2 Algorithm).

---

## 2. Engineering Architecture

### A. The "Zero-Buffer" Latency Strategy
Short-form video demands <200ms load times.
*   **Client-Side Pre-fetching**: The mobile client strictly maintains a buffer of the *next 3 videos*.
    *   **Implementation**: When Video N starts playing, immediately fetch the first 3 seconds of Video N+1, N+2, N+3.
*   **Protocol**: Use **QUIC (HTTP/3)** over TCP to eliminate head-of-line blocking on cellular networks.
*   **CDN Strategy (Cloudflare Stream)**:
    *   *Hot Content*: Cached at the Edge (PoPs).
    *   *Manifests*: Values for HLS/DASH are generated instantly.

### B. The Feedback Loop (Real-time Learning)
*   **Stream Processing**: User actions (Swipe vs. Watch vs. Quiz Answer) are pushed to a **Kafka** topic.
*   **Online Learning**: Simple linear models (e.g., Logistic Regression for CTR) are updated near real-time (every 15 mins) to catch viral trends.
*   **Deep Learning Models**: Complex Vector-based models are retrained nightly.

### C. The "Cold Start" Solution
1.  **New Users**:
    *   **Onboarding**: The "Interest Cloud" (selected at signup) seeds the initial Vector Profile.
    *   **Geo-Proxy**: Use location to boost local/cultural relevance initially.
2.  **New Videos (Exploration)**:
    *   **Multi-Armed Bandit**: Every new video gets a "Test Budget" of 100 impressions to random users with matching Interest Tags.
    *   **Promotion**: If *Insight Score* (Watch time + Quiz completion) > Threshold, move to the global candidate pool.

---

## 3. The Synapse Differentiators

### A. Prerequisite Filtering (The "Hard Gate")
Unlike TikTok, we cannot show Advanced content to Beginners.
*   **Logic**: Before ranking, query the **Neo4j Knowledge Graph**.
*   **Query**: `MATCH (u:User)-[:KNOWS]->(p:Topic)<-[:REQUIRES]-(v:Video) RETURN v`
*   **Result**: If the user lacks the prerequisites, the video is *excluded* from the candidate set, regardless of virality.

### B. SRS Injection
*   **Logic**: The Feed Service queries the **SRS Engine** for "Due Reviews".
*   **UX**: These appear as "Pop-Quiz" cards or "Quick Review" videos interspersed between new content.

---

## 4. Data Processing Pipeline

### A. Ingestion (AI Analysis)
When a video is uploaded:
1.  **Transcode**: Cloudflare generates ABR ladder (360p/720p/1080p).
2.  **Transcription**: Whisper API extracts text.
3.  **Semantic Tagging**: LLM analyzes text to extract:
    *   *Topics*: e.g., "React Hooks", "Quantum Physics".
    *   *Difficulty*: Beginner/Intermediate/Advanced.
    *   *Prerequisites*: "Requires: JavaScript Basics".
4.  **Vectorization**: Store embeddings in **Pinecone**.

### B. Storage Schema
*   **User Profile (Cassandra/ScyllaDB)**: High-write throughput for "Seen History", "Swipes", "Quiz Results".
*   **Video Metadata (Postgres/ScyllaDB)**: Stats (Views, Insight Score), Creator ID, Topic Tags.
*   **Knowledge Graph (Neo4j)**: The Tree of Topics.

---

## 5. Metrics & Optimization (Objective Function)

We optimize for **Insight**, not just Engagement.

$$ Score = w_1 \cdot (WatchTime) + w_2 \cdot (Completion) + w_3 \cdot (QuizAccuracy) + w_4 \cdot (SaveRate) $$

*   **Negative Signals**: Quick Swipe (< 3s).
*   **Positive Signals**:
    *   *Completion*: Watched 90%.
    *   *Rewatch*: Looped > 1 time.
    *   *Validation*: Answered the "Micro-Quiz" correctly (The strongest signal).
