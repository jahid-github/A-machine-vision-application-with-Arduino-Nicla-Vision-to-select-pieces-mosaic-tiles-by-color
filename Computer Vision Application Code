# Use this code only for openMV IDE software
import sensor
import time

# Initialize the camera
sensor.reset()                      # Reset and initialize the sensor
sensor.set_pixformat(sensor.RGB565) # Set pixel format to RGB565
sensor.set_framesize(sensor.QVGA)   # Set frame size to QVGA (320x240)
sensor.skip_frames(time=2000)       # Let the camera adjust
sensor.set_auto_gain(False)         # Disable auto gain for consistent color detection
sensor.set_auto_whitebal(False)     # Disable auto white balance
clock = time.clock()                # Track elapsed time

# Define color thresholds (HSV values)
# Adjust these thresholds using OpenMV's threshold editor
thresholds = {
    "red":       (30, 100, 15, 127, 15, 127),
    "green":     (30, 100, -64, -8, -32, 32),
    "blue":      (0, 30, 0, 64, -128, 0),
    "yellow":    (30, 100, -10, 10, 30, 127),
    "orange":    (30, 100, 30, 127, 15, 127),
    "pink":      (50, 100, 15, 127, 15, 127),
    "purple":    (30, 100, 15, 127, -128, -8),
    "dark red":  (20, 70, 15, 50, -20, 20),
    "brown":     (30, 70, 10, 40, 10, 60),
    "black":     (0, 30, -20, 20, -20, 20),
    "white":     (0, 30, -128, 128, -128, 128)
}
#Below line: Just use this code only for checking in one color
"""
thresholds = {
    "red":       (30, 100, 15, 127, 15, 127), 
}"""

while True:
    clock.tick()                    # Start measuring frame time
    img = sensor.snapshot()         # Capture an image

    # Loop through each color threshold
    for color_name, threshold in thresholds.items():
        # Detect blobs for the current color
        blobs = img.find_blobs([threshold], pixels_threshold=200, area_threshold=200, merge=True)

        for blob in blobs:
            # Draw a rectangle around the detected blob
            img.draw_rectangle(blob.rect(), color=(255, 255, 255)) # White rectangle
            img.draw_cross(blob.cx(), blob.cy(), color=(0, 0, 0))  # Black cross

            # Label the blob with its color name
            img.draw_string(blob.x(), blob.y() - 10, color_name, color=(255, 255, 255), scale=1)

            # Print detected blob information
            print(f"{color_name} detected at: {blob.cx()}, {blob.cy()}")

    # Print FPS (optional)
    print("FPS:", clock.fps())

