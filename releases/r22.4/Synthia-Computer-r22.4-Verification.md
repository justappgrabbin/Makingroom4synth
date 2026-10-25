# Synthia Computer r22.4 — verification and use

## Completed build

This separate v0.5.2/versionCode 7 release replaces the generic AI-dashboard appearance with a distinctive Synthia field-instrument interface. It preserves the useful computer, real readers, x86 emulator, experimental runtime, phone hands, queues, persistent to-dos, and clean interface for your future language model.

### Interface redesign

- Warm paper, black ink, and signal red replace the dark forest/lime dashboard palette.
- An asymmetric editorial tool index replaces the uniform stacked tool rows.
- A custom Synthia technical schematic and circular voice control provide a specific visual identity.
- The app drawer is now a full-screen red index with large editorial navigation and working search.
- Computer and Assistant use document-style work surfaces rather than generic rounded cards and chat bubbles.
- Fraunces, Inter Tight, and JetBrains Mono are bundled locally with their SIL Open Font License notices; no network font fetch is required.
- Zoom remains enabled. Safe areas, visible keyboard focus, reduced motion, and 44px-class touch targets remain supported.

### Preserved useful functions

- **Wake word:** say “Hey Synthia” after enabling **Wake word**. Listening uses Android speech recognition or the browser equivalent, requests microphone permission, and stops when the Android app pauses. Offline recognition depends on the installed recognizer and is not assumed.
- **Local commands:** manage to-dos, calculate arithmetic, open apps and URLs, report capabilities, summarize imported documents, run bounded study jobs, and retrieve supporting passages.
- **Persistent library:** import PDF, EPUB, UTF-8 text, Markdown, JSON, CSV, and source-code files. Documents and generated study reports persist in IndexedDB on the device.
- **Real PDF and EPUB reading:** bundled PDF.js, EPUB.js, and JSZip extract text locally. Scanned PDFs require OCR, which is not included.
- **Bounded autonomy:** `study DOCUMENT TITLE` creates and saves an extractive report, then stops. It does not pretend to perform open-ended research.
- **Code computer:** edit and run JavaScript in a fresh Worker with a ten-second limit. Load/save text in the app-private Android workspace.
- **Real emulator:** boot the bundled 32-bit x86 Linux ISO through v86/WebAssembly, with VGA output, pause/resume/restart, and a real serial console. Networking and host file sharing are disabled.
- **Linux bridge:** reviewed commands can be dispatched to Termux. The bridge returns `complete:false` because it cannot capture stdout, stderr, or an exit code.
- **Optional Trident:** configure the real Hugging Face Space URL and a Gradio API name accepting one text input. The token is session-only. Returned text is never executed automatically.

## Trident setup

Open **Computer → Optional Trident on Hugging Face** and enter:

1. The exact Space URL, such as `https://huggingface.co/spaces/OWNER/SPACE`.
2. The named Gradio API, commonly `predict`, but only if Trident actually exposes that name.
3. An optional Hugging Face token.

Saving the connection does not claim it works. Only the client protocol was tested here, using a controlled mock exchange. No live Trident integration is claimed.

## Verification

- Root tests: **24 passed, 0 failed**.
- Additional current runtime checks: **52 passed, 0 failed**. The historical legacy-resolver check and retired R20 shell check are described below.
- Chromium interface acceptance: all six primary tools opened and closed, all nine drawer apps rendered, app search worked, Assistant worked, and 375/768/1440-pixel layouts had no horizontal overflow, unexpected missing resources, or page script errors.
- Home, Computer, red Index, Assistant, and phone/tablet/desktop screens were visually inspected after the redesign.
- Chromium interaction: commands, persistent import, grounded Q&A, autonomous study report, Worker execution, Trident protocol, and wake-word state reporting passed with **zero page script errors**.
- Reader acceptance: real PDF and EPUB files were extracted, indexed, summarized, and used for grounded answers.
- Emulator acceptance: the actual x86 guest reached its shell prompt and ran `echo SYNTHIA_X86_OK && uname -s`; observed output included `SYNTHIA_X86_OK` and `Linux`, with zero page script errors.
- WebView boot graph: **168 statically reachable modules**, with no Node-only static imports.
- Android: Java compilation, DEX generation, APK ZIP integrity, alignment, and APK Signature Scheme **v2/v3 verification passed**. V4 was not claimed.
- APK asset identity: **2,477 source assets checked; 0 missing, 0 changed, and no generated `.synthia` state packaged**. Required fonts, firmware, WebAssembly, Linux ISO, and plain/gzip root filesystem siblings are present under their exact names.
- APK size: **100,650,610 bytes**.
- APK SHA-256: `6304469e9f0fab0b55d01ffd6b27e62dae0875772a730c922f85fd1efbc1e9e5`.
- Signing certificate SHA-256: `8911ab63b736628168deb3a083078c09ff1fd50804eda4a808ad040cae2c9fae`, matching r22.2 and r22.3.

## Installation note

This is a separately debug-signed build. It retains the r22.2/r22.3 signing identity and advances versionCode to 7, so it is intended to upgrade either of those versions without changing certificates. Its certificate differs from R22.1, so Android may refuse an in-place upgrade from R22.1 and require that version to be removed first. Removing an app erases its app-local data; export anything needed before doing that. Physical installation was not tested here.

## Honest boundaries

- No live Trident request was made because the exact Space and API contract were not available.
- Extractive summaries and passage retrieval are deterministic tools, not claims of general language comprehension or a bundled language model.
- Physical-device installation, microphone behavior, Accessibility, Termux, lifecycle, and phone-control tests still need to be performed on your phone.
- Scanned PDFs need OCR, which is not included. Emulator networking and host file sharing are disabled.
- `real-world-version-lineage-smoke.mjs` still requires the genuine historical legacy-resolver files, which have not been recovered. No replacement history was fabricated.
- The old `r20-browser-live-ui-smoke.mjs` targets the retired R20 shell and cache contract rather than the current R22 architecture. Current WebView, self-install, public-shell, and interaction checks were run separately.
- R21.21/R21.22 historical Drive archive inspection remains a separate recovery task.
- The original repaired R22, R22.1, r22.2, and r22.3 artifacts remain untouched.

## Source archive integrity

- Source ZIP CRC/integrity test: **passed**.
- Generated `.synthia` runtime state: **excluded**.
- Source archive size: **100,545,749 bytes**.
- Source archive SHA-256: `2a43915b847c7a6143813872694a7dc402ae0afe9bec6cb0af8166797d4a2130`.
