# Memories — Android Photo Management App

**Memories** is an Android application developed in **Kotlin** for taking photos and managing a cloud-backed photo collection. It combines an Android camera workflow with Firebase Storage and Cloud Firestore.

## Features

- **Capture photos** using the device camera
- **Upload images** to Firebase Cloud Storage
- **Display a gallery** of stored images in a three-column grid
- **View photos** at a larger size
- **Edit metadata**, including image name and description
- **Delete photos**, with corresponding removal from cloud storage and Firestore
- **Store image metadata** (name, URL, description, date, and format) in Firestore

## Tech stack

| Layer | Technology |
| --- | --- |
| Mobile | Android, Kotlin, XML layouts |
| UI | AndroidX, Material Components, RecyclerView, fragments |
| Image handling | Device camera, FileProvider, Glide |
| Image storage | Firebase Cloud Storage |
| Metadata | Cloud Firestore |
| Build | Gradle, Android Gradle Plugin 7.3.1, Kotlin 1.7.20 |

## How it works

1. The user captures an image through Android's camera intent.
2. The application stores a temporary image and uploads it to Firebase Storage.
3. After the upload succeeds, the app writes a `pictures` document to Cloud Firestore.
4. The gallery retrieves Firestore metadata and uses Glide to load image URLs.
5. Edit and delete actions update Firestore and the corresponding Storage object.

## Getting started

### Prerequisites

- Android Studio with a compatible Android SDK and JDK
- An Android device or emulator meeting **minimum API level 31** (Android 12)
- A Firebase project with **Cloud Firestore** and **Cloud Storage** configured

### Configure Firebase

1. Register an Android app in the Firebase console with the application ID **`com.patrik_frankovic.memories`** (or adjust the application ID and related configuration together).
2. Download the Firebase Android configuration file.
3. Place it at **`app/google-services.json`** in your local project.
4. Configure **Firestore and Storage security rules** appropriate to your environment before creating or uploading data.
5. Open the project root in Android Studio and sync Gradle.
6. Build and run on a compatible device or emulator. The camera feature needs a camera-capable environment.

> `app/google-services.json` and `local.properties` are deliberately excluded from the repository. The Firebase configuration identifies a specific project; it is not a replacement for correctly configured authentication, access rules, and restrictions.

## Source structure

```text
app/
└── src/main/
    ├── java/.../memories/
    │   ├── MainActivity.kt           # Camera, upload, gallery
    │   ├── DisplayImageFragment.kt   # Photo display and deletion
    │   ├── EditFragment.kt           # Metadata editing
    │   ├── ImageRecyclerAdapter.kt   # Gallery adapter
    │   └── ImageInfo.kt              # Firestore metadata model
    ├── res/layout/                   # Screens and dialogs
    └── AndroidManifest.xml
```

## Limitations and security notes

This is an **academic prototype**, not a production-ready photo-storage service.

- The repository does **not** implement a complete sign-in, per-user authorization, or private-gallery model; configure Firebase rules accordingly and do not use it for sensitive personal photos without adding access controls.
- The project targets **Android API 32** and uses legacy Android APIs/plugins; it may require maintenance for modern tooling and Android versions.
- The camera and cloud-storage workflow has **not been retested** as part of this GitHub cleanup.
- Included unit/instrumented test files are Android Studio templates, not comprehensive automated tests.

## Background

The application was originally developed as part of a larger web and mobile application coursework repository and is now maintained as a separate GitHub portfolio project.
