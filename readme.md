# TikTok System Design

**1. High level overview**

- Millions of concurrent users.
- Real time video uploads and playback.
- Highly personalized recommendations.
- Seamless global delivery.

- The key system design goals are: **Low latency, massive scalability, realtime egagement**

**Functional Requirements**

1. User profile
2. View video
3. Upload video
4. Create video
5. Like video
6. Follow user
7. Live streaming

**Non-functional Requirements**

1. Security
2. Storage
3. Performance
4. Latency
5. Scalable

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
- Stored in Object storage (like AWS S3)
- DB is updated with video record and features

**Feed Path**

- User opens the app
- Feed service calls recommendation engine
- List of video IDs returned
- Video metadata + CDN links fetched
- App renders video

**4. CDN**

- Store static chunks of video
- Reduce latency
- They use **Adaptive Birate Streaming (ABR)** based on your network, the app loads higher/lower quality video.

**5. Recommendation Engine**

- Watch time
- Likes
- Replays
- Shares
- Comments
- Skip behaviour

**Multi-stage Pipeline**

1. Candidate generation

- narrow down from millions to thousands using collaborative filtering.

2. Filtering

- Rule-based removal (nudity, banned topics)

3. Ranking model

- Deep learning score videos for this user.

4. Re-ranking/Diversity

- Inject variety, promote trends, don't show duplicates.

**Database Design**

- UserData - MySQL
- Video metadata - Cassandra
- Media storage - S3-compatible object storage
- Engagement logs - Kafka
- Real time stats - Redis

**FANOUT**

- It describes how content is distributed to multiple consumers - how a new video gets delivered to potentially millions of users feeds.
- Distributes one piece of content to many users.

**Fanout Models**

- Two main types of fanout patterns

1. Fanout on write (Push model)

- When content is created, it is pushed to all followers immediately.
- Used by X
- Fast read times (feeds load fast)
- Costly write ops if user has millions of followers.

2. Fanout on Read (Pull Model)

- When user opens the app, the backend pulls fresh content for them from creators they follow
- Used by IG and TikTok
- Efficient for users with many follows.
- Slower read time, heavier backend query.


---------------------------------------------

# Challenges
1. Ingestion
2. Storage
3. Distribution


