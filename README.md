# 🔗 URL Shortener

A minimal, cache-first URL shortening backend service built with **Spring Boot**, **Redis**, and **NoSQL (MongoDB or DynamoDB)**. Designed as a micro backend project to showcase clean architecture, async request flows, and system design decisions — especially around cost-efficiency and scalability.

---

## 📌 Purpose

- 🎯 Build something small, but architecturally solid
- 💡 Focus on backend layers, not frontend/UI
- 🔁 Apply **cache-first thinking** (Redis → NoSQL)
- 🧠 Practice **system design storytelling** for interviews (e.g., Microsoft, Meta)
- ⏱️ Deliverable in 1 week — code + design doc + optional Docker

---

## 🚀 Core Features

- `POST /shorten` → Accepts a long URL and returns a shortened version
- `GET /{shortId}` → Redirects to the original URL
- Built-in **TTL** support for expiring links
- Redis cache layer for fast redirect resolution
- Unique ID generation (Base62 encoding strategy)

---

## ⚙️ Tech Stack

| Layer             | Technology            |
|-------------------|------------------------|
| Backend Framework | Spring Boot (Java)     |
| Database          | MongoDB / DynamoDB     |
| Caching           | Redis                  |
| Containerization  | Docker (optional)      |
| Testing           | JUnit 5                |

---

## 📐 System Design Overview

Full design details, architecture diagram, and trade-offs documented in:  
👉 [`/docs/design-notes-url-shortener.md`](./docs/design-notes-url-shortener.md)

Covers:
- Redis + NoSQL rationale
- Cache hit/miss flow
- Database choice and scaling
- TTL handling
- API & request flow diagrams

---

## 📮 API Endpoints

| Method | Endpoint       | Description                            |
|--------|----------------|----------------------------------------|
| POST   | /shorten       | Accept long URL, return short version  |
| GET    | /{shortId}     | Redirect to original URL               |

---

## 📁 Folder Structure

```bash

/url-shortener
│
├── docs/
│   └── design-notes-url-shortener.md
|
├── src/main/java/com/bivek/urlshortener
│   ├── controller/
│   ├── service/
│   ├── repository/
│   ├── model/
│   ├── utils/
│
├── src/test/
├── Dockerfile
├── application.yml
└── README.md
```

---

## 🧪 How to Run (Local)

# Clone the repo
git clone https://github.com/BivekKumarMali/URL-Shortener.git

cd url-shortener

# Optional: Start Redis and MongoDB using Docker
docker-compose up -d

# Run the Spring Boot application
./mvnw spring-boot:run

---

## 🧠 Why NoSQL?

This project uses **MongoDB / DynamoDB** instead of relational databases like PostgreSQL for these reasons:

- 🗃️ **Simpler data model** — the system is inherently key-value: `shortId → longUrl`
- ⏳ **Built-in TTL support** — easily expire links without writing custom cleanup logic
- ⚡ **High read throughput** — ideal for redirect-heavy workloads
- 💸 **Cost-effective at scale** — avoids the overhead of SQL features we don’t use (e.g. joins, transactions)

> 📝 Full breakdown in: [`/docs/design-notes-url-shortener.md`](./docs/design-notes-url-shortener.md)
