# CivicPulse – System Design Document

## 1. High-Level Architecture

User (Web/Mobile)
        ↓
Frontend (React + Tailwind)
        ↓
Backend API (Node.js + Express)
        ↓
Database (MongoDB)
        ↓
AI Layer (NLP + Scoring Engine)
        ↓
Admin Dashboard

---

## 2. System Components

### 2.1 Frontend
- Issue submission form
- Voice input module
- Map view (Google Maps / Mapbox)
- Trending & prioritized issues feed
- Status tracking interface

---

### 2.2 Backend Services

#### a) Issue Service
- Store issue details
- Geolocation tagging
- Status management

#### b) AI Processing Service
Triggered when new issue is created:
1. Categorization (sanitation, roads, water, etc.)
2. Sentiment & urgency analysis
3. Duplicate detection (cosine similarity)
4. Impact score calculation

Impact Score Formula (MVP example):
Impact Score = (Number of Similar Reports × Sentiment Severity × Geographic Spread Weight)

---

### 2.3 Clustering Logic

- Convert complaint text to embeddings
- Compare with existing issues
- If similarity > threshold → group into cluster
- Update cluster impact score

---

### 2.4 Heatmap Module

- Aggregate issues by location
- Generate density values
- Render heatmap on frontend map view

---

### 2.5 AI Report Generator

Input:
- Clustered issue data
- Number of reports
- Severity score
- Location

Output:
- Structured summary
- Recommended action
- Priority level (High / Medium / Low)

---

## 3. Database Schema (Simplified)

### Users
- userId
- name
- role (citizen / admin)

### Issues
- issueId
- title
- description
- category
- sentimentScore
- impactScore
- location (lat, lng)
- clusterId
- status
- createdAt

### Clusters
- clusterId
- issueCount
- avgSeverity
- region
- priorityLevel

---

## 4. AI Workflow

1. User submits issue
2. Backend stores raw data
3. AI processes text
4. Assign category & sentiment
5. Check similarity with existing issues
6. Update cluster or create new one
7. Recalculate impact score
8. Generate summary for dashboard

---

## 5. Security & Privacy

- JWT-based authentication
- Role-based access control
- Minimal personal data storage
- Secure API endpoints

---

## 6. Future Scalability

- Multi-city deployment
- Integration with real municipal APIs
- Predictive civic risk analysis
- Multilingual model fine-tuning
