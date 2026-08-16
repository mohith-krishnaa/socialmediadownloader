# Social Media Downloader API

A Flask-based backend that provides a browser UI and HTTP download endpoint for supported public media through `yt-dlp`.

> **Important:** Only download content you have permission or legal rights to download. Platform terms and copyright rules still apply.

## Overview

The application combines a lightweight Flask server with explicit resource controls so a download does not consume unlimited server resources.

```text
Client
  ↓
Flask /download
  ↓
Rate + concurrency checks
  ↓
yt-dlp extractor
  ↓
Temporary media file
  ↓
HTTP response
  ↓
Cleanup
```

## Features

- YouTube, Instagram, Facebook and X/Twitter URL handling through `yt-dlp`
- Per-IP rate limiting: **5 requests/minute**
- Maximum **2 concurrent downloads**
- Maximum **50 MB** downloaded file size
- Minimum **100 MB** free-disk-space requirement
- Automatic temporary-file cleanup
- Simple built-in browser UI
- Separate download directories by platform

The resource limits are defined directly in `app.py`. fileciteturn78file0

## Tech stack

- Python
- Flask
- yt-dlp
- psutil
- HTML/CSS/JavaScript

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

Then open the local address printed by Flask.

## Configuration

The current application does not require a project API key. `yt-dlp` handles extraction for supported URLs.

If you deploy this publicly, configure host-level resource limits and HTTPS in addition to the application-level controls.

## Resource protection

The application includes four important limits:

| Control | Current value |
|---|---:|
| Requests per IP | 5 / minute |
| Concurrent downloads | 2 |
| Maximum file size | 50 MB |
| Minimum free disk space | 100 MB |

These are **resource-protection mechanisms, not a complete security boundary**. A public deployment should also use a reverse proxy, HTTPS, process isolation, request timeouts, monitoring, and appropriate host-level limits.

## Limitations

- `yt-dlp` extractor support changes as platforms change their APIs and anti-bot measures.
- A supported platform does not mean every URL or account type will work.
- Downloads can fail because of authentication, geo-restrictions, rate limits, removed content or extractor changes.
- A public deployment can become expensive or abusive if resource limits are too permissive.
- In-memory rate-limit state is process-local and is not suitable for a multi-instance deployment without shared state.

## Deployment

This application is best suited to a controlled local machine, VPS, or server where temporary files, CPU, memory and bandwidth can be managed explicitly. Serverless environments can impose execution-time, filesystem and binary-runtime constraints that make media downloads unreliable.

## Legal notice

This project is provided for educational and personal-use purposes. Users are responsible for complying with applicable laws, copyright requirements and the terms of the platforms they access.

## License

See the repository license for the applicable terms.

## Author

**Mohith Krishnaa** — [@mohith-krishnaa](https://github.com/mohith-krishnaa)
