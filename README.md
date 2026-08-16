# Social Media Downloader API

A Flask-based backend that provides a unified HTTP interface for downloading supported public media through `yt-dlp`.

> **Important:** Only download content you have permission or legal rights to download. Platform terms and copyright rules still apply.

## Overview

The project combines a lightweight Flask API with resource controls intended to prevent a public downloader from exhausting server resources.

```text
Client
  ↓
Flask API
  ↓
Validation / rate limits
  ↓
yt-dlp
  ↓
Temporary media file
  ↓
Response
  ↓
Cleanup
```

## Features

- YouTube, Instagram, Facebook and X/Twitter support through `yt-dlp` where the installed extractor supports the requested URL
- Per-IP rate limiting
- Concurrent download limits
- Maximum file-size enforcement
- Disk-space checks
- Automatic temporary-file cleanup
- Simple browser UI
- Suitable for local/VPS deployment with appropriate resource limits

## Tech stack

- Python
- Flask
- yt-dlp
- psutil
- HTML/CSS

## Installation

```bash
git clone https://github.com/mohith-krishnaa/socialmediadownloader.git
cd socialmediadownloader
python -m venv .venv
```

### Windows

```powershell
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python app.py
```

### Linux / macOS

```bash
source .venv/bin/activate
pip install -r requirements.txt
python app.py
```

Use the startup command defined by the repository if the application entry point differs from `app.py`.

## Configuration

Review the source for the available resource limits before deployment. Never commit API credentials or other secrets to the repository.

For a production deployment, configure limits appropriate for the host's CPU, RAM, disk capacity and network bandwidth.

## Security and abuse controls

The project includes application-level controls such as rate limiting, concurrency limits, file-size limits and disk checks. These are **resource-protection mechanisms**, not a complete security boundary.

A production deployment should also use HTTPS, request timeouts, reverse-proxy limits, process isolation and host-level monitoring.

## Limitations

- `yt-dlp` extractor support changes over time as platforms change their APIs and anti-bot measures.
- A supported platform does not mean every URL or account type will work.
- Downloading may fail because of authentication, geo-restrictions, rate limits, removed content or extractor changes.
- A public deployment can become expensive or abusive if resource limits are too permissive.

## Deployment

This application is better suited to a controlled server/VPS environment where temporary files, CPU, memory and bandwidth can be managed explicitly. Serverless platforms may impose execution-time, filesystem and binary-runtime constraints that make media downloads unreliable.

## Legal notice

This repository is provided for educational and personal-use purposes. Users are responsible for complying with applicable laws, copyright requirements and the terms of the platforms they access.

## License

See the repository license for the applicable terms.

## Author

**Mohith Krishnaa** — [@mohith-krishnaa](https://github.com/mohith-krishnaa)
