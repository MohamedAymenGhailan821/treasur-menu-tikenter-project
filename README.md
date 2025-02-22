# treasur-menu-tikenter-project
import tkinter as tk
from tkinter import simpledialog, colorchooser
from PIL import Image, ImageTk
import os

def change_resolution(width, height):
    root.geometry(f"{width}x{height}")

def toggle_mode():
    current_bg = root.cget("bg")
    new_bg = "white" if current_bg == "#654321" else "#654321"  # Using hex code for dark brown
    root.config(bg=new_bg)
    options_frame.config(bg=new_bg)
    for widget in options_frame.winfo_children():
        widget.config(bg=new_bg, fg="white" if new_bg == "#654321" else "black")

def show_options():
    main_frame.pack_forget()
    options_frame.pack(fill="both", expand=True)

def show_main_menu():
    options_frame.pack_forget()
    main_frame.pack(fill="both", expand=True)

def ask_player_name():
    name = simpledialog.askstring("Player Name", "Enter your name:")
    if name:
        player_name_label.config(text=f"Hello, {name}!")
        show_story(name)

def show_story(name):
    main_frame.pack_forget()
    story_frame.pack(fill="both", expand=True)
    story_label.config(text=f"A Treasure Finder, known for his relentless pursuit of rare artifacts, had heard whispers of a legendary treasure hidden deep within the unknown. This treasure, said to bring unimaginable wealth and power, was a prize no one had ever claimed. Determined to uncover it, the Treasure Finder set off on a journey full of danger and mystery, ready to face whatever challenges lay ahead.\n\n{name}, your adventure begins now!")
    # Load and display the image
    image_path = "trasure.jpeg"
    if os.path.exists(image_path):
        image = Image.open(image_path)
        image = image.resize((300, 200), Image.LANCZOS)  # Resize the image if needed
        photo = ImageTk.PhotoImage(image)
        image_label.config(image=photo)
        image_label.image = photo  # Keep a reference to avoid garbage collection
    else:
        print(f"Error: The image file '{image_path}' was not found.")

def quit_game():
    root.quit()

# Create the main window
root = tk.Tk()
root.title("Treasure Finder")
root.geometry("800x600")
root.config(bg="gold")

# Main menu frame
main_frame = tk.Frame(root, bg="gold")
main_frame.pack(fill="both", expand=True)

title = tk.Label(main_frame, text="Treasure Finder", font=("Helvetica", 36, "bold"), bg="gold", fg="black")
title.pack(pady=50)

player_name_label = tk.Label(main_frame, text="", font=("Helvetica", 18), bg="gold", fg="black")
player_name_label.pack(pady=10)

play_button = tk.Button(main_frame, text="Play", font=("Helvetica", 24, "bold"), bg="light green", command=ask_player_name)
play_button.pack(pady=20)

options_button = tk.Button(main_frame, text="Options", font=("Helvetica", 24, "bold"), bg="light green", command=show_options)
options_button.pack(pady=20)

quit_button = tk.Button(main_frame, text="Quit", font=("Helvetica", 24, "bold"), bg="tomato", command=quit_game)
quit_button.pack(pady=20)

# Options menu frame
options_frame = tk.Frame(root, bg="#654321")  # Using hex code for dark brown

resolution_label = tk.Label(options_frame, text="Resolution", font=("Helvetica", 18), bg="#654321", fg="white")
resolution_label.pack(pady=10)

resolution_800x600 = tk.Button(options_frame, text="800x600", font=("Helvetica", 14), bg="light green", command=lambda: change_resolution(800, 600))
resolution_800x600.pack(pady=5)

resolution_1024x768 = tk.Button(options_frame, text="1024x768", font=("Helvetica", 14), bg="light green", command=lambda: change_resolution(1024, 768))
resolution_1024x768.pack(pady=5)

resolution_1280x720 = tk.Button(options_frame, text="1280x720", font=("Helvetica", 14), bg="light green", command=lambda: change_resolution(1280, 720))
resolution_1280x720.pack(pady=5)

mode_toggle = tk.Button(options_frame, text="Toggle Light/Dark Mode", font=("Helvetica", 14), bg="light green", command=toggle_mode)
mode_toggle.pack(pady=20)

back_button = tk.Button(options_frame, text="Back", font=("Helvetica", 18), bg="light green", command=show_main_menu)
back_button.pack(pady=10)

# Story frame
story_frame = tk.Frame(root, bg="gold")
story_label = tk.Label(story_frame, text="", font=("Helvetica", 18), bg="gold", fg="black", wraplength=700, justify="left")
story_label.pack(pady=50)

# Image label for the story frame
image_label = tk.Label(story_frame, bg="gold")
image_label.pack(pady=20)

# Run the application
root.mainloop()
