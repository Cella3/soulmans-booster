# Soulmans Sound Booster — Music Player 5.0

A personal, ad-free Android audio and video player with Soulmans artwork, optional boost, a seven-band equalizer, four sample pads, and music-reactive visuals. Android 8.0 or newer. No account, ads, analytics, internet, or microphone permission.

## Listening

- **Files / Folder:** choose audio or video files, multiple files, or a folder and its subfolders using Android Files. Access is remembered. Android restricts some system folders; choose a media subfolder instead.
- **Library:** tap a track to play. Hold it for Play next, Add to queue, Add to playlist, or Remove from library. Removing a track never deletes its original audio file.
- **Lists:** save the current queue, create or rename playlists, add or remove tracks, and delete playlists. The library, lists, play counts, and history stay on this phone.
- **Queue:** hold a track to move it up/down or remove it. Shuffle and repeat-one/repeat-all are available on Now Playing.
- **History:** the latest 200 playback starts, timestamps, and lifetime play counts. Pausing and resuming a loaded track does not add another play. History can be cleared from the library menu.
- Queue and playback position are remembered. Reopening restores the queue paused. Position is saved every five seconds and on playback changes.
- Playback continues with the screen off and has notification, lock-screen, and Bluetooth media controls.

## Player and samples

- Drag the progress bar to seek. Video plays in the artwork window, with a fullscreen video option. Embedded album artwork appears when a song provides it; otherwise the speaker-blast portrait appears.
- PCM WAV tracks and samples also show peak-volume waveforms. On a track, tap or drag the waveform to seek. In the pad editor, the waveform shows the selected trim region and its start/end markers.
- **Four sample pads:** tap an empty pad to choose an audio file. Tap a loaded pad to play it; one-shot, toggle, and gate triggers are available. All four can overlap with a song or play on their own. Hold a pad to edit it. Stop All stops every pad. Sample volume is adjustable in Sound.
- **MPC sample editor:** trim a sample's start and end with sliders, enable looping with a checkbox, and see volume peaks with IN/OUT markers for PCM WAV. Adjust pitch, fade-in, fade-out, echo mix, and echo delay per pad. Preview the edited slice or export it as a separate 16-bit PCM WAV (up to 60 seconds); the source file stays unchanged.
- **Pitch:** choose -12 to +12 semitones in half-step increments. Pitch is saved per track while tempo stays the same.
- **Visuals:** neon spectrum, electric waveform, orbital pulse, or artwork glow. The visualizer reads the decoded music signal without recording the microphone. A small overlay appears after four seconds without touch. Tap Visuals for fullscreen; optionally enter fullscreen after 15 seconds. Tap anywhere to leave.

## Boost and EQ

- Player boost is optional, 0–12 dB, applied to the player's audio with a soft limiter to reduce hard clipping. The speakers and already-loud recordings still impose physical limits.
- Seven software EQ bands: 60, 150, 400, 1k, 2.5k, 6k, and 12k Hz, each ±6 dB. Presets: Flat, Bass, Vocal, Bright, Rock, Electronic, and Acoustic, plus Custom. Boost and EQ each have a separate switch and are initially off.
- **Other apps boost** retains the original experimental global audio effect. It pauses this player; starting player playback switches global boost off to avoid stacked processing. Support depends on the phone and output route. It does not boost phone calls.

## Formats and file access

Common Android-supported audio formats include MP3, AAC/M4A, FLAC, WAV, Ogg/Vorbis, Opus, and AMR. Common video containers include MP4, WebM, MKV, MOV, and 3GP when the device has a compatible codec. Android codecs vary by device, so no player can guarantee every codec, damaged file, or DRM-protected file. Unsupported or inaccessible files show an error. The waveform view reads uncompressed PCM WAV; compressed WAV variants can still play if Android can decode them, but may not get the peak view. MIDI, WMA, AIFF, and unusual encodings depend on the device and may be rejected.

The app remembers document permissions, not copies of music files. If a file moves, a storage card is removed, or a provider revokes access, re-import it. Saved folders can be rescanned from the Library menu. Cloud document providers may use their own network connection; this app itself is offline.

## Build

Java 17, Gradle 8.13, Android Gradle Plugin 8.13.2, SDK 35, min SDK 26, target SDK 34, Media3 1.8.0.

```text
gradlew.bat assembleDebug
gradlew.bat testDebugUnitTest lintDebug
gradlew.bat connectedDebugAndroidTest
gradlew.bat assembleRelease
```

Set `ANDROID_HOME` to an Android SDK or use an Android Studio `local.properties`. The application ID remains `com.cleargain.app`, version code is 5, and the delivered APK uses the existing signing certificate so it can update earlier versions. The private signing key is excluded from the public source ZIP. A new source checkout uses a new debug key unless the owner's existing key is supplied as `app/debug.keystore`; an APK signed with another key cannot replace an existing install.

Media3 ExoPlayer and MediaSessionService provide decoding and background media controls. Storage Access Framework handles file and folder selection. SQLite stores tracks, playlists, and history. A custom PCM processor supplies the EQ, gain, limiter, and frequency analysis.

Official references: [Media3](https://developer.android.com/jetpack/androidx/releases/media3), [background playback](https://developer.android.com/media/media3/session/background-playback), [supported formats](https://developer.android.com/media/media3/exoplayer/supported-formats).
