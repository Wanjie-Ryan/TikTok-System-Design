# TikTok System Design
**1. High level overview**
- Millions of concurrent users..
- Real time video uploads and playback.
- Highly personalized recommendations.
- Seamless global delivery.

- The key system design goals are: **Low latency, massive scalability, realtime egagement**

**2. Core system components**
- Backend Gateway - Entry point, API Gateway routes traffic to microservices
- User service - Handles Authentication
- Video service - Upload, encode, store, stream videos
- Feed service - Core of recommendation engine logic.
- Comment/Like service - Manages likes, comments, shares and interaction logs.
- Notification service - Push notifications and engagement loops
- Analytics service - Logs user behaviour for training ML models.
- Moderation service - Filters hate speech, nudity, illegal content.

- All of the services are microservices and communicate via REST/gRPC

**3. Data Flow and Infrastructure**
- User uploads a video(chunked)
- Video is stored temporarily (Redis/s3)
- Video gets passed to encoding service
- metadata is extracted(frame sampling, audio analysis, object detection)
