# Driver Monitoring System

Real-time driver distraction detection using facial landmarks — runs entirely in the browser.

## Features

- **Drowsiness Detection** — Eye Aspect Ratio (EAR) with 20-frame consecutive threshold
- **Yawn Detection** — Mouth Aspect Ratio (MAR) with 15-frame consecutive threshold
- **Head Pose Estimation** — Yaw (left/right) and Pitch (up/down) angle tracking
- **Gaze Estimation** — Left/Center/Right gaze direction
- **Real-time Alerts** — Visual and audio warnings for unsafe behavior

## How to Use

1. Open `index.html` in a browser (Chrome recommended)
2. Click **Start Camera**
3. Allow camera access when prompted
4. The system will detect your face and monitor for distraction

## Deploy to GitHub Pages

1. Create a new GitHub repository
2. Push the `docs/` folder contents
3. Go to Settings → Pages → Source: Deploy from branch → Branch: main, folder: /docs
4. Your site will be live at `https://yourusername.github.io/repo-name/`

## Algorithm

Uses face-api.js (TensorFlow.js) for face detection and 68-point landmark estimation, then calculates:

| Metric | Formula | Threshold |
|--------|---------|-----------|
| EAR | (‖p2-p6‖ + ‖p3-p5‖) / (2 · ‖p1-p4‖) | < 0.25 for 20 frames |
| MAR | (‖p2-p8‖ + ‖p3-p7‖ + ‖p4-p6‖) / (3 · ‖p1-p5‖) | > 0.60 for 15 frames |
| Yaw | atan2(nose_x - eye_center_x) | > 30° |
| Pitch | atan2(chin_y - eye_center_y) | > 25° |
| Gaze | iris_x / eye_width | < 0.40 right, > 0.60 left |

## License

MIT
