# SnapTap

> A mobile-first, cross-platform video streaming application optimized for vertical, one-handed use and bite-sized, segmented viewing experiences. Built with **Kotlin Multiplatform (KMP)** and **Compose Multiplatform (CMP)**.

---

## 📱 About SnapTap

**SnapTap** is designed for modern mobile users who consume video content in fragments—whether during a quick commute, waiting in line, or taking a short break. By focusing on vertical ergonomics, instant-start playback, and smart progress memory, SnapTap bridges the gap between long-form depth and short-form speed.

---

## ✨ Key Features

* **Thumb-Zone Optimized UI**: Navigation bars and interactive hotzones are anchored within natural thumb reach for effortless one-handed vertical operation.
* **Smart Segmented Progress (Resume Anytime)**: Automatically tracks exact watch timestamps across sessions. Re-opening the app surfaces a "Continue Watching" card for seamless drop-in viewing.
* **Hybrid Feed Experience**: Blends a vertical short-video feed (Reels-style scrolling) with short-burst insights for longer videos.
* **Zero-Lag Instant Startup**: Lightweight caching mechanisms ensure videos play the moment they are tapped, minimizing buffering overhead on mobile networks.

---

## 🛠️ Tech Stack

* **UI Framework**: JetBrains Compose Multiplatform (CMP) for shared, native-speed UI across Android and iOS.
* **Architecture**: Clean Architecture with Kotlin Multiplatform (Shared Business Logic & Domain).
* **Networking**: Ktor Client for asynchronous API communication.
* **Local Caching**: SQLDelight / Okio for offline watch-history and progress persistence.
* **Dependency Injection**: Koin.

---

## 📂 Project Structure

```text
SnapTap/
├── shared/                       # Cross-platform core (Kotlin)
│   ├── commonMain/               # Shared domain, data layers, and CMP UI
│   ├── androidMain/              # Android-specific implementations
│   └── iosMain/                  # iOS-specific implementations (Swift interop)
├── androidApp/                   # Android native app launcher
└── iosApp/                       # iOS Xcode native app wrapper

```

---

## 🚀 Getting Started

### Prerequisites

* **Android Studio** (Koala or newer) with Kotlin Multiplatform Plugin enabled.
* **Xcode** (latest version for iOS compilation).
* **JDK 17+**.

### Running the Project

1. Clone the repository:
```bash
git clone https://github.com/your-username/SnapTap.git

```


2. Open the project folder in Android Studio.
3. Run the **`androidApp`** configuration to launch on an Android emulator or device.
4. To run on iOS, open `iosApp/iosApp.xcodeproj` in Xcode or use the CMP Gradle task for iOS deployment.

---

## 💡 Code Snippet: Segmented Watch Card

Here is an example of the progress-tracking component used in `commonMain` to support fragmented viewing habits:

```kotlin
@Composable
fun SegmentedWatchCard(
    title: String,
    channelName: String,
    progressPercent: Float, // 0.0 to 1.0 tracking progress
    timeLeft: String,      
    modifier: Modifier = Modifier
) {
    Column(
        modifier = modifier
            .fillMaxWidth()
            .clip(RoundedCornerShape(12.dp))
            .background(Color(0xFF1E1E1E))
            .padding(12.dp)
    ) {
        Text(text = title, color = Color.White, fontSize = 15.sp, maxLines = 1)
        Spacer(modifier = Modifier.height(4.dp))
        Text(text = "$channelName • $timeLeft", color = Color.Gray, fontSize = 12.sp)
        
        Spacer(modifier = Modifier.height(10.dp))

        LinearProgressIndicator(
            progress = { progressPercent },
            modifier = Modifier
                .fillMaxWidth()
                .height(4.dp)
                .clip(RoundedCornerShape(2.dp)),
            color = Color.Red,
            trackColor = Color.DarkGray,
        )
    }
}

```

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.
