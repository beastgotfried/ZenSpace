# ZenSpace - Enhanced Full Screen Intervention System

A comprehensive gesture recognition and wellness intervention system that monitors habits and stress indicators through real-time computer vision, providing immediate interventions for better mental health and focus.

## Overview

ZenSpace uses advanced gesture detection and pose analysis to monitor:
- **Stress indicators** (clenched fists, anxiety habits)
- **Fatigue levels** (yawning patterns)
- **Postural problems** (tech neck, slouching)
- **Bad habits** (nail biting, phone distraction)
- **Emotional states** (through body language)

When issues are detected, ZenSpace activates intelligent interventions:
- Guided breathing exercises
- Meditation audio and calming overlays
- Screen warmth adjustment for awareness
- Brown noise for focus
- Posture correction feedback
- Energy breaks for fatigue

## Features

### 🎯 Gesture Recognition System

**Emergency Gestures (Quick Intervention Triggers):**
- ✋ **Open Palm** (2s hold) → Zen Mode with meditation
- 🙌 **Both Hands Raised** (2s hold) → Guided breathing exercise
- 🙉 **Hands on Ears** (2s hold) → Quiet Mode with brown noise
- ✊ **Clenched Fist** (3s hold) → Box breathing + screen warmth

**Calm & Focus Gestures:**
- 🤲 **Palms Together** (2s hold) → Mindfulness meditation (5 min)
- ✌️ **Peace Sign** (2s hold) → Focus Mode (5 min blur + calming ambience)

**Exit Gesture:**
- 👌 **OK Sign** (1.5s hold) → Exit all active modes

### 📊 Passive Monitoring & Interventions

**Nail Biting Detection:**
- Episodes 1-5: Progressive screen warmth (habit awareness building)
- Episode 6+: Breathing exercise activation (anxiety intervention)
- Visual feedback on screen with episode counter

**Fatigue Detection:**
- Monitors yawning patterns (5 yawns in 25-second window)
- Triggers energy break overlay with guided recovery
- Shows prominent fatigue alerts

**Phone Distraction Warning:**
- Detects when user looks down at phone (3+ seconds)
- Activates screen warmth and beeping alert
- Clears when user looks back up

**Posture Monitoring:**
- Detects forward head posture (tech neck)
- Identifies slouching and hunching
- Monitors shoulder alignment and asymmetry
- After 30 seconds of poor posture:
  - Visual feedback with red pose lines
  - Beeping alerts
  - Screen warmth activation
  - Real-time posture issue display
- Lines turn green when posture corrects

## Installation

### Requirements
- Python 3.8+
- Webcam
- Windows/macOS/Linux

### Setup

1. **Clone the repository:**
```bash
git clone https://github.com/beastgotfried/ZenSpace.git
cd ZenSpace
```

2. **Create virtual environment (recommended):**
```bash
python -m venv venv
venv\Scripts\activate  # Windows
source venv/bin/activate  # macOS/Linux
```

3. **Install dependencies:**
```bash
pip install -r requirements.txt
```

### Dependencies
- **opencv-python** - Computer vision and video processing
- **mediapipe** - Hand, pose, and face landmark detection
- **numpy** - Numerical computing
- **pydub** - Audio playback and manipulation
- **pygame** - Audio support

See `requirements.txt` for complete list.

## Usage

### Running ZenSpace

```bash
python main.py
```

### Controls

| Gesture | Duration | Action |
|---------|----------|--------|
| Open Palm | 2 seconds | Activate Zen Mode |
| Both Hands Raised | 2 seconds | Start Breathing Exercise |
| Hands on Ears | 2 seconds | Enter Quiet Mode |
| Clenched Fist | 3 seconds | Box Breathing + Warmth |
| Palms Together | 2 seconds | Mindfulness Session |
| Peace Sign | 2 seconds | 5-Min Focus Mode |
| OK Sign | 1.5 seconds | Exit All Modes |
| ESC Key | - | Exit Application |
| Q Key | - | Quit Camera Window |

## How It Works

### Detection Pipeline

1. **Video Capture** → Real-time webcam feed
2. **MediaPipe Processing** → Extract hand, pose, and face landmarks
3. **Gesture Recognition** → Identify specific hand and body positions
4. **Behavior Analysis** → Monitor for stress signs, habits, and fatigue
5. **Intervention Trigger** → Activate appropriate wellness response
6. **Real-time Feedback** → Visual and audio cues on screen

### Core Components

**detector.py:**
- GestureDetector class with MediaPipe integration
- Hand gesture recognition (palm, fist, peace sign, OK sign, etc.)
- Pose analysis for posture and body position
- Facial landmark processing for yawn detection
- Mouth landmark extraction for nail biting detection

**intervention.py:**
- BrownNoisePlayer - Ambient brown noise for focus
- WhiteNoiseBeeper - Audio alerts for distraction
- ZenMeditationPlayer - Calming meditation audio
- BreathingOverlay - Visual breathing guides (box, 4-7-8)
- EnergyBreakOverlay - Fatigue recovery screen
- ScreenWarmer - Progressive screen warmth for awareness
- ZenModeDim - Full-screen dimming with messages
- PostureWarningOverlay - Posture feedback visualizations
- PostureWarningBeeper - Audible posture alerts

**main.py:**
- ZenSpaceEnhanced controller class
- Gesture processing and intervention coordination
- State management for all active modes
- Real-time monitoring loops
- Camera overlay rendering

## Configuration

### Thresholds (adjustable in main.py)

```python
# Yawn threshold for energy break (in 25-second window)
self.yawn_threshold = 5

# Nail biting episodes before anxiety intervention
self.nail_biting_threshold = 6

# Bad posture warning time (seconds)
self.posture_warning_threshold = 30

# Phone distraction detection time (seconds)
# Configured in process_gestures: 3 seconds

# Screen warmth levels (nail biting episodes 1-5)
self.nail_biting_warmth_levels = [10, 20, 30, 40, 50]
```

## Audio Files

Place the following audio files in the project directory:
- `brown_noise.mp3` - Brown noise for quiet mode
- `beep_alert.mp3` - Alert sound for distractions
- `meditation_background.mp3` - Meditation ambience

## Output

### On-Screen Display
- **Status indicators** - Active modes (Zen, Breathing, Quiet, Focus, Energy)
- **Gesture feedback** - Visual confirmation of recognized gestures
- **Counter displays** - Yawn count, nail biting episodes
- **Pose visualization** - Skeletal overlays with posture feedback
- **Alerts and warnings** - Color-coded messages for urgent issues

### Console Output
- Real-time event logging
- Gesture detection confirmations
- Intervention state transitions
- Performance metrics

## Use Cases

✅ **Work/Study Environments:**
- Combat phone distraction during focused work
- Maintain proper posture during extended screen time
- Manage stress and anxiety through quick interventions

✅ **Mental Health Support:**
- Monitor anxiety indicators (nail biting)
- Provide on-demand breathing exercises
- Break stress cycles with immediate interventions

✅ **Habit Tracking:**
- Increase awareness of nervous habits
- Progressive intervention as severity increases
- Gentle nudges toward healthier patterns

✅ **Wellness & Self-Care:**
- Guided meditation and breathing
- Fatigue management
- Break reminders and energy recovery

## Technical Details

### MediaPipe Models Used
- **Hands Solution** - 21-point hand landmark detection
- **Pose Solution** - 33-point full-body pose estimation
- **Face Mesh** - 468-point facial landmark detection

### Performance
- Real-time processing at ~30 FPS
- Minimal latency for gesture feedback
- Lightweight overlay rendering
- Efficient frame processing pipeline

## Known Limitations

- Requires adequate lighting for accurate detection
- Works best with upper-body visibility in camera frame
- Gesture recognition may be affected by:
  - Extreme camera angles
  - Poor lighting conditions
  - Occlusions or partial visibility
  - Fast or jerky movements

## Future Enhancements

- 🎵 Expanded audio intervention library
- 📊 User analytics and habit tracking dashboard
- 🧘 Customizable meditation content
- 🌙 Darkmode and accessibility options
- 💾 Session history and progress tracking
- 🎮 Gamification and reward system

## Troubleshooting

**No gesture recognition:**
- Ensure good lighting (natural or bright indoor lighting)
- Keep hands clearly visible to camera
- Maintain stable camera position
- Check webcam is properly connected

**Audio not playing:**
- Verify audio files are in project directory
- Check system volume settings
- Ensure pygame audio support is installed

**Poor posture detection:**
- Position camera to capture full upper body
- Ensure good lighting on torso and shoulders
- Maintain clear visibility of spine and shoulders

**Performance issues:**
- Close unnecessary background applications
- Ensure adequate CPU/GPU resources
- Reduce camera resolution if needed
- Check system temperature

## Contributing

Contributions are welcome! Please feel free to submit issues and enhancement requests.

## License

MIT License - See LICENSE file for details

## Authors

**ZenSpace Development Team**
- Built for Ultron 9.0 Hackathon (Top 35)

## Support

For issues, feature requests, or questions:
1. Check existing documentation
2. Review code comments and docstrings
3. Submit detailed issue reports on GitHub

---

**Stay zen. Stay focused. Stay healthy.** 🧘‍♂️✨
