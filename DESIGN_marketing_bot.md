# Digivyapar Marketing Bot – System Design

## 1. Overview
The Digivyapar Marketing Bot is a chat-based AI system that converts product images and basic product details into marketing content such as styled images and short videos.
The bot works through chat (Telegram) and automates media generation using AI services, orchestrated by n8n workflows.
The system is designed only for marketing content conversion and does not modify or replace the original product.

---

## 2. High-Level Architecture

User (Telegram Chat)
        |
        v
Telegram Bot API
        |
        v
n8n Webhook Trigger
        |
        v
AI Layer (LLM for intent + prompt generation)
        |
        +---------------------+
        |                     |
        v                     v
Nano Banana (Image Gen)     Sora (Video Gen)
        |                     |
        +----------+----------+
                   |
                   v
           Media Processing (Sharp / FFmpeg if needed)
                   |
                   v
          File Storage (Local / Cloudinary / S3)
                   |
                   v
            Telegram Response (Image / Video Link)

Optional:
Google Vision OCR (if product text extraction is required)

---

## 3. Core Components

### 3.1 Chat Interface
- Telegram Bot API
- Handles product image uploads and delivery of generated media

### 3.2 Workflow Orchestration
- n8n (Self-hosted)
- Routes user intent (image → image / image → video)
- Handles async jobs for video generation

### 3.3 AI Prompt Engine
- LLM API
- Generates safe, structured prompts
- Enforces rules:
  - Use product as-is
  - No replacement or renaming
  - Marketing-only content

### 3.4 Media Generation
- Sora API (Product Image → Video)
- Nano Banana API (Product Image → Marketing Image)
- Sharp / ImageMagick for resizing and watermarking (optional)

### 3.5 OCR (Optional Input Enhancement)
- Google Vision OCR for label text extraction

### 3.6 Storage
- Local storage (MVP)
- Cloudinary / AWS S3 (scale)

---

## 4. Workflow (Step-by-Step)
1. User sends product image on Telegram
2. n8n webhook receives the message
3. (Optional) OCR extracts text
4. LLM generates safe marketing prompt
5. n8n routes to Sora (video) or Nano Banana (image)
6. Media is processed and stored
7. Final image/video is sent back to Telegram

---

## 5. Non-Functional Design
- Async processing for video jobs
- Rate limiting
- Provider abstraction
- Basic logging and retries
