# Bcachefs Pro Windows v5.0 (Ultra Fast Extract Engine) 🚀

An innovative, non-destructive, and high-performance user-space hybrid storage utility inspired by Linux's **Bcachefs** architecture. 

This engine optimizes the data flow between a **Long-Term HDD (Safe Source)** and an **Ultra-Fast SSD (Target Cache)**. It utilizes a highly optimized, multi-threaded **Rclone Synchronization Engine** paired with an automated post-transfer **Native Windows LZX Compression Layer**, completely bypassing standard Windows Explorer bottlenecks and file system stalls.

Specially developed and tailored for clean, lightweight, or de-bloated operating systems (such as *Windows X-Lite, AtlasOS, or ReviOS*) where native Microsoft subsystems like WSL2 or Windows Storage Spaces are stripped out or unavailable.

---

## 🌟 Key Innovations & Architecture

Unlike generic copy scripts or basic backup utilities, **Bcachefs Pro Windows v5.0** introduces advanced low-level I/O optimizations straight into user-space:

*   **Safe Mirroring & Drive Flattening (`rclone sync`):** Your master HDD source directory remains **100% intact and untouched**. The engine safely mirrors its contents onto the fast SSD. Any residual or orphan files left on the SSD that no longer exist on the HDD source are automatically purged, keeping your active cache pristine.
*   **Ultra Fast-Transfer Mode (Hardware Saturation):**
    *   `--fast-list`: Scans and maps the directory structure directly into RAM, eliminating linear directory listing latency.
    *   `--use-mmap`: Leverages Memory-Mapped I/O to handle file operations natively in system memory, significantly lowering CPU overhead.
    *   `--buffer-size 64M`: Allocates a generous sequential memory cache per stream to keep the mechanical HDD read-head pinned at maximum hardware throughput.
    *   `--multi-thread-streams`: Dynamically splits large standalone files into parallel chunk streams to saturate your hardware buses.
*   **Post-Transfer Native Block Compression (LZX Engine):** The second the Rclone sync wrapper achieves 100% completion, an async `.bat` supervisor triggers. It runs Windows native LZX block-level deployment (`compact /exe:lzx`) directly onto the SSD folder, maximizing space savings with near-zero read performance penalties.

---

## 🛠️ Repository Tree & Setup

Ensure your local deployment workspace mirrors the file layout below:

```text
Bcachefs_Windows_v5/
├── bcachefs_v5.py        # Core Python Tkinter GUI & Synchronization Wrapper
├── rclone.exe              # Standalone Rclone Engine Binary (Must be placed here)
└── bcachefs_compressor.bat # Automatically generated at runtime for LZX compression
```

### 🛑 Mandatory System Prerequisites
1.  **Administrative Privileges:** The script automatically invokes a UAC prompt upon execution. This is strictly required to execute the native Windows file layout compression commands (`compact`).
2.  **Rclone Binary:** You must download the official `rclone.exe` executable for Windows and drop it inside the same folder as the Python script.
3.  **Python 3.10+** must be installed and properly configured in your system Environment Variables (`PATH`).

---

## 🚀 How to Run

1.  Confirm that **`rclone.exe`** resides in the exact same directory as your `bcachefs_v5.py` file.
2.  Open your terminal (**CMD** or **PowerShell**) as **Administrator** inside the project folder.
3.  Execute the supervisor script:
    ```bash
    python bcachefs_v5.py
    ```
4.  Interact with the graphical control dashboard:
    *   Select your **1. Sursa Principală HDD** — your long-term storage HDD source folder containing your original files (remains completely intact).
    *   Select your **2. Destinație SSD** — your official SSD target folder where files will be synchronized and compressed.
5.  Click the **"Lansează Sincronizarea Rapidă"** button to start the execution.
6.  The application will process the multi-threaded file pipeline in the background and pop open an automated console displaying the progress of the final LZX block compaction.
