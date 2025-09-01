# FaceFind (EZPIC) – PRD

## 1. Problem

Too many event / trip photos. Manually scrolling to find yourself is slow.

## 2. Goal (MVP)

Let a user provide one clear face photo (or webcam capture) and see all photos in a chosen folder that contain that face.

## 3. Users

- Student / Attendee: wants own photos fast.
- Organizer (basic): provides shared folder / zip.

## 4. Scope (In)

Face capture, local folder/zip upload, face match, simple gallery with download. Everything runs locally or with free tiers.

### Out of Scope (Now)

Cloud album integrations, multi-user tagging, analytics dashboards, advanced privacy policies, mobile app store release.

## 5. Basic Flow

1. Landing screen: “Add Your Face” or “Upload Album”.
2. User adds face (upload or webcam) → embedding created.
3. User uploads folder/zip of photos (<= 2,000 images).
4. App detects faces, compares to user embedding.
5. Show matched photos grid → allow save/download selected.
6. Optional: Delete face data (clears embedding + temp files).

## 6. Functional Requirements

| ID | Requirement |
|----|-------------|
| FR1 | Upload OR capture single face image (JPEG/PNG). |
| FR2 | Validate exactly one face; else ask retry. |
| FR3 | Compute face embedding (local). |
| FR4 | Upload/select photo set (folder or zip). |
| FR5 | Batch detect faces in each photo. |
| FR6 | Compare embeddings; flag matches above threshold. |
| FR7 | Display matches grid (thumbnail + open full). |
| FR8 | Select & download matched photos (bulk zip). |
| FR9 | Delete session (remove embedding + temp data). |

## 7. Non-Functional (Light)

| Aspect | Target |
|--------|--------|
| Performance | <= 10s for 500 photos on mid laptop (approx). |
| Privacy | No cloud upload unless user chooses; default local. |
| Cost | Use free/open-source only. |
| Usability | One screen per step, minimal text. |

## 8. Data Handling

- Store face embedding only in memory (not persisted) unless user explicitly clicks “Keep for later”.
- Temporary image thumbnails kept in browser memory / IndexedDB (optional), cleared on session end.

## 9. Simple Matching Logic

1. Preprocess face (align / resize 160x160 or model required size).
2. Generate embedding vector (e.g., length 128 or 512 based on model).
3. For each detected face in album: compute embedding (cache per photo).
4. Cosine similarity >= threshold (start 0.85) → match.

## 10. Metrics (Local Console Only)

- Number photos processed.
- Avg ms per photo.
- Match count.

## 11. Risks

| Risk | Simple Mitigation |
|------|------------------|
| Slow on weak hardware | Resize images (e.g., max 720p) before detection. |
| False matches | Adjust threshold slider. |
| Multiple faces in face photo | Force user to crop / recapture. |

## 12. Quick Timeline

| Week | Focus |
|------|-------|
| 1 | Basic UI + face capture + model load. |
| 2 | Album upload + detection loop. |
| 3 | Matching + gallery + download. |
| 4 | Polish, threshold slider, delete session. |

## 13. Definition of Done (MVP)

- Can load page, capture/upload face, upload photos, see matches, download them, and clear data—all without paid services.
