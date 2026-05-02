# Playing .MOV Files on Windows

A guide to making `.mov` files play natively on any Windows media player without conversion, using the command line.

---

## The Problem

Windows does not ship with native support for `.mov` files (Apple QuickTime format). Without the right codecs installed, `.mov` files will either refuse to open or show an error in Windows Media Player and Films & TV.

---

## The Solution

Install **K-Lite Codec Pack Full** via **Chocolatey**. This installs system-wide DirectShow filters and codec support so every media player on the machine can read `.mov` files natively.

---

## Prerequisites

- Windows 10 or Windows 11
- Internet connection
- PowerShell run as Administrator

---

## Step 1: Open PowerShell as Administrator

1. Press `Windows + S`
2. Type `PowerShell`
3. Right click and select **Run as Administrator**

> Make sure the title bar says **Administrator: Windows PowerShell**

---

## Step 2: Install Chocolatey

Paste the following command and press Enter:

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Wait for it to complete. You should see a success message at the end.

> If you see a warning that Chocolatey is already installed but `choco` is not recognized, delete the broken install first:
> ```powershell
> Remove-Item -Recurse -Force "C:\ProgramData\chocolatey"
> ```
> Then rerun the install command above.

---

## Step 3: Install K-Lite Codec Pack Full

```powershell
choco install k-litecodecpackfull -y
```

This will download and install K-Lite Codec Pack Full (~55 MB). You should see:

```
The install of k-litecodecpackfull was successful.
Deployed to 'C:\Program Files (x86)\K-Lite Codec Pack'
```

---

## Step 4: Restart Your PC

Restart for the codecs to register properly with Windows.

After restarting, `.mov` files will play in:

- Windows Media Player
- Films & TV
- Any DirectShow-based media player
- File Explorer thumbnail previews

---

## Updating Later

To update K-Lite to the latest version in the future:

```powershell
choco upgrade k-litecodecpackfull -y
```

To upgrade all Chocolatey packages at once:

```powershell
choco upgrade all -y
```

---

## Why K-Lite Codec Pack

| Feature | K-Lite Full |
|---|---|
| .mov support | Yes |
| .mkv, .avi, .flv support | Yes |
| File Explorer thumbnails | Yes |
| LAV Filters included | Yes |
| Works with all media players | Yes |
| Free | Yes |

---

## Troubleshooting

**`choco` is not recognized after install**
Refresh the PATH manually:
```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")
```
If that does not work, delete `C:\ProgramData\chocolatey` and reinstall Chocolatey from Step 2.

**No internet connection**
Download K-Lite Full manually from [codecguide.com](https://www.codecguide.com/download_k-lite_codec_pack.htm) on another device, transfer via USB, and run the installer directly.

**Some .mov files still do not play**
`.mov` is a container format and can hold various codecs inside (H.264, ProRes, MJPEG). K-Lite covers the common ones. For Apple ProRes specifically, install [VLC Media Player](https://www.videolan.org/) as a fallback.

---

## License

MIT
