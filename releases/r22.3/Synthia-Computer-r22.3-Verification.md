# Synthia Computer r22.3 — verification and use

## Completed build

This separate v0.5.1/versionCode 6 build repairs the mobile interface while preserving the useful computer, real readers, x86 emulator, experimental runtime, phone hands, queues, persistent to-dos, and clean interface for your future language model.

### Interface repair

- The fake status bar, lock screen, emoji-heavy launcher, floating orb, and overlapping Suite Center control were removed from the home interface.
- The home screen now provides a readable local command center with direct actions for Computer, Emulator, To-do, Browser, Acode, and Universe.
- Assistant, To-do, and Apps remain available in the bottom navigation. Suite Center remains reachable from the app drawer.
- The app drawer is a searchable list with all nine existing applications preserved.
- Zoom is no longer disabled. The interface supports safe areas, visible keyboard focus, reduced motion, offline bundled fonts, and phone/tablet/desktop layouts.
- Inter Tight and JetBrains Mono are bundled locally with their SIL Open Font License notices; no network font fetch is required.

## Existing useful functions

- **Wake word:** say “Hey Synthia” after enabling **Wake word**. Listening uses Android speech recognition or the browser equivalent, requests microphone permission, and stops when the Android app pauses. It is not a hidden background microphone service. Offline recognition depends on the installed recognizer and is not assumed.
- **Local commands:** manage to-dos, calculate arithmetic, open apps and URLs, report capabilities, summarize imported documents, run bounded study jobs, and retrieve supporting passages.
- **Persistent library:** import PDF, EPUB, UTF-8 text, Markdown, JSON, CSV, and source-code files. Documents and generated study reports persist in IndexedDB on the device. Source files are limited to 50 MB and extracted document text to 20 MB.
- **Real PDF reading:** bundled PDF.js extracts every text page with page markers and progress. Image-only/scanned PDFs are rejected clearly rather than presented as successfully read; OCR is not included.
- **Real EPUB reading:** bundled EPUB.js and JSZip read spine sections and preserve block/sentence boundaries for search, summaries, and grounded answers.
- **Bounded autonomy:** `study DOCUMENT TITLE` loads the document, creates an extractive report, saves a separate library document, and stops. It does not pretend to perform open-ended research.
- **Code computer:** edit and run JavaScript in a fresh Worker with a ten-second limit. Load/save text in the app-private Android workspace.
- **Real emulator:** open **Emulator** to boot the bundled 32-bit x86 Linux ISO through v86/WebAssembly. It has VGA output, pause/resume/restart, and a serial console that accepts real guest commands. Networking and host file sharing are disabled; an optional host9p mount can report unavailable.
- **Linux bridge:** reviewed commands can be dispatched to Termux. The bridge returns `complete:false` because it cannot capture stdout, stderr, or an exit code.
- **Optional Trident:** configure the real Hugging Face Space URL and a Gradio API name accepting one text input. The token is session-only. Returned text is never executed automatically.

## Trident setup

Open **Computer → Optional Trident on Hugging Face** and enter:

1. The exact Space URL, such as `https://huggingface.co/spaces/OWNER/SPACE`.
2. The named Gradio API, commonly `predict`, but only if Trident actually exposes that name.
3. An optional Hugging Face token.

Saving the connection does not claim it works. Send a prompt to test the actual API schema. The live Trident agent was not identified from its name alone, so only the client protocol was tested here, using a controlled mock exchange.

## Useful voice examples

- `Hey Synthia, add task test the new build`
- `Hey Synthia, list tasks`
- `Hey Synthia, calculate 12 * (8 + 2)`
- `Hey Synthia, open computer`
- `Hey Synthia, study Manual`
- `Hey Synthia, find cache expiration in Manual`

Unknown requests go to Trident when configured, otherwise to the preserved experimental runtime.

## Verification

- Root tests: **24 passed, 0 failed**.
- Additional current runtime checks: **52 passed, 0 failed**. The historical legacy-resolver check and retired R20 shell check were run separately from this current-runtime set and are described below.
- Chromium interface acceptance: all six primary tools opened and closed, all nine drawer apps rendered, app search worked, Assistant worked, and 375/768/1440-pixel layouts had no horizontal overflow, unexpected missing resources, or page script errors.
- Settled home, Computer, Apps, Assistant, and 375-pixel phone screens were visually inspected after the final typography and file-picker changes.
- Chromium interaction: commands, persistent import, grounded Q&A, autonomous study report, Worker execution, Trident protocol, and wake-word state reporting passed with **zero page script errors**.
- Reader acceptance: real PDF and EPUB files were extracted, indexed, summarized, and used for grounded answers.
- Emulator acceptance: the actual x86 guest reached its shell prompt and ran `echo SYNTHIA_X86_OK && uname -s`; observed output included `SYNTHIA_X86_OK` and `Linux`, with zero page script errors.
- WebView boot graph: **168 statically reachable modules**, with no Node-only static imports.
- Android: Java compilation, DEX generation, APK ZIP integrity, alignment, and APK Signature Scheme **v2/v3 verification passed**. V4 was not claimed.
- APK asset identity: **2,475 source assets checked; 0 missing, 0 changed, and no generated `.synthia` state packaged**. Plain and gzip root filesystem siblings, firmware, WebAssembly, and the Linux ISO are present under their exact names.
- APK size: **100,396,429 bytes**.
- APK SHA-256: `b59c54d7b4337c2620d5a950cfe2f136f446a5127a663b84267b0b4817045430`.
- Signing certificate SHA-256: `8911ab63b736628168deb3a083078c09ff1fd50804eda4a808ad040cae2c9fae`, matching r22.2.

## Installation note

This is a separately debug-signed build. It retains r22.2's signing identity and advances versionCode to 6, so it is intended to upgrade r22.2 without changing certificates. Its certificate differs from R22.1, so Android may refuse an in-place upgrade from R22.1 and require that version to be removed first. Removing an app erases its app-local data; export anything needed before doing that. Physical installation was not tested here.

## Honest boundaries

- No live Trident request was made because the exact Space and API contract were not available.
- Extractive summaries and passage retrieval are useful deterministic tools, not claims of general language comprehension or a bundled language model.
- Physical-device installation, microphone behavior, Accessibility, Termux, lifecycle, and phone-control tests still need to be performed on your phone.
- Scanned PDFs need OCR, which is not included. Emulator networking and host file sharing are disabled.
- `real-world-version-lineage-smoke.mjs` still requires the genuine historical legacy-resolver files, which have not been recovered. No replacement history was fabricated.
- The old `r20-browser-live-ui-smoke.mjs` targets the retired R20 shell and cache contract rather than the current R22 architecture. Current WebView, self-install, public-shell, and interaction checks were run separately.
- R21.21/R21.22 historical Drive archive inspection remains a separate recovery task.
- The original repaired R22, R22.1, and r22.2 APKs, source archives, and reports remain untouched.

## Source archive integrity

- Source ZIP CRC/integrity test: **passed**.
- Generated `.synthia` runtime state: **excluded**.
- Source archive size: **100,294,085 bytes**.
- Source archive SHA-256: `167ff06ea64b5638832ca9a32888871b352b04efe81812323801e343c9a0ec83`.
