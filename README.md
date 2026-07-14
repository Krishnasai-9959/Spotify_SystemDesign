# 1. Requirements & Assumptions

The system is designed to support approximately **500K active users** with a music catalog of around **30 Million songs**.

## Functional Requirements

- Artists can upload songs.
- Users can search and stream songs.
- Users can create and manage playlists.
- Users can maintain their profiles.
- Basic monitoring and observability including:
  - Health checks
  - Error tracking
  - Performance metrics

## Audio Formats

The platform stores audio in **Ogg** and **AAC** formats with multiple bitrates for adaptive streaming.

| Quality | Purpose |
|---------|---------|
| 64 kbps | Mobile data saving |
| 128 kbps | Standard quality |
| 320 kbps | Premium quality |

### Assumption

- Average song size (standard quality): **3 MB**

---

# 2. Capacity Planning

## Song Storage

### Formula

```
Total Storage = Average Song Size × Total Songs
```

### Calculation

```
3 MB × 30 Million Songs
≈ 90 TB
```

### Notes

- Excludes replicas across regions.
- Excludes versioning when artists re-upload songs.
- Actual storage should be planned for **2–3×** the calculated value.

---

## User Metadata

Each user stores:

- Profile
- Preferences
- Playlists

### Formula

```
Average User Metadata × Total Users
```

### Calculation

```
1 KB × 500K Users
≈ 0.5 GB
```

---

## Song Metadata

Each song stores:

- Title
- Artist references
- Duration
- File URLs

### Formula

```
Average Metadata Size × Total Songs
```

### Calculation

```
100 Bytes × 30 Million Songs
≈ 3 GB
```

Song metadata occupies very little storage compared to the audio files.

---

## Daily Bandwidth

### Assumptions

- Average listening time: **3.5 minutes**
- Audio quality: **128–160 kbps**
- Average bandwidth per stream: **3–4 MB**
- Each user streams **10–15 songs** per day.

### Observation

Streaming contributes significantly to outbound bandwidth (egress) costs and should be considered during infrastructure planning.
