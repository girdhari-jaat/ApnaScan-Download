<div align="center">
  <img width="100%" alt="ApnaScan Banner" src="./public/ApnaScan_Play_Store_Feature_Graphic_1024x500.png" />ApnaScan: High-Performance Offline Document Scanner

A fast, secure, and privacy-first Android document scanner built with native Kotlin, Jetpack Compose, CameraX, Google AI Edge LiteRT, OpenCV, and ML Kit.

""Platform" (https://img.shields.io/badge/Platform-Android%208.0%2B%20(API%2026--37)-3DDC84?logo=android&logoColor=white)" (#build-configuration)
""Language" (https://img.shields.io/badge/Language-Kotlin%202.x-7F52FF?logo=kotlin&logoColor=white)" (#architecture)
""UI Framework" (https://img.shields.io/badge/UI-Jetpack%20Compose%20%2F%20Material%203-4285F4?logo=jetpackcompose&logoColor=white)" (#architecture)
""Privacy" (https://img.shields.io/badge/Privacy-Local%20First-green?logo=shield&logoColor=white)" (#privacy--offline-first-experience)
""Compatibility" (https://img.shields.io/badge/Memory-16KB%20Page%20Size-orange?logo=linux&logoColor=white)" (#high-performance-processing)
""License" (https://img.shields.io/badge/License-Proprietary-red)" (#license)

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
</div>---

📖 Overview

ApnaScan is a modern Android document scanning application designed for users who need fast, reliable, and high-quality document digitization without compromising their privacy.

Built with native Android technologies, ApnaScan combines intelligent camera capture, advanced image processing, non-destructive editing, QR and barcode recognition, and flexible PDF generation in one lightweight application.

Unlike cloud-dependent scanning solutions, ApnaScan performs its core scanning, image processing, editing, and document management operations directly on the device.

With no application-level Internet permission, documents remain stored locally within the application's private storage. Your scans stay under your control rather than being routinely uploaded to remote servers.

---

🌟 Key Features

📷 1. Intelligent Hardware Capture

- Native CameraX Engine: Direct integration with Android CameraX ("camera-camera2", "camera-lifecycle") for camera preview, autofocus, pinch-to-zoom, torch controls, and device-supported capture resolutions.
- Dynamic Resolution Selection:
  - HD (Fast): Optimized for responsive capture and quick multi-page scanning.
  - FHD (Standard): Balanced resolution for everyday document scanning.
  - UHD (High): High-resolution capture for fine text, detailed documents, and professional scanning needs, subject to device camera capabilities.
- Multiple Capture Modes:
  - DOCS Mode: Document-focused capture with aspect-ratio guidance and edge alignment.
  - ID Card Mode: Dedicated front-and-back identity card scanning with single-sided and dual-sided workflows and on-screen alignment guides.
- ML Kit Document Scanner: Integration with Google ML Kit Document Scanner for automated document detection, edge recognition, cropping, and scanning workflows through Google Play services.
- Batch Scanning: Capture and manage multi-page documents in a single scanning session, supporting up to 50 pages.

🎨 2. Advanced Non-Destructive Editing Studio

- Magnetic Edge Cropping: Four-point manual corner adjustment with magnified loupe preview and automatic boundary snapping.
- Non-Destructive Rotation: 90-degree rotation adjustments while preserving the original captured image.
- Professional Image Filters:
  - Original: Preserves the original captured appearance.
  - Magic Color: Enhances contrast and color intensity while maintaining document details.
  - Paper / Clean White: Reduces page shadows and unwanted color casts for cleaner-looking documents.
  - Card / ID: Optimized image enhancement for identity cards, photographs, and detailed printed patterns.
  - B&W (Binarization): Otsu threshold-based monochrome processing for crisp, printer-friendly text.
  - Grayscale: Smooth 8-bit grayscale conversion.
- Fine-Tuning Controls: Independent adjustment sliders for Contrast, Brightness, Saturation, and Sharpness.

🔍 3. QR & Barcode Recognition

- On-Device Recognition: Integrated Google ML Kit Barcode Scanning for lightweight QR code and barcode recognition.
- Instant Extraction: Detect and extract supported barcode and QR code content from scanned documents or supported camera workflows.
- Quick Actions: Copy extracted content, share results, or open detected URLs.

📁 4. Document Management

- Organize scanned pages into multi-page documents.
- View document pages in a convenient grid layout.
- Reorder pages before exporting.
- Continue editing previously scanned documents.
- Manage document sessions with locally stored editing information.
- Export completed documents as PDF files.

---

⚡ High-Performance Processing

ApnaScan uses an optimized on-device image-processing architecture designed to maintain responsive previews, efficient memory usage, and smooth document editing.

Image Processing Pipeline

+-----------------------------------------------------------------------------------+
|                     OPTIMIZED ON-DEVICE IMAGE PIPELINE                            |
+-----------------------------------------------------------------------------------+
  [ Camera Capture / File Input ]
              |
              v
  [ Private Internal Storage ]  <--- (Original Captured Image Preserved)
              |
              v
  [ Coroutine Dispatcher.IO ]  <--- (Background Image Processing)
              |
              v
  [ Non-Destructive Editing ]  <--- (Corners, Rotation, Filters & Adjustments)
              |
              v
  [ Display Render Cache ]    <--- (Cached Previews & Responsive UI)
              |
              v
  [ PDF Export Engine ]       <--- (Image Processing & PDF Assembly)
              |
              v
  [ Final PDF Document ]
+-----------------------------------------------------------------------------------+

Architectural Highlights

- Non-Destructive Editing Architecture: Original captured images are preserved in private application storage. Cropping, rotation, filters, image adjustments, and annotations are maintained separately as editing metadata. This allows users to modify or revert their edits without repeatedly degrading the original image.

- Dual-Layer Caching Engine:
  
  - Display Render Cache: Processed previews and thumbnails are cached locally to reduce repeated image-processing operations and improve document loading responsiveness.
  - PDF Hash Cache ("currentHash"): Document state is fingerprinted to identify previously exported versions. Unchanged documents can reuse cached PDF output instead of repeating the entire export process.

- 16KB Page-Size Compatibility: The application targets compatibility with Android devices using 16KB memory pages. Native libraries, including OpenCV and other packaged dependencies, must meet the required ELF alignment and packaging requirements.

- Efficient Offscreen Rendering: Image composition, watermarking, and annotation rendering use native Android Canvas operations and bitmap processing with controlled memory management.

- Background Processing: Kotlin Coroutines and dedicated dispatchers keep computationally intensive image transformations and PDF generation away from the main UI thread.

---

📄 Flexible PDF Export

ApnaScan provides configurable PDF generation options for personal documents, identity cards, professional paperwork, and printing workflows.

Configuration| Available Options| Description
Page Sizes| "Original", "Auto", "A4", "Letter", "Legal"| Preserve original image geometry or fit content to standard paper dimensions.
Orientation| "Portrait", "Landscape", "Auto"| Choose page orientation manually or determine it automatically from content dimensions.
Resolution (DPI)| "72", "150", "300 DPI"| Select draft, standard, or print-oriented output resolution.
JPEG Quality| "40%" to "95%"| Control image compression and balance PDF size against visual quality.
Card Layouts| "Grid" (2-up), "Stack" (Side-by-side)| Arrange front and back ID card images on a single PDF page.
Security| RC4 Password Protection| Apply PDF 1.4-compatible password protection using the implemented RC4 encryption mechanism.
Custom Watermark| Custom text / Unicode| Add a diagonally positioned watermark with approximately 18% opacity.
Page Numbering| "1 / N" Footer| Display page numbers with adaptive positioning. Original-size pages can receive an additional bottom strip to avoid covering document content.
Export Actions| Share, Save, Print| Use the Android share sheet, MediaStore document storage, or Android PrintManager.

PDF Export Capabilities

- Multi-page PDF generation.
- Configurable page dimensions and orientation.
- Adjustable image compression.
- Custom watermark support.
- Automatic page numbering.
- ID card front-and-back layouts.
- Password-protected PDF output.
- Direct sharing, saving, and printing.

---

✍️ Annotation Studio

ApnaScan includes an integrated document annotation and digital signature studio for marking up scanned documents without modifying the original captured image.

Annotation Tools

- Pen & Signature: Freehand vector drawing with simulated pressure-sensitive stroke-width control. Includes a quick-access signature drawer for signing forms, receipts, and documents.
- Highlighter & Marker: Translucent highlighting with adjustable stroke widths from 2dp to 50dp and smooth alpha blending.
- Smart Eraser: Removes annotation strokes and vector paths without erasing the underlying document image.
- Text Annotation: Insert custom text, labels, dates, and notes with adjustable typography, size, and color.
- Color Palette & Eyedropper: Eight curated annotation colors with an interactive eyedropper for selecting colors directly from the document canvas.
- Undo / Redo History: Stroke-by-stroke editing history with one-tap undo, redo, and canvas clearing.

Annotation Features

- Vector-based annotation storage.
- Customizable drawing tools.
- Adjustable brush widths and colors.
- Reusable digital signatures.
- Independent annotation editing.
- Non-destructive annotation rendering.

---

🏗️ Architecture

ApnaScan follows Modern Android Development (MAD) principles, combining Clean Architecture, Unidirectional Data Flow (UDF), and a modular separation of application responsibilities.

Project Structure

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
│   ├── CropScreen.kt               # Four-point perspective correction
│   ├── DocumentGrid.kt             # Multi-page overview, reordering, batch export
│   └── theme/                      # Material 3 Color Schemes, Typography, Shapes
└── util/                           # Utilities & Native Bridges
    ├── PdfExporter.kt              # Native PDF stream generation
    ├── OpenCVHelper.kt             # Native edge detection & perspective transformation
    └── DiagnosticsLogger.kt        # Lightweight diagnostics logging

Core Technologies

- Kotlin: Primary programming language for native Android development.
- Jetpack Compose & Material 3: Declarative UI development with responsive layouts, animations, edge-to-edge design, and Day/Night dynamic color theming.
- CameraX: Native Android camera integration for capture, preview, and device-supported camera controls.
- Dagger Hilt ("2.60.1"): Dependency injection across application components, ViewModels, and use cases.
- Kotlin Coroutines & Flow: Structured concurrency and asynchronous processing for responsive application performance.
- OpenCV ("4.11.0"): Computer vision operations, document contour detection, image processing, and perspective transformation. Packaged native ABIs depend on the configured build.
- Google AI Edge LiteRT ("2.3.0"): On-device machine learning runtime.
- Google ML Kit: Document scanning and barcode recognition capabilities.
- Coil 3 ("3.6.3"): Asynchronous image loading and memory-aware image rendering in Compose.

---

🔒 Privacy & Offline-First Experience

Privacy is a core design principle of ApnaScan. The application is designed to keep scanned documents and core processing operations on the user's device.

Privacy Features

- No Application-Level Internet Permission: ApnaScan does not request "android.permission.INTERNET" in its application manifest. Its own application code therefore cannot perform ordinary internet network requests.

- No First-Party Analytics or Telemetry: No Google Analytics, Firebase Crashlytics, Facebook SDK, or application-level tracking services are intentionally integrated.

- Private Local Storage: Scanned documents and related editing data are stored in the application's private internal storage ("Context.filesDir"), protected by Android's application sandbox.

- Local Image Processing: Document cropping, filters, adjustments, annotations, and PDF generation are designed to run locally on the device.

- Camera Access Control: Camera access is used during active scanning workflows and released when the camera session is no longer required.

Offline Operation

ApnaScan's core scanning and document-processing workflows are designed to work locally without requiring an application-level internet connection.

Note: Certain Google ML Kit features, particularly the Google Play services-powered Document Scanner, may require Google Play services and initial resource availability or downloads. This is separate from ApnaScan's own application-level network access.

---

🌍 Localization Support

ApnaScan supports multiple languages with native Right-to-Left (RTL) layout handling for supported locales.

Language| Locale Code| Direction| Native Name
English| "en"| LTR| English
Urdu| "ur"| RTL| اردو
Sindhi| "sd"| RTL| سنڌي
Hindi| "hi"| LTR| हिन्दी

Localization Features

- Supported locales declared in "res/xml/locales_config.xml".
- Android 13+ per-app language preferences.
- Localized interface elements, dialogs, buttons, hints, and alerts.
- RTL-aware layout direction for supported languages.
- Native text rendering and layout adaptation.

---

🛠️ Build Configuration

Prerequisites

- Android Studio: Ladybug / Meerkat or newer.
- JDK: Java 17 (OpenJDK or Azul Zulu recommended).
- Android SDK: Compile SDK "37", Target SDK "37", Minimum SDK "26" (Android 8.0 Oreo).
- Android NDK: Version "25.x+" as configured by the project.
- Gradle: Use the version specified in the Gradle wrapper.
- ABI: Default native ABI configuration: "arm64-v8a".

Build Steps

1. Clone the Repository

git clone https://github.com/your-username/ApnaScan.git
cd ApnaScan/android

2. Assemble Debug APK

./gradlew assembleDebug

The generated debug APK will be available at:

app/build/outputs/apk/debug/app-debug.apk

3. Assemble Release APK / AAB

Generate an Android App Bundle for Google Play:

./gradlew :app:bundleRelease

Or generate a release APK for direct installation:

./gradlew :app:assembleRelease

Expected output locations:

- AAB: "app/build/outputs/bundle/release/app-release.aab"
- APK: "app/build/outputs/apk/release/app-release.apk"

ProGuard & Resource Shrinking

Release builds use code shrinking and resource optimization through the configured Gradle release settings.

The project includes custom ProGuard/R8 rules in "proguard-rules.pro" to preserve required OpenCV JNI bindings, LiteRT runtime components, and ML Kit interfaces where necessary.

Unused code and resources can be removed to help reduce the final application package size.

Native Library Compatibility

For Android devices using 16KB memory pages, verify all packaged native shared libraries and their ELF alignment.

Native dependencies, including OpenCV and LiteRT, must be compatible with the target memory page size.

Release APK and AAB artifacts should be tested using Android's official 16KB compatibility verification tools before distribution.

---

📄 License

ApnaScan is proprietary software.

Copyright (c) 2026 ApnaScan. All Rights Reserved.

The application and its original source code, design, branding, and associated intellectual property are owned by the author.

Terms of Use

1. Free Use: ApnaScan is currently available free of charge. The author reserves the right to introduce paid features, subscriptions, or other pricing models in future versions.

2. Ownership: All rights, title, and interest in ApnaScan and its original intellectual property remain with the author.

3. Restrictions: Unauthorized copying, modification, redistribution, reverse engineering, or creation of derivative works is prohibited, except where expressly permitted by applicable law.

4. Disclaimer: The software is provided "AS IS", without warranties of any kind, express or implied. The author shall not be liable for damages arising from its use to the extent permitted by applicable law.

Third-Party Licenses

ApnaScan incorporates third-party libraries and technologies, including OpenCV, Google AI Edge LiteRT, Google ML Kit, AndroidX, and Coil.

These components remain subject to their respective licenses and copyright notices. Their licenses are separate from the proprietary license governing ApnaScan's original application code.

For applicable third-party license information, refer to the respective upstream projects and included license notices.

---

<div align="center">ApnaScan — Scan Smart. Stay Private.

Fast • Secure • Offline-First • Lightweight • Ad-Free

</div>