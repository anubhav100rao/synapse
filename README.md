# Synapse: The Micro-Learning Network

**Synapse** is a dual-mode social platform that solves the "Doomscrolling" problem by bridging the gap between passive consumption (short-form video) and active deep learning (structured text & discussion).

## 🚀 Core Value Proposition
*   **The Problem:** Existing social media (TikTok/Instagram) offers high dopamine but low value. Educational platforms (Coursera) have high friction.
*   **The Solution:** A "Trojan Horse" for learning. We catch users with high-signal visual hooks ("Sparks") and instantly convert that attention into deep understanding ("Logs").

## 📚 Documentation Index
This repository contains the core product and technical specifications for Synapse.

| Document | Description |
| :--- | :--- |
| **[Product Definition](product_idea.md)** | The "Bible" of the product. Defines the "Spark & Log" mechanic, AI features, and gamification strategy. |
| **[Architecture Guidelines](synapse_architecture_doc.md)** | High-level technical architecture, including the Flutter/FastAPI/Neo4j stack. |
| **[System Diagram](architecture.md)** | Mermaid diagram visualizing the service interactions and data flow. |

## 🌟 Key Features
1.  **Dual-Mode Content**:
    *   **Spark**: 60s vertical video (Video Hook).
    *   **Log**: Threaded deep-dive text (Knowledge).
    *   **Interaction**: "Dock & Scroll" UI allowing simultaneous watching and reading.

2.  **Synapse Studio (AI Co-Pilot)**:
    *   Auto-generates text threads from video transcripts to lower creator friction.

3.  **Spaced Repetition System (SRS)**:
    *   The "Feed" intersperses review quizzes to ensure long-term retention of "Saved" facts.

4.  **Peer Review Protocol**:
    *   Community-driven verification ("Level 10 Python Expert") instead of paid blue checks.

## 🛠 Tech Stack
*   **Mobile**: Flutter (Dart)
*   **Backend**: FastAPI (Python)
*   **Database**: PostgreSQL + Neo4j (Graph)
*   **AI/Search**: Pinecone (Vector) + OpenAI/Claude

## 🏁 Getting Started
*This section will be updated as the MVP is built.*

1.  Read the **[Product Definition](product_idea.md)** to understand the vision.
2.  Review the **[Architecture](synapse_architecture_doc.md)** to understand the system design.
