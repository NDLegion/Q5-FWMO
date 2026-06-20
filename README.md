# Q5-FWMO

# Game Automation Tools Suite 🤖
 
A collection of Python-based automation scripts for game interaction, designed for **RP servers** and similar game environments. These tools provide reliable color-based triggering, object detection, and interactive automation.
 
**⚠️ Disclaimer:** These tools are for personal use and educational purposes. Use responsibly and ensure compliance with game terms of service and anti-cheat policies.
 
---
 
## 📋 Tools Overview
 
### 1. **MILK 6.13** - Mini-Game Interaction Bot
**File:** `__milk6_13.py`
 
#### Purpose
Automates the white marker detection mini-game mechanic (typically found in GTA V RP fishing/farming interactions).
 
#### Features
- ✅ **Dual-color trigger detection** - Responds to green and yellow indicator colors
- ✅ **Polygon-based zone detection** - Precise detection area configuration
- ✅ **Semi-transparent overlay status** - Real-time visual feedback (IDLE/ON/OFF states)
- ✅ **Auto start/stop** - Color-triggered automation
- ✅ **F9 manual toggle** - Instant start/stop control
- ✅ **Config file persistence** - Settings saved to `config.json`
- ✅ **GUI configuration tools** - Visual point and zone picker overlays
#### Configuration
```python
start_stop_point = (1318, 668)  # Trigger color detection point
polygon_coords = [[1465, 503], [1803, 502], [1820, 850], [1441, 863]]  # Detection zone
 
start_stop_colors = [
    (125, 192, 170),  # Green color
    (216, 218, 108)   # Yellow color
]
```
 
#### Known Issues & Limitations
- ❌ **Trigger detection reliability** - Color matching can fail if screen brightness changes
- ❌ **UI overlapping** - If game HUD elements overlap trigger point, detection fails
- ❌ **Fixed resolution** - Currently hardcoded for specific screen coordinates
- ❌ **Anti-cheat detection risk** - Consistent perfect accuracy may trigger anti-bot systems
#### Future Improvements
- [ ] Dynamic resolution scaling
- [ ] Multi-monitor support
- [ ] Brightness/contrast auto-adjustment
- [ ] Randomized timing to reduce detection risk
---
 
### 2. **ORANGE PICKER 1.0** - Object Detection & Drag Automation
**File:** `oranges_1_0.py`
 
#### Purpose
Detects circular objects (oranges) in a defined screen zone and automatically drags them to a drop zone. Optimized for 2560×1440 (2K) resolution.
 
#### Features
- ✅ **Advanced color detection** - HSV-based orange color detection with Gaussian blur
- ✅ **Morphological operations** - Separation of touching objects using erosion/dilation
- ✅ **Circularity & aspect ratio filtering** - Reduces false positives
- ✅ **Smart memory system** - Prevents re-picking same objects (3-second expiration)
- ✅ **Touch/overlap detection** - Handles oranges placed 5-10px apart or overlapping
- ✅ **Auto start/stop triggers** - E button (yellow) and green point detection
- ✅ **F9 instant control** - Manual start/stop with responsive interruption
- ✅ **2x speed optimization** - All timings tuned for fast processing
#### Configuration
```python
DETECTION_ZONE = {'x': 40, 'y': 0, 'width': 1710, 'height': 1440}
DROP_ZONE_CENTER = {'x': 2060, 'y': 920}
 
ORANGE_LOWER = np.array([10, 140, 120])  # HSV range
ORANGE_UPPER = np.array([25, 255, 255])
 
POSITION_TOLERANCE = 100  # px - exclusion zone for memory
MEMORY_TIME = 2.0  # seconds - how long to remember picked positions
```
 
#### Detection Process
1. Capture screen region
2. Convert RGB → HSV color space
3. Color range filtering
4. Gaussian blur (noise reduction)
5. Morphological open/close
6. **Erosion × 2 + Dilation × 2** (separate touching objects)
7. Find contours
8. Apply filters: circularity (0.55+), aspect ratio (0.6-1.4), area size
9. Calculate center of mass
10. Memory check (avoid duplicates)
11. Drag to drop zone
#### Known Issues & Limitations
- ❌ **Color range sensitivity** - Orange detection may fail with different lighting conditions
- ❌ **Touch detection edge case** - Very close objects (< 5px) may still be detected as one
- ❌ **Top UI elements** - Currently ignores objects at y < 100px (may miss some oranges)
- ❌ **Fixed resolution** - Coordinates hardcoded for 2560×1440
- ❌ **No simultaneous multi-dragging** - Can only pick one orange at a time
- ❌ **Memory time tradeoff** - 2.0s memory prevents re-picks but may skip if re-spawned quickly
#### Future Improvements
- [ ] Dynamic resolution detection & scaling
- [ ] Adjustable HSV range via GUI
- [ ] Real-time detection visualization (debug mode)
- [ ] Contour splitting algorithm for heavily overlapping objects
- [ ] Parallel processing for faster detection
- [ ] Configuration file support
- [ ] Multiple drop zones support
- [ ] Statistics tracking (objects/minute, efficiency)
---
 
### 3. **WOOD CLICKER** - Simple E-Trigger Click Bot
**File:** `wood.py`
 
#### Purpose
Monitors a specific color point and automatically performs rapid mouse clicks when that color appears (useful for wood-chopping or similar mechanics).
 
#### Features
- ✅ **Color-based triggering** - Activates on specific RGB values
- ✅ **Configurable click count** - Customizable number of clicks per trigger
- ✅ **Adjustable delays** - Separate timing for before/between clicks
- ✅ **F9 toggle control** - Instant start/stop
- ✅ **Direct input** - Uses `pydirectinput` for reliable input
- ✅ **Busy flag** - Prevents overlapping trigger cycles
#### Configuration
```python
CHECK_X, CHECK_Y = 1268, 1256  # Trigger point
TARGET_COLOR = (254, 188, 32)  # RGB color to match
TOLERANCE = 10  # Color matching tolerance
 
CLICK_COUNT = 10  # Number of clicks per trigger
DELAY_BEFORE_CLICK = 1.5  # Seconds before first click
DELAY_BETWEEN_CLICKS = 1.5  # Seconds between clicks
```
 
#### Known Issues & Limitations
- ❌ **Single point monitoring** - Only checks one coordinate
- ❌ **Color precision** - Sensitive to lighting changes
- ❌ **No anti-cheat evasion** - Predictable timing patterns
- ❌ **Busy blocking** - Waits for entire click sequence to finish
#### Future Improvements
- [ ] Multi-point triggering
- [ ] Randomized delays to evade detection
- [ ] Adjustable click types (single, double, hold)
- [ ] Visual feedback overlay
---
 
### 4. **CURSOR LOGGER** - Mouse Position Tracker
**File:** `cursor.py`
 
#### Purpose
Simple utility to log mouse click positions. Useful for identifying and calibrating click points for other tools.
 
#### Features
- ✅ **Left/Right click detection** - Logs both button types
- ✅ **Real-time coordinates** - Prints (x, y) position of clicks
- ✅ **Background monitoring** - Doesn't interfere with normal mouse usage
#### Usage
```bash
python cursor.py
# Click anywhere on screen
# Output: Натиснута ліва кнопка миші в точці (x=1242, y=1254)
```
 
---
 
## ⚙️ System Requirements
 
- **Python 3.8+**
- **Operating System:** Windows 10/11 (most scripts use Windows-specific APIs)
- **Screen Resolution:** 2560×1440 (2K) - scripts are optimized for this
- **Dependencies:**
```bash
pip install pyautogui keyboard pillow opencv-python numpy pydirectinput pynput
```
 
### Optional GUI Requirements
- `tkinter` - Usually included with Python on Windows
- For color overlays: Direct graphics rendering (native Windows)
---
 
## 🚀 Installation & Setup
 
1. **Clone the repository**
```bash
   git clone https://github.com/yourusername/game-automation-tools.git
   cd game-automation-tools
```
 
2. **Install dependencies**
```bash
   pip install -r requirements.txt
```
 
3. **Configure coordinates** (Critical!)
   - Run `cursor.py` to identify click positions
   - Update configuration in each script with YOUR screen coordinates
   - Run setup overlays to mark zones visually (MILK 6.13)
4. **Test in isolated environment**
   - Always test on a fresh game instance
   - Verify color values with cursor logger
5. **Run the tool**
```bash
   python oranges_1_0.py      # Orange picker
   python __milk6_13.py        # Mini-game bot
   python wood.py              # Click bot
```
 
---
 
## 🔧 Troubleshooting Guide
 
### General Issues
 
| Problem | Solution |
|---------|----------|
| **Script not detecting triggers** | Run `cursor.py` to verify exact pixel colors. Lighting/brightness may have changed. |
| **Tool stops responding** | Check if game window lost focus. Some tools pause when not in focus. |
| **False positives** | Increase `TOLERANCE` or `CIRCULARITY` thresholds slightly. |
| **Missing dependency error** | Run `pip install -r requirements.txt` |
| **Anti-cheat ban risk** | Reduce script accuracy, add randomized delays, avoid running 24/7 |
 
### MILK 6.13 Specific
 
| Problem | Solution |
|---------|----------|
| **Color trigger not working** | Check `start_stop_point` coordinates. Use cursor.py to verify. Brightness changed? |
| **Overlay not visible** | Ensure `-topmost` is supported. Try running as administrator. |
| **Detection zone wrong** | Click "Choose circle zone" button to reconfigure visually. |
| **Config not loading** | Delete `config.json` and restart to regenerate. |
 
### Orange Picker Specific
 
| Problem | Solution |
|---------|----------|
| **Oranges not detected** | Adjust `ORANGE_LOWER` and `ORANGE_UPPER` HSV values. Check lighting. |
| **Re-detecting same orange** | Increase `MEMORY_TIME` or `POSITION_TOLERANCE`. |
| **Picking objects at top** | Decrease `if y < 100:` threshold. Current value ignores top 100px. |
| **Touching oranges missed** | They're likely being treated as one "8" shape. Erosion/dilation might need tuning. Increase `separation_kernel` iterations. |
| **Wrong drop zone** | Verify `DROP_ZONE_CENTER` matches visual box location. Use cursor.py to find center. |
| **Slow detection** | Reduce `DETECTION_PAUSE` (currently 0.03s). Increase `BLACKOUT_AFTER_DRAG` reduction. |
 
### Wood Clicker Specific
 
| Problem | Solution |
|---------|----------|
| **Not clicking** | Verify `TARGET_COLOR` using cursor.py. Yellow/orange colors are tricky. |
| **Clicking too slowly** | Reduce `DELAY_BETWEEN_CLICKS`. Currently 1.5s - try 1.0s. |
| **Getting stuck** | Increase `DELAY_BEFORE_CLICK` to give game time to update state. |
 
---
 
## ⚠️ Known Risks & Anti-Cheat Considerations
 
### Why Detection Risk Exists
- ✅ **Mousedown/mouseup patterns** - If you always click the exact same duration, it's detectable
- ✅ **Perfect accuracy** - Humans miss clicks. Perfect accuracy = bot flag
- ✅ **Consistent timing** - Humans have reaction time variation. Machines don't.
- ✅ **Operating outside normal input ranges** - Very fast clicks or drag operations
### Mitigation Strategies
1. **Add randomization** - Vary delays by ±10-20%
2. **Simulate human error** - Occasionally miss or overshoot
3. **Variable timing** - Don't always wait the exact same duration
4. **Take breaks** - Alternate with manual play
5. **Don't run 24/7** - Short sessions (30-60 min) are less suspicious
### Example Randomization
```python
import random
 
def random_delay(base_delay, variance=0.15):
    """Add variance to delays (e.g., 1.0s ±15%)"""
    return base_delay * (1 + random.uniform(-variance, variance))
 
time.sleep(random_delay(DELAY_BETWEEN_CLICKS))
```
 
---
 
## 📊 Performance Metrics (2K Resolution)
 
| Metric | Value | Notes |
|--------|-------|-------|
| **Orange detection speed** | ~30-50ms | Per frame capture + processing |
| **Drag operation time** | ~200ms | Move + interact + blackout |
| **Maximum pick rate** | ~5-6 oranges/minute | At optimal conditions |
| **Memory overhead** | ~50MB | Python + OpenCV + libraries |
| **CPU usage** | 5-15% | Depends on detection complexity |
 
---
 
## 📝 Configuration Best Practices
 
### For Each Tool
1. **Use cursor.py to find exact coordinates** - Don't guess
2. **Test color tolerance** - Start with 10, increase if unreliable
3. **Screenshot reference state** - Keep screenshots of working configuration
4. **Document your coordinates** - Comment why each zone exists
5. **Version your configs** - Keep backup of working settings
### Resolution Handling
All scripts are hardcoded for **2560×1440**. For other resolutions:
 
```python
# Option 1: Calculate scale factor
REFERENCE_WIDTH, REFERENCE_HEIGHT = 1279, 717
SCALE_X = SCREEN_WIDTH / REFERENCE_WIDTH
SCALE_Y = SCREEN_HEIGHT / REFERENCE_HEIGHT
 
# Option 2: Use relative positioning
# Calculate percentages instead of absolute pixels
```
 
---
 
## 🔄 Update History
 
### Version 1.0 (Current)
- ✅ MILK 6.13: Dual-color detection with overlay
- ✅ Orange Picker: Touching object separation, 2x speed
- ✅ Wood Clicker: Stable click automation
- ✅ Cursor Logger: Position tracking
### Planned
- [ ] Dynamic resolution scaling
- [ ] Configuration GUI
- [ ] Anti-cheat evasion module
- [ ] Statistics tracking
- [ ] Multi-monitor support
---
 
## 📄 License
 
Personal use only. Do not distribute or sell.
 
**Terms of Use:**
- For educational/personal experimentation
- Comply with game terms of service
- No commercial use
- No modifications sold/shared without permission
- Author assumes no responsibility for bans/detections
---
 
## 🤝 Contributing
 
Found a bug? Have a suggestion?
 
1. Test in isolation environment first
2. Document exact reproduction steps
3. Include screen resolution and OS
4. Provide color values (use cursor.py)
5. Share relevant configuration snippets
---
 
## 📧 Support
 
**Common Questions:**
 
**Q: Will this get me banned?**
A: Depends on anti-cheat system. Use randomization, vary timing, don't run 24/7.
 
**Q: Why detect oranges by color instead of OCR?**
A: Color-based detection is faster (30-50ms vs 200-500ms) and more reliable.
 
**Q: Can I use this on Linux/Mac?**
A: Some tools use Windows-specific APIs. Would need refactoring for cross-platform.
 
**Q: Why is my detection failing?**
A: 99% of issues = wrong coordinates or changed lighting. Use cursor.py first.
 
**Q: How do I add more triggers?**
A: Duplicate the `check_color` functions and extend the main loop logic.
 
---
 
## 🛠️ Advanced Tweaking
 
### Adjusting Orange Detection Sensitivity
 
```python
# More sensitive (picks smaller/darker oranges)
ORANGE_LOWER = np.array([8, 130, 100])
ORANGE_UPPER = np.array([30, 255, 255])
MIN_ORANGE_AREA = 1000  # Smaller minimum
 
# More strict (ignores faint colors/shadows)
ORANGE_LOWER = np.array([12, 150, 140])
ORANGE_UPPER = np.array([20, 255, 255])
MIN_ORANGE_AREA = 2000  # Larger minimum
```
 
### Tuning Separation (Touching Objects)
 
```python
# Current (2 erosions, 2 dilations):
separation_kernel = np.ones((7,7), np.uint8)
mask = cv2.erode(mask, separation_kernel, iterations=2)
mask = cv2.dilate(mask, separation_kernel, iterations=2)
 
# More aggressive separation:
mask = cv2.erode(mask, separation_kernel, iterations=3)
mask = cv2.dilate(mask, separation_kernel, iterations=3)
 
# Gentler separation:
mask = cv2.erode(mask, separation_kernel, iterations=1)
mask = cv2.dilate(mask, separation_kernel, iterations=1)
```
 
---
 
## 📚 References
 
- **OpenCV Documentation**: https://docs.opencv.org/
- **PyAutoGUI**: https://pyautogui.readthedocs.io/
- **HSV Color Space**: https://en.wikipedia.org/wiki/HSL_and_HSV
- **Color Picker Online**: https://htmlcolorcodes.com/
---
 
**Last Updated:** June 2026  
**Author:** NDLEGION (Python Game Automation)  
**Status:** Stable (v1.0)
 
---
 
*This suite represents months of optimization and refinement. Use responsibly.* ⚙️✨

*Quadt RP Farm Cheats
