# GET BONUS Scripts

This directory contains utility scripts for the GET BONUS project.

## Available Scripts

### 1. Image to Video Generator (`image_to_video_generator.py`)
Generate images and convert them into videos.

**Features:**
- Generate gradient images
- Generate geometric shapes
- Generate text overlays
- Apply filters (blur, sharpen, brightness, contrast, grayscale)
- Convert image sequences to MP4 videos
- Create custom slideshows

**Usage:**
```bash
python image_to_video_generator.py --mode demo
python image_to_video_generator.py --mode slideshow --fps 30 --duration 2.0
```

**Output:** `output/images/` and `output/videos/`

---

### 2. YouTube Uploader (`youtube_uploader.py`)
Upload generated videos to YouTube with automatic retry handling.

**Features:**
- OAuth2 authentication with caching
- Automatic retry on server errors
- Progress tracking
- Customizable metadata (title, description, tags, privacy)
- Resumable uploads for large files

**Setup:**
1. Create OAuth credentials at [Google Cloud Console](https://console.cloud.google.com)
2. Download credentials as `client_secret.json`
3. Place in project root

**Usage:**
```bash
python youtube_uploader.py output/videos/my_video.mp4 \
    --title "My Generated Video" \
    --description "Created with GET BONUS" \
    --tags AI Automation Gaming \
    --privacy private
```

---

## Workflow Example

### Complete Pipeline: Generate → Edit → Create Video → Upload

```bash
# 1. Generate images and create video
python scripts/image_to_video_generator.py --mode slideshow

# 2. Upload to YouTube
python scripts/youtube_uploader.py output/videos/slideshow.mp4 \
    --title "Game Intro Video" \
    --description "Auto-generated video for GET BONUS" \
    --privacy unlisted
```

---

## Project Structure

```
scripts/
├── image_to_video_generator.py    # Image generation & video creation
├── youtube_uploader.py             # YouTube upload utility
├── README.md                       # This file
└── examples/
    ├── create_game_intro.py        # Example: Game intro video
    ├── create_gradient_video.py    # Example: Gradient transitions
    └── batch_upload.py             # Example: Batch upload to YouTube
```

---

## Quick Start

### Install Dependencies
```bash
pip install -r requirements.txt
```

### Generate Sample Images & Video
```bash
python scripts/image_to_video_generator.py --mode demo
```

### View Results
Check the `output/` directory:
- Images: `output/images/`
- Videos: `output/videos/`

---

## API Documentation

### ImageGenerator Class

```python
from scripts.image_to_video_generator import ImageGenerator

gen = ImageGenerator(output_dir="my_output")

# Generate images
gen.generate_gradient_image(width=800, height=600, color1=(255,0,0), color2=(0,0,255))
gen.generate_geometric_image(width=800, height=600, bg_color=(255,255,255))
gen.generate_text_image(text="Hello", width=800, height=600)

# Edit images
gen.add_text_to_image("image.png", text="Overlay Text", font_size=40)
gen.apply_filter("image.png", filter_type="blur")

# Create videos
gen.images_to_video(output_filename="video.mp4", fps=30, duration_per_image=2.0)

# Create slideshows
slides = [
    {"type": "text", "text": "Slide 1"},
    {"type": "gradient", "color1": (255,0,0), "color2": (0,255,0)},
]
gen.create_slide_show_video(slides, output_filename="slideshow.mp4")
```

---

## Troubleshooting

### Missing Dependencies
```bash
pip install -r requirements.txt
```

### Font Issues
Install system fonts:
```bash
sudo apt-get install fonts-dejavu
```

### YouTube Upload Fails
- Ensure `client_secret.json` exists
- Check YouTube API is enabled in Google Cloud Console
- Verify OAuth credentials are valid

### Video Codec Issues
```bash
sudo apt-get install ffmpeg libsm6 libxext6
```

---

## Examples

See `examples/` directory for complete examples:
- `create_game_intro.py` - Create an animated game intro
- `create_gradient_video.py` - Create gradient transition video
- `batch_upload.py` - Upload multiple videos

---

## Contributing

Feel free to extend these scripts:
- Add new image generators
- Add new filters
- Add support for audio
- Add animation effects

---

## License

Same as GET BONUS project.
