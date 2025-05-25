#os is used to interact with the operating system, like checking if folders and files exist.
#shutil is used to perform file operations, like copying files.
import os
import shutil

# User inputs for folder location, and transfer location
source_folder = input("Enter the source folder path: ").strip()
destination_folder = input("Enter the destination folder path: ").strip()
file_list_path = input("Enter the .txt file path with the filenames like eg IMG_0001.jpg : ").strip()

# Check if destination folder exists
if not os.path.isdir(destination_folder):
    print("Folder path not specified/found")
    exit()

# Read filenames from the text file
try:
    with open(file_list_path, 'r') as f:
        filenames = [line.strip() for line in f if line.strip()]
except FileNotFoundError:
    print("The .txt file with filenames was not found.")
    exit()

# Copy each file
for filename in filenames:
    source_file = os.path.join(source_folder, filename)
    dest_file = os.path.join(destination_folder, filename)

    if os.path.isfile(source_file):
        shutil.copy2(source_file, dest_file)
        print(f"Copied: {filename}")
    else:
        print(f"File not found: {filename}")
