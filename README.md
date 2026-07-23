# Audio Level HUD (`audio-level-hud`)

A lightweight, always-on-top, Fluent 2-styled desktop overlay for Windows that displays real-time VU audio meters for both **Microphone Input** and **System Audio Output (Desktop Loopback)**.

Designed for streamers, content creators, gamers, and remote workers who need instant, at-a-glance confirmation that their microphone and system audio are live and capturing, without alt-tabbing away from full-screen games or applications.

---

## 🌟 Key Features

- **Dual Real-time VU Level Meters**:
  - **Microphone Input**: Real-time WASAPI peak metering for the default capture endpoint.
  - **System Audio Output**: Real-time WASAPI loopback peak metering for the default render endpoint.
- **Fluent 2 Design Matching Reference**:
  - **Segmented Audio Level Meters**: 25 discrete rounded vertical pill segments per row with color transitions (vibrant Fluent Green `#22C55E` for low/mid and Fluent Yellow `#F5B80D` for peak).
  - **Live dB Readouts**: Real-time decibel value display (e.g. `-12 dB`, `-8 dB`, `0 dB`, `-60 dB`) aligned on the right.
  - **Fluent Icons & Typography**: Native Segoe Fluent vector glyphs for Microphone (`Mic`) and System (`System`) audio.
  - **Acrylic / Mica Blur**: Translucent dark acrylic background card with smooth continuous rounded corners and subtle border glow.
  - **Horizontal Row Divider & Overflow Menu**: Clean horizontal line separating rows and 3-dot overflow menu (`⋮`) on the far right.
  - **Mute & Clip Alerts**: Segmented meter turns alert red when audio clips ($\ge 98\%$ peak level) and dims gray when muted.
- **Overlay Customization**:
  - **Screen Docking**: Corner snap options (`Top-Right`, `Top-Left`, `Bottom-Right`, `Bottom-Left`, `Custom`).
  - **Dimensions & Opacity**: Adjustable card width, height, and translucency percentage (10% - 100%).
  - **Input Pass-Through**: Click-through mode (`WS_EX_TRANSPARENT`) so mouse input passes seamlessly to windows underneath.
- **Global Hotkey Toggle**:
  - Press `Ctrl+Shift+M` (configurable) to instantly show or hide the overlay anytime.
- **Ultra Low Overhead**:
  - Queries kernel audio peak levels via WASAPI `IAudioMeterInformation` without buffer copying or audio buffer FFT computation.
  - Hardware-accelerated rendering using Direct2D & DirectWrite.
  - Configurable update rate (15 FPS, 30 FPS, 60 FPS).

---

## 🚀 Installation & Usage

1. Install [Windhawk](https://windhawk.net/).
2. Open Windhawk and click **Create Mod** (or open the Mod Manager).
3. Copy the entire contents of [`audio-level-hud.wh.cpp`](file:///x:/GitHub/audio-level-hud/audio-level-hud.wh.cpp) into the editor.
4. Click **Compile Mod** and **Save**.
5. Enable the mod. The HUD will instantly appear in the top-right corner of your desktop!

---

## ⚙️ Configuration Options

| Setting | Default | Description |
| :--- | :--- | :--- |
| **Screen Position** | `top-right` | Docking corner (`top-right`, `top-left`, `bottom-right`, `bottom-left`, `custom`). |
| **Horizontal Offset** | `24` | Margin distance in pixels from the screen edge or custom X position. |
| **Vertical Offset** | `24` | Margin distance in pixels from the screen edge or custom Y position. |
| **HUD Width** | `500` | Width of the overlay HUD card in pixels. |
| **HUD Height** | `104` | Height of the overlay HUD card in pixels. |
| **Card Opacity** | `88` | Translucency percentage of the card background (10% to 100%). |
| **Microphone Device** | `default` | Enter `default`, `communications`, or any mic name/brand substring (e.g. `Yeti`, `Realtek`, `Elgato`, `HyperX`, `Headset`). |
| **Show Microphone** | `true` | Toggle display of the microphone input meter bar. |
| **Show System** | `true` | Toggle display of the system audio output meter bar. |
| **Click-Through Mode** | `true` | When enabled, mouse clicks pass through the overlay. When disabled, drag the HUD to reposition. |
| **Toggle Hotkey** | `Ctrl+Shift+M` | Global keyboard shortcut to show/hide the HUD. |
| **Refresh Rate** | `30` | Target frame rate (15 FPS, 30 FPS, 60 FPS). |
| **Color Theme** | `fluent` | Visual palette (`fluent`, `neon`, `emerald`, `sunset`, `monochrome`). |

---

## 📐 Technical Architecture

- **Injection Target**: `explorer.exe` (Windows Desktop Shell).
- **Audio Metrics**: WASAPI `IMMDeviceEnumerator` + `IAudioMeterInformation` + `IAudioEndpointVolume`.
- **Rendering Pipeline**: Direct2D 1.0 (`ID2D1HwndRenderTarget`) + DirectWrite (`IDWriteFactory`).
- **Window Layering**: Win32 Layered Window (`WS_EX_TOPMOST` \| `WS_EX_LAYERED` \| `WS_EX_TOOLWINDOW` \| `WS_EX_NOACTIVATE`).

---

## 👨‍💻 Author

- **AKS HAY** ([@sysakshay](https://github.com/sysakshay))

---

## 📄 License

GNU General Public License v3.0 (GPL-3.0). Free to use, modify, and distribute according to the terms of the GPLv3 license.
