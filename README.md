# Vinny's Terminal ASCII Player (VTAP)

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Installation and Setup](#installation-and-setup)
  - [Clone the Repository](#clone-the-repository)
  - [Install Dependencies](#install-dependencies)
- [Usage](#usage)
  - [Command-Line Arguments](#command-line-arguments)
  - [Examples](#examples)
- [How It Works](#how-it-works)
- [Contributing](#contributing)
- [License](#license)

## Overview

This project allows you to download a YouTube video and play it in your terminal as ASCII art with synchronized audio. It leverages multithreading to process video frames efficiently, ensuring smooth playback at the proper frames per second (FPS). Skipping frames as needed if unable to keep up with just multithreading.

**There is a bug that you have to press Ctrl+C twice to exit the program. when playing a video.**

### Features 

- **ASCII Art Video Playback:** Watch YouTube videos in your terminal as ASCII art.
- **Synchronized Audio:** Enjoy the video's audio alongside the ASCII art.
- **Customization Options:** Adjust the ASCII art scale, characters, and colors.
- **Demo Mode:** Play a demo video to test the functionality.
- **Multithreaded Processing:** Utilize multiple threads for efficient video processing.
- **Fullscreen Mode:** Fit the ASCII art to your terminal size. (Default, use `--fullscreen` to disable)
- **Colored ASCII Art:** Enable colored ASCII art for a more vibrant experience. (Default, use `--colors` to disable)
- **Display Pictures:** Display pictures in the terminal as ASCII art. (Default, use `--image_path` to specify a file path or url to an image)
    - ex. `python vtap.py --image_path 'https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png' --chars ' .:-=+*#%@'`
    - or `python vtap.py --image_path '~/Downloads/your_image.png' --chars ' .:-=+*#%@'`

## Prerequisites

Before you begin, ensure you have the following installed on your system:

- **Python 3.12**
- **ffmpeg** or **ffplay** (for audio playback)
- **pip** (Python package installer)

### Required Python Packages

- `pytube` (for downloading YouTube videos)
- `opencv-python` (for video processing)
- `numpy` (for numerical operations)
- `colorama` (for colored ASCII art) - allows color on Windows

You can install the Python packages using:

```bash
pip install -r requirements.txt
```

## Installation and Setup

### Clone the Repository

```bash
git clone https://github.com/VinnyVanGogh/vtap.git
```

### Install Dependencies

Navigate to the project directory and install the required packages:

```bash
cd vtap
pip install -r requirements.txt
```

Ensure that `ffmpeg` or `ffplay` is installed and accessible from your command line:

- **On macOS with Homebrew:**

  ```bash
  brew install ffmpeg
  ```

- **On Ubuntu/Debian:**

  ```bash
  sudo apt-get install ffmpeg
  ```

- **On Windows:**

  Download from [ffmpeg.org](https://ffmpeg.org/download.html) and add it to your system PATH.

## Usage

### Command-Line Arguments

The script accepts several command-line arguments to customize the playback:

- `--url`: **(Required)** The YouTube video URL.
- `--chars`: Characters to use for ASCII art (default: `' .:-=+*#%@'`).
- `--scale`: Scale factor for ASCII art (e.g., `0.5` for half size; default: `1.0`).
- `--colors`: Enable colored ASCII art.
- `--fullscreen`: Fit ASCII art to terminal size.
- `--demo`: Play a demo video. (Plays 'Dax - Eminem "Houdini" Remix [One Take Video](https://www.youtube.com/watch?v=zyefOCRZMpA)' with --chars '█▓▒░ ')
- `--image_path`: Display an image in the terminal as ASCII art. (e.g., `--image_path 'https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png'` or `--image_path '~/Downloads/your_image.png'`)


### Examples

**Demo Mode:**

```bash
python vtap.py --demo
```

**Basic Usage:**

```bash
python vtap.py --url 'https://www.youtube.com/watch?v=dQw4w9WgXcQ'
```

**Custom Characters and Scaling:**

```bash
python vtap.py --url 'https://www.youtube.com/watch?v=dQw4w9WgXcQ' --chars ' .:-=+*#%@' --scale 0.5
```

**Enable Colored ASCII Art:**

```bash
python vtap.py --url 'https://www.youtube.com/watch?v=dQw4w9WgXcQ' --colors
```

**Fullscreen Mode:**

```bash
python vtap.py --url 'https://www.youtube.com/watch?v=dQw4w9WgXcQ' --fullscreen
```

## How It Works

1. **Download Video:**

   The script uses `pytube` to download the specified YouTube video in MP4 format with both audio and video streams.

2. **Multithreaded Processing:**

   - **Frame Reading Thread:** Reads video frames and queues them for processing.
   - **Frame Processing Threads:** Multiple threads convert frames to ASCII art in parallel.
   - **Frame Display Thread:** Displays the ASCII frames in the terminal at the correct FPS.
   - **Audio Playback Thread:** Plays the video's audio simultaneously using `ffplay`.

3. **ASCII Art Generation:**

   - Each video frame is resized according to the specified scale or terminal size.
   - Frames are converted to grayscale and mapped to ASCII characters based on pixel intensity.
   - Optionally, color information is added using ANSI escape codes.

4. **Synchronized Playback:**

   - The display thread ensures that frames are shown at intervals matching the video's FPS.
   - Audio playback is synchronized with the video frames for a cohesive experience.

## Project Structure

```
vtap/
├── vtap.py
├── components/
├────── downloader.py
├────── ascii_art.py
├────── ascii_picture.py
├────── ascii_video.py
├────── audio_player.py
├────── my_args.py
├── requirements.txt
```

### File Descriptions

- **vtap.py:** The entry point of the program; parses arguments and initiates threads.
- **downloader.py:** Handles downloading the YouTube video.
- **ascii_art.py:** Contains the `AsciiArt` class for converting frames to ASCII art.
- **ascii_video.py:** Manages video playback, including multithreading for frame processing.
- **ascii_picture.py:** Manages picture display, displaying an image in the terminal as ASCII art.
- **audio_player.py:** Handles audio playback using `ffplay`.
- **my_args.py:** Contains the argument parser configuration.
- **requirements.txt:** Lists the required Python packages.

## Contributing

We welcome contributions to improve this project. To contribute, follow these steps:

1. **Fork the Repository:**

   Click the "Fork" button at the top right of the repository page.

2. **Clone Your Fork:**

   ```bash
   git clone https://github.com/<your-username>/vtap.git
   cd vtap
   ```

3. **Create a Branch:**

   ```bash
   git checkout -b 'feature/your-feature-name'
   ```

4. **Make Your Changes:**

   - Improve code efficiency.
   - Fix bugs.
   - Add new features.

5. **Commit Your Changes:**

   ```bash
   git commit -am 'Add your commit message here'
   ```

6. **Push to Your Fork:**

   ```bash
   git push origin feature/your-feature-name
   ```

7. **Create a Pull Request:**

   - Go to the original repository.
   - Click on "Pull Requests" and then "New Pull Request".
   - Select your branch and submit the pull request.

## License

This project is licensed under the [MIT License](LICENSE). You are free to use, modify, and distribute this software in accordance with the license.

---

**Disclaimer:** This project is intended for educational and personal use. Ensure you comply with YouTube's Terms of Service and respect copyright laws when downloading and using YouTube content.

---

## Troubleshooting

### Common Issues

- **SSL Certificate Error when Downloading Videos:**

  If you encounter an SSL error, you may need to install the necessary certificates. On macOS, run the `Install Certificates.command` script located in `/Applications/Python 3.13/` or `/opt/homebrew/bin/python3.12` replace 3.12 with your current version.

- **Slow Performance:**

  - Reduce the `--scale` factor to lower the resolution.
  - Use fewer characters in `--chars`.
  - Disable colors by omitting the `--colors` flag.

- **Audio Not Playing:**

  Ensure that `ffmpeg` or `ffplay` is correctly installed and accessible from your command line.

### Support

If you experience any issues or have questions, feel free to open an issue on the [GitHub repository](https://github.com/VinnyVanGogh/vtap/issues).

---
