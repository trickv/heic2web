# heic2web

Convert HEIC image files to web-compatible formats (JPEG, PNG, and WebP).

## Installation

### Prerequisites

- [uv](https://docs.astral.sh/uv/) (Python package manager)

### Installing heic2web in your PATH

1. **Clone or download this repository**
   ```bash
   git clone <repository-url>
   cd heic2web
   ```

2. **Make the script executable**
   ```bash
   chmod +x heic2web
   ```

3. **Install to your PATH** (choose one method):

   **Option A: Copy to a directory in your PATH**
   ```bash
   cp heic2web ~/.local/bin/
   # or
   sudo cp heic2web /usr/local/bin/
   ```

   **Option B: Create a symlink**
   ```bash
   ln -s $(pwd)/heic2web ~/.local/bin/heic2web
   ```

   **Option C: Add this directory to your PATH**
   ```bash
   echo 'export PATH="$PATH:'$(pwd)'"' >> ~/.bashrc
   source ~/.bashrc
   ```

## Usage

```bash
# Convert single file to JPEG (default)
heic2web image.HEIC

# Convert to PNG format
heic2web -f png image.HEIC

# Convert to WebP format
heic2web -f webp image.HEIC

# Convert with specific JPEG quality (1-100)
heic2web -q 85 image.HEIC

# Convert multiple files
heic2web *.HEIC

# Force overwrite existing files
heic2web --force image.HEIC

# Get help
heic2web --help
```

### Options

- `-f, --format {jpg,png,webp}` - Output format (default: jpg)
- `-q, --quality N` - Quality 1-100 for JPEG/WebP (default: 95, ignored for PNG)
- `--force` - Overwrite existing output files without prompting

## Features

- Converts HEIC files to JPEG, PNG, or WebP format
- Interactive prompts before overwriting existing files
- Configurable JPEG quality settings
- Batch processing support
- Standard UNIX utility conventions
- No dependencies to install - uses uv's inline script dependencies

## Dependencies

The script automatically manages its dependencies using uv:
- Pillow (PIL)
- pillow_heif

These are declared inline in the script and will be automatically installed when run with `uv run`.