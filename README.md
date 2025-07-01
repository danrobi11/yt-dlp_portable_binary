# Unofficial yt-dlp Portable Binary

This repository provides a GitHub Actions workflow to build a portable `yt-dlp` binary against the master branch for Linux systems. The binary is dynamically linked, includes FFmpeg, and is verified to launch successfully.

## About

`yt-dlp` is a feature-rich command-line tool for downloading audio and video content from various websites. This project automates the process of building a `yt-dlp` binary using Python 3.12.10 and FFmpeg 6.1.2, packaged with `PyInstaller` for ease of use.

## Features

- Builds `yt-dlp` against master branch.
- Includes FFmpeg for post-processing capabilities.
- Produces a dynamically linked binary for x86_64 Linux systems.
- Verifies binary functionality with `--version` and `--help` commands.
- Uploads the binary and build logs as GitHub Actions artifacts.

## Usage

1. **Trigger the Build**:
   - Push a commit to the `main` branch or manually trigger the workflow via the GitHub Actions tab.
   - The workflow builds the binary and uploads it as an artifact named `yt-dlp-binary`.

2. **Download the Binary**:
   - Navigate to the Actions tab in the repository.
   - Select the latest successful workflow run.
   - Download the `yt-dlp-binary` artifact, which includes `yt-dlp-dist-x86_64`.

3. **Run the Binary**:
   - Ensure your Linux system has compatible libraries (e.g., `libpython3.12.so`, `libavdevice.so.60`).
   - Make the binary executable: `chmod +x yt-dlp-dist-x86_64`.
   - Test the binary:
     ```bash
     ./yt-dlp-dist-x86_64 --version
     ./yt-dlp-dist-x86_64 --help
     ```
   - Use `yt-dlp` to download content, e.g.:
     ```bash
     ./yt-dlp-dist-x86_64 https://example.com/video
     ```

## Requirements

The binary requires a Linux system with the following libraries:
- `libpython3.12.so`
- `libavdevice.so.60` (and other FFmpeg libraries)
- Standard C libraries (e.g., `libc.so.6`)

## Workflow Details

The GitHub Actions workflow (`.github/workflows/main.yml`) performs the following:
- Installs dependencies in a `debian:bullseye-slim` container.
- Builds Python 3.12.10 with shared libraries.
- Builds FFmpeg 6.1.2 with required codecs and protocols.
- Installs `yt-dlp` 2025.05.22 and dependencies via `pip`.
- Uses `PyInstaller` to create a standalone `yt-dlp` binary.
- Verifies the binary’s functionality.
- Uploads the binary and logs as artifacts.

## Contributing

Contributions are welcome. Please open an issue or submit a pull request to suggest improvements or report bugs.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details. Note that `yt-dlp` and its dependencies have their own licenses.

## Acknowledgments

- Thanks to the [yt-dlp](https://github.com/yt-dlp/yt-dlp) project for providing a powerful downloader.
- Built with support from GitHub Actions and open-source tools like Python, FFmpeg, and PyInstaller.
