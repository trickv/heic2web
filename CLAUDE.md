# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a utility for converting HEIC image files to web-compatible formats (JPEG, PNG, and WebP). The tool leverages Pillow and pillow_heif libraries to handle HEIC files that many Linux libraries cannot process natively.

## Architecture

- **Single script utility**: `heic2web` - A standalone Python script that handles HEIC to JPEG/PNG/WebP conversion
- **UV script format**: Uses `uv run` shebang with inline dependencies (Pillow, pillow_heif)
- **CLI interface**: Uses argparse for command-line argument parsing with support for multiple files and output formats

## Running the Tool

```bash
# Convert single file to JPEG (default)
./heic2web image.HEIC

# Convert to PNG format
./heic2web -f png image.HEIC

# Convert to WebP format
./heic2web -f webp image.HEIC

# Convert with specific JPEG quality
./heic2web -q 85 image.HEIC

# Convert multiple files
./heic2web *.HEIC

# Force overwrite existing files
./heic2web --force image.HEIC
```

The script requires UV to be installed for dependency management. Dependencies are declared inline in the script header.

## Key Implementation Details

- Uses `pillow_heif.register_heif_opener()` to enable HEIC support in Pillow
- Supports JPEG, PNG, and WebP output formats
- Converts images to appropriate color modes (RGB for JPEG, RGBA for PNG from palette mode)
- Configurable quality for JPEG and WebP (1-100, default 95)
- File overwrite protection with interactive prompts (bypassed with --force)
- Follows UNIX utility conventions for error messages and return codes
- Returns appropriate exit codes (0 for success, 1 if any conversions failed)
- Provides conversion statistics for batch operations
## Development Guidelines

- Follow standard UNIX utility conventions (proper arguments, return codes, ASCII-only output)
- Allow potentially destructive operations when explicitly requested (e.g., --force)
- User should not be expected to care about implementation details beyond needing `uv` installed
- When adding features, maintain the simple single-script architecture
- Preserve inline dependency declarations in the script header
- When making changes, prompt the user to make incremental git commits as this repo will be published for others to borrow from.

## Future Enhancement Ideas

Additional UNIX utility conventions to consider:
- `--version` flag to show version information
- `-v/--verbose` mode for detailed output during batch operations
- `-q/--quiet` mode to suppress non-error output
- Stdin support for reading filenames (e.g., `find . -name "*.HEIC" | heic2web`)
- `-n/--dry-run` mode to preview operations without executing them
- Man page documentation
