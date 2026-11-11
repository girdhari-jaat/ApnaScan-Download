<div align="center">
<img width="1200" height="475" alt="ApnaScan Banner" src="./banner.png" />
</div>
  # ApnaScan: High-Performance Offline Document Scanner

  **Enterprise-grade, privacy-first mobile document scanner built with native Kotlin, Jetpack Compose, CameraX, Google AI Edge LiteRT, OpenCV, and ML Kit.**

  [![Platform](https://img.shields.io/badge/Platform-Android%208.0%2B%20(API%2026--37)-3DDC84?logo=android&logoColor=white)](#build-configuration)
  [![Language](https://img.shields.io/badge/Language-Kotlin%202.x-7F52FF?logo=kotlin&logoColor=white)](#architecture)
  [![UI Framework](https://img.shields.io/badge/UI-Jetpack%20Compose%20%2F%20Material%203-4285F4?logo=jetpackcompose&logoColor=white)](#architecture)
  [![Privacy](https://img.shields.io/badge/Privacy-100%25%20Offline%20%7C%20Zero%20Internet-green?logo=shield&logoColor=white)](#privacy--offline-first-experience)
  [![Kernel](https://img.shields.io/badge/Kernel-16KB%20Page--Aligned-orange?logo=linux&logoColor=white)](#high-performance-processing)
  [![License](https://img.shields.io/badge/License-Proprietary-red)](#license))

  <p align="center">
    <a href="#-key-features">Key Features</a> •
    <a href="#-high-performance-processing">High-Performance Processing</a> •
    <a href="#-flexible-pdf-export">Flexible PDF Export</a> •
    <a href="#-annotation-studio">Annotation Studio</a> •
    <a href="#-architecture">Architecture</a> •
    <a href="#-localization-support">Localization Support</a> •
    <a href="#-privacy--offline-first-experience">Privacy</a> •
    <a href="#-build-configuration">Build Configuration</a>
  </p>
</div>

---

## 📖 Overview

**ApnaScan** is a modern, high-performance Android document scanner engineered for users and professionals who require uncompromising scan clarity, high execution speed, and absolute data privacy. 

Unlike traditional scanning applications that upload user documents to remote cloud servers, ApnaScan runs **100% on-device**. The application requests **zero internet permissions**, embeds lightweight computer vision engines directly into the binary, and utilizes a zero-copy pixel pipeline for lightning-fast camera previews, edge detection, perspective warping, and PDF generation.

---

## 🌟 Key Features

### 📷 1. Intelligent Hardware Capture
* **Native CameraX Engine**: Direct integration with Android's CameraX subsystem (`camera-camera2`, `camera-lifecycle`) providing hardware-negotiated resolution selection, continuous auto-focus, pinch-to-zoom, and torch controls.
* **Dynamic Hardware Negotiation**:
  * **HD (Fast)**: Optimized for ultra-low latency and quick multi-page snapping.
  * **FHD (Standard)**: Balanced high-resolution capture for typical day-to-day scanning.
  * **UHD (High)**: Maximum sensor resolution capture for fine text and legal documents.
* **Multiple Capture Modes**:
  * **DOCS Mode**: Automated document capture with aspect-ratio locking and edge snapping.
  * **ID Card Mode**: Specialized workflows for dual-sided identity cards (Front/Back) and single-sided cards with on-screen alignment guides.
* **ML Kit Document Scanner**: Embedded Google ML Kit Document Scanner integration for auto-detection, edge detection, and real-time document boundary recognition.
* **Batch Scanning**: Rapid multi-page capture supporting sessions of up to 50 pages with live slot management.

### 🎨 2. Advanced Non-Destructive Editing Studio
* **Magnetic Edge Cropping**: 4-point manual corner adjustment with magnified loupe preview and automatic boundary snapping.
* **Lossless Rotation**: 90-degree rotational transformations without generational compression loss.
* **Professional Color Filters**:
  * **Original**: Preserves authentic raw sensor capture.
  * **Magic Color**: High-contrast color enhancement designed to pop text while preserving photo elements.
  * **Paper / Clean White**: Removes page shadows and yellow tints, rendering clean, bright paper backgrounds.
  * **Card / ID**: Optimized for ID card holograms, micro-print, and high-frequency patterns.
  * **B&W (Binarization)**: High-precision Otsu thresholding for ultra-crisp, printer-ready monochrome text.
  * **Grayscale**: Smooth 8-bit tonal reduction.
* **Fine-Tuning Sliders**: Individual non-destructive adjustment for **Contrast**, **Brightness**, **Saturation**, and **Sharpness**.

### 🔍 3. QR & Barcode Recognition
* **On-Device Vision**: Integrated lightweight Google Play Services ML Kit Barcode Scanning (~200KB overhead).
* **Instant Extraction**: Scan barcodes and QR codes from existing scanned documents or live view with one-tap copy, share, and URL navigation.

---

## ⚡ High-Performance Processing

ApnaScan adheres to a strict performance, memory-safety, and battery-saver standard across all image transformations.

```
+-----------------------------------------------------------------------------------+
|                            ZERO-COPY PIXEL PIPELINE                               |
+-----------------------------------------------------------------------------------+
  [ Camera / File Input ]
            |
            v
  [ Sandbox Internal Storage ]  <--- (Original Raw Uncompressed Master File Saved)
            |
            v
  [ Coroutine Dispatcher.IO ]   <--- (Off-Thread Perspective Warp & Filtering)
            |
            v
  [ Non-Destructive JSON State ] <--- (Corners, Rotation, Sliders Stored as Metadata)
            |
            v
  [ Display Cache (Indexed/File) ] <--- (Immediate UI Feedback, Zero Main-Thread Janks)
            |
            v
  [ Direct Stream PDF Output ]  <--- (Native In-Memory Assembly & Jpeg Compression)
+-----------------------------------------------------------------------------------+
```

### Architectural Highlights:
* **Non-Destructive Metadata Architecture**: Original raw captures are stored untouched in sandboxed internal storage. All crops, rotations, filters, and annotations are maintained as immutable JSON metadata states. Edits can be adjusted or reverted at any point without degrading image quality.
* **Dual-Layer Caching Engine**:
  * **Display Render Cache**: Processed screen thumbnails and previews are cached on disk. Opening an existing document fetches instant cached previews without re-running CPU-intensive image filters.
  * **PDF Hash Cache (`currentHash`)**: Document changes are fingerprinted. If a user exports an unmodified document twice, the compiled PDF is served instantly from cache.
* **16KB Memory Page-Alignment**: Powered by Google AI Edge LiteRT (`2.3.0`), ensuring full forward compatibility with Android 15/16 16KB page-size Linux kernels for maximum memory throughput and reduced page faults.
* **Hardware Accelerated Offscreen Rendering**: All composite rendering, watermarking, and annotation merging occur in memory buffers using native Android Canvas matrices and native recycling routines (`bitmap.recycle()`).

---

## 📄 Flexible PDF Export

The PDF export engine provides deep configuration options to meet both personal and enterprise documentation standards:

| Configuration | Options Available | Details |
| :--- | :--- | :--- |
| **Page Sizes** | `Original`, `Auto`, `A4`, `Letter`, `Legal` | `Original` preserves exact 1:1 image geometry; standard sizes fit documents neatly into printable paper sheets. |
| **Orientation** | `Portrait`, `Landscape`, `Auto` | Dynamically auto-detects page aspect ratios or enforces unified orientation. |
| **Resolution (DPI)** | `72 DPI` (Fast/Draft), `150 DPI` (Standard), `300 DPI` (Print Quality) | Generates crisp text at 300 DPI or compact file sizes for email at 72/150 DPI. |
| **JPEG Quality** | `40%` to `95%` | Fine-grain compression control to target specific upload size limits. |
| **Card Layouts** | `Grid` (2-up), `Stack` (Side-by-side) | Formats Front & Back of ID cards on a single clean page. |
| **Security** | RC4 Password Encryption | Native PDF 1.4 encryption protects sensitive documents with user/owner passwords. |
| **Custom Watermark** | Any text / Unicode | Diagonally centered (-45°) with subtle ~18% opacity; keeps document content 100% legible. |
| **Page Numbering** | `1 / N` Clean Footer | Smart positioning: on `Original` pages, dynamically appends an extra bottom strip so page numbers never overlap or obscure document text. |
| **Actions** | Share, Save to Documents, Print | Direct Android share sheet, MediaStore public document storage, or direct printer dispatch via `PrintManager`. |

---

## ✍️ Annotation Studio

ApnaScan includes a built-in on-device markup and digital signature studio:

* **Pen & Signature**: Free-hand vector drawing with pressure-sensitive width simulation. Quick access signature drawer for signing contracts, receipts, and forms.
* **Highlighter & Marker**: Translucent highlighting brush with customizable stroke widths (2dp to 50dp) and smooth alpha blending.
* **Smart Eraser**: Erases annotation vectors and stroke paths only, leaving the underlying document image pristine.
* **Text Annotation**: Insert typed labels, dates, and notes with customizable typography, sizing, and colors.
* **Color Palette & Eyedropper**: 8 curated document markup colors plus an interactive eyedropper tool to pick any exact color from the document canvas.
* **Undo / Redo History**: Complete stroke-by-stroke undo/redo stack and one-tap canvas clearing.

---

## 🏗️ Architecture

ApnaScan is architected using Modern Android Development (MAD) best practices, following **Clean Architecture** and **Unidirectional Data Flow (UDF)**.

```
android/app/src/main/java/com/apnascan/
├── ApnaScanApplication.kt          # Application class, Hilt dependency root
├── MainActivity.kt                 # Single-activity container, Edge-to-Edge setup
├── data/                           # Data layer (Entities, DataStore, Repositories)
│   ├── ScannerMode.kt              # Modes: DOCUMENT, CARD
│   ├── Slot.kt                     # Document page model with bitmap/path references
│   └── FilterType.kt               # Image filter definitions
├── domain/                         # Business logic & Use Cases
│   ├── ExportPdfUseCase.kt         # PDF compilation coordination
│   ├── SaveDocumentUseCase.kt       # Document persistence & JSON metadata storage
│   └── AnnotationManager.kt        # Vector stroke management and JSON serialization
├── presentation/                   # UI Layer (Jetpack Compose, ViewModels)
│   ├── scanner/                    # Camera capture, ScannerViewModel, ExportHelper
│   ├── components/                 # Reusable Compose buttons, dialogs, sliders
│   └── dialogs/                    # ExportModalDialog, SettingsDialog, AboutDialog
├── ui/                             # Screens & Custom Layouts
│   ├── CaptureScreen.kt            # Live camera view, shutter, and guide overlays
│   ├── EditorScreen.kt             # Filter picker, tuning sliders, crop entry
│   ├── CropScreen.kt               # 4-point magnetic corner perspective warp
│   ├── DocumentGrid.kt             # Multi-page overview, reordering, batch export
│   └── theme/                      # Material 3 Color Schemes, Typography, Shapes
└── util/                           # Utilities & Native Bridges
    ├── PdfExporter.kt              # High-performance native PDF stream generation
    ├── OpenCVHelper.kt             # Native edge detection & perspective transformation
    └── DiagnosticsLogger.kt        # Lightweight zero-allocation diagnostics logger
```

### Core Technologies:
* **Jetpack Compose & Material 3**: 100% declarative UI with edge-to-edge layout, responsive animations, and Day/Night dynamic color theming.
* **Dagger Hilt (`2.60.1`)**: Compile-time dependency injection across ViewModels, UseCases, and Repositories.
* **Kotlin Coroutines & Flow**: Structured concurrency for all background processing, preventing main thread frame drops.
* **OpenCV 4.11.0**: Tailored lightweight AAR stripped for `arm64-v8a` (~6MB) for contour identification and homography warping.
* **Google AI Edge LiteRT (`2.3.0`)**: High-efficiency on-device AI runtime with 16KB page-alignment support.
* **Coil 3 (`3.6.3`)**: Asynchronous, memory-cached image rendering in Compose.

---

## 🔒 Privacy & Offline-First Experience

* 🚫 **No Internet Permission**: `android.permission.INTERNET` is **NOT** present in `AndroidManifest.xml`. The app cannot connect to the internet, make HTTP requests, or leak data.
* 🛡️ **Zero Analytics / Telemetry**: No Google Analytics, no Firebase Crashlytics, no Facebook SDK, and no background tracking daemons.
* 📁 **Sandboxed Local Storage**: Scans are stored in private internal application storage (`Context.filesDir`). Other apps cannot access your scanned documents.
* 🔐 **Hardware Sandboxing**: Camera access is used exclusively during active scanning sessions and is released immediately when switching screens or backgrounding the app.

---

## 🌍 Localization Support

ApnaScan provides full multi-language localization with native Right-to-Left (RTL) mirroring:

| Language | Locale Code | Direction | Native Name |
| :--- | :--- | :--- | :--- |
| **English** | `en` | LTR | English |
| **Urdu** | `ur` | RTL | اردو |
| **Sindhi** | `sd` | RTL | سنڌي |
| **Hindi** | `hi` | LTR | हिन्दी |

* Supported locales are declared in `res/xml/locales_config.xml`, supporting Android 13+ per-app language preferences.
* UI elements, action buttons, dialogs, hints, and error alerts dynamically mirror their layouts when an RTL locale is active.

---

## 🛠️ Build Configuration

### Prerequisites
* **Android Studio**: Ladybug / Meerkat or newer
* **JDK**: Java 17 (Azul Zulu or OpenJDK recommended)
* **Android SDK**: Compile SDK `37`, Target SDK `37`, Min SDK `26` (Android 8.0 Oreo)
* **NDK**: Version `25.x+` (Default ABI filter: `arm64-v8a`)

### Build Steps

#### 1. Clone the repository
```bash
git clone https://github.com/your-username/ApnaScan.git
cd ApnaScan/android
```

#### 2. Assemble Debug APK
```bash
./gradlew assembleDebug
```
The debug APK will be generated at:
`app/build/outputs/apk/debug/app-debug.apk`

#### 3. Assemble Release APK / AAB
To build an optimized release bundle signed with your keystore:
```bash
# Generate Release AAB (for Google Play Console)
./gradlew :app:bundleRelease

# Or Generate Release APK (for Direct Sideloading)
./gradlew :app:assembleRelease
```

The output artifacts will be located at:
* **AAB**: `app/build/outputs/bundle/release/app-release.aab`
* **APK**: `app/build/outputs/apk/release/app-release.apk`

### ProGuard & Shrinking
Release builds have `isMinifyEnabled = true` and `isShrinkResources = true` enabled with customized rules in `proguard-rules.pro` to preserve OpenCV JNI bindings, LiteRT runtimes, and ML Kit interfaces while stripping unused symbols and debug logs.

---

## 📄 License

```ApnaScan – User License & Terms
Copyright (c) 2026 ApnaScan. All Rights Reserved.
By using ApnaScan, you agree to these terms:

1. Free Use & Future Pricing: ApnaScan is currently free. The Author reserves the right to add paid features in future.

2. Ownership: All source code and IP remains with the Author.

3. Restrictions: No copying, modification, reverse engineering, distribution, or derivative works allowed.

4. Disclaimer: Provided "AS IS" without warranty. Author not liable for damages.

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

*Third-Party Libraries: OpenCV, TensorFlow/LiteRT, Google ML Kit, AndroidX, and Coil are licensed under their respective permissive open-source licenses.*

<div align="center">📄 ApnaScan

Your Documents. Your Privacy. Your Control.

Scan • Enhance • Annotate • Export

"🚀 Open Live Preview" https://apnascan.ai.studio

</div>
