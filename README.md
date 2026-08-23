# Dasify Lite Gateway v0.2

A deliberately small Android SMS gateway targeting Android 6 (API 23+) and designed for low-RAM devices.

## What changed in v0.2
- Adds a persistent outgoing SMS queue.
- Processes one outgoing SMS at a time.
- Uses Android `SmsManager`.
- Captures per-message send result through a BroadcastReceiver.
- Failed/no-result sends remain queued and are retried.
- Keeps the task-fetch and incoming-upload loops independent.
- Keeps seconds-based intervals.
- Adds a retry-base setting.
- Adds a GitHub Actions workflow that builds a debug APK in the cloud.

## SMSSync-compatible task flow
The gateway fetches `?task=send`, expects `payload.task=send` with `messages[]`, and reads `uuid`, `to`, and `message`.

Incoming SMS upload sends the conventional fields:
`from`, `message`, `message_id`, `sent_to`, `secret`, `device_id`, `sent_timestamp`.

The outgoing queue is persistent, so multiple messages are stored before processing. A malformed item is skipped instead of terminating the whole batch.

## Build without Android Studio
1. Create a GitHub repository.
2. Upload the contents of this directory.
3. Commit to `main` or `master`.
4. Open **Actions**.
5. Select **Build Dasify Lite Gateway APK**.
6. Click **Run workflow** (or push a commit).
7. Download the artifact `DasifyLiteGateway-debug-apk`.
8. The APK inside is `app-debug.apk`.

No Android Studio is required.

## Important
This is a buildable engineering prototype, not a claim of successful real-device modem testing. Android manufacturer firmware, SIM behavior, SMS role/default-app restrictions, and the exact server response format still need testing on the intended Android 6 handset.
