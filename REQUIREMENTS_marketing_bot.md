# Digivyapar Marketing Bot – Requirements

## 1. Functional Requirements

### 1.1 Chat-Based Input
- Users can send product images, name, and short description
- System responds via Telegram

### 1.2 Marketing Image Generation
- Convert product image into styled marketing image
- Must use the exact product image
- Must not change brand, color, or packaging

### 1.3 Marketing Video Generation
- Convert product image into short marketing video
- Video suitable for social platforms

### 1.4 AI Prompt Safety Rules
- No product renaming or replacement
- No category changes
- No medical or guaranteed claims
- Marketing-only content

### 1.5 OCR Support (Optional)
- Extract label text from images
- Use extracted text only for description

### 1.6 Media Delivery
- Return final image/video
- Provide downloadable link

---

## 2. Non-Functional Requirements

### 2.1 Performance
- Image generation target: under 2 minutes
- Video generation: async with status updates

### 2.2 Reliability
- Retry failed API calls
- Fallback message on failure

### 2.3 Scalability
- Support multiple users
- Queue-based processing for videos

### 2.4 Security
- Validate file type and size
- Prevent prompt injection
- Secure API keys

---

## 3. Constraints
- Marketing content conversion only
- Depends on third-party AI services
- Video generation may be delayed

---

## 4. Future Enhancements
- WhatsApp Business API
- Multi-language content
- Brand style presets
- Bulk processing
- Scheduled delivery
