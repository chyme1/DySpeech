# Import the required modules
import os
import tkinter as tk
import pygame
from gtts import gTTS
from io import BytesIO
import pyttsx3

# Initialize the pygame mixer for the media player
pygame.mixer.init()

# Initialize the text-to-speech engine
engine = pyttsx3.init()

# Function to convert text to speech and play it
def convert_text_and_play():
    text = input_text.get()
    if text:
        
        language = 'en'
        
        # Break the text into words
        words = text.split()
        audio_stream = BytesIO()

        for word in words:
            tts = gTTS(word, lang=language)
            tts.write_to_fp(audio_stream)
            audio_stream.write(b' ')  # Add a space between words

        # Get the latest word typed (the word after the last space)
        latest_word = text.split()[-1]

        audio_stream = BytesIO()
        tts = gTTS(latest_word, lang=language)
        tts.write_to_fp(audio_stream)
        audio_stream.seek(0)

        # Reset the stream position to the beginning
        audio_stream.seek(0)

        # Play the audio using pygame
        pygame.mixer.music.load(audio_stream)
        pygame.mixer.music.play()

# Function to stop playing the audio
def stop_audio():
    pygame.mixer.music.stop()

# Function to trigger convert and play when the spacebar or enter key is pressed
def on_key(event):
    if event.keysym in ('space', 'Return'):
        convert_text_and_play()

# Function to open the "About" window 
def open_about_window():
    about_window = tk.Toplevel(root)
    about_window.title("About")
    about_label = tk.Label(about_window, text="This is a Text to Speech Converter application.", font=("Helvetica", 12))
    about_label.pack()
    about_window.geometry("300x100")


# Function to break each word into its own sound as it's typed
def on_key_press(event):
    current_text = input_text.get()
    words = current_text.split()
    if len(words) >= 2 and current_text.endswith(" "):
        # New word detected, get the last word
        new_word = words[-1]
        tts = gTTS(new_word, lang='en')
        audio_stream = BytesIO()
        tts.write_to_fp(audio_stream)
        pygame.mixer.music.load(audio_stream)
        pygame.mixer.music.play()

# Create the main window
root = tk.Tk()
root.title("Text to Speech Converter")

# Welcome message and project description
welcome_label = tk.Label(root, text="Welcome to Text to Speech Converter", font=("Helvetica", 16, "bold"))
welcome_label.pack()
description_label = tk.Label(root, text="Enter text, adjust the speed, and click 'Convert and Play' to hear it!", font=("Helvetica", 12))
description_label.pack()

# Label to prompt for input
input_label = tk.Label(root, text="Enter the text you want to convert to audio:")
input_label.pack()

# Entry widget to input text
input_text = tk.Entry(root)
input_text.pack()

# Button to convert text and play sound
convert_button = tk.Button(root, text="Convert and Play", command=convert_text_and_play)
convert_button.pack()

# Button to open the "About" window
about_button = tk.Button(root, text="About", command=open_about_window)
about_button.pack()

# Bind space and enter key events to the convert and play function
root.bind('<space>', on_key)
root.bind('<Return>', on_key)
# Bind KeyPress event to break words into sounds as they are typed
input_text.bind("<KeyPress>", on_key_press)

# Start the GUI main loop
root.mainloop()

