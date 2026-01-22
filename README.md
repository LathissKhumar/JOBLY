# JOBLY

Jobly is a full-stack application built with Flutter and Serverpod.

## Get Started

Follow these instructions to set up your development environment and run the project on your machine.

### 1. Prerequisites

Before you begin, ensure you have the following installed:

#### A. Install Flutter SDK

**Windows:**
1.  **Download SDK:** Go to the [Flutter install page for Windows](https://docs.flutter.dev/get-started/install/windows) and download the latest stable release zip.
2.  **Extract:** Extract the zip file to a location (e.g., `C:\src\flutter`). Do not install it in `C:\Program Files`.
3.  **Update Path:**
    *   Search for "env" in the Start menu and select **Edit the system environment variables**.
    *   Click **Environment Variables**.
    *   Under **User variables**, select **Path** and click **Edit**.
    *   Click **New** and add the path to `flutter\bin`.
4.  **Verify:** Open PowerShell and run `flutter doctor`.

**Linux (Ubuntu/Debian):**
1.  **Install Dependencies:**
    ```bash
    sudo apt-get update -y && sudo apt-get install -y curl git unzip xz-utils zip libglu1-mesa
    ```
2.  **Download SDK:** Go to the [Flutter install page for Linux](https://docs.flutter.dev/get-started/install/linux) and download the tarball.
3.  **Extract:**
    ```bash
    tar xf ~/Downloads/flutter_linux_subsystem_*.tar.xz
    ```
4.  **Update Path:** Add the following to your `~/.bashrc` or `~/.zshrc`:
    ```bash
    export PATH="$PATH:`pwd`/flutter/bin"
    ```
5.  **Verify:** Run `flutter doctor`.

**Arch Linux:**
1.  **Install Dependencies:**
    ```bash
    sudo pacman -S git base-devel
    ```
2.  **Install Flutter:**
    You can install via AUR (Arch User Repository) for easier management.
    ```bash
    git clone https://aur.archlinux.org/flutter-git.git
    cd flutter-git
    makepkg -si
    ```
    *Alternatively, download the tarball manually as per standard Linux instructions.*
3.  **Config:**
    If installed via AUR, it places flutter in `/opt/flutter`.
    Add to path if needed, or follow prompt instructions.
4.  **Verify:** Run `flutter doctor`.

**macOS:**
1.  **Download SDK:** Go to the [Flutter install page for macOS](https://docs.flutter.dev/get-started/install/macos).
2.  **Extract:** Unzip the downloaded file.
3.  **Update Path:** Add the following to your `~/.zshrc` or `~/.bash_profile`:
    ```bash
    export PATH="$PATH:`pwd`/flutter/bin"
    ```
4.  **Verify:** Run `flutter doctor`.

#### B. Install Docker

Serverpod requires Docker to run the database (PostgreSQL) and Redis.

*   **Windows & macOS:** Download and install [Docker Desktop](https://www.docker.com/products/docker-desktop).
*   **Linux (Ubuntu/Debian):** Install Docker Engine following the official guide for your distribution (e.g., [Ubuntu](https://docs.docker.com/engine/install/ubuntu/)).
*   **Arch Linux:**
    1.  Install Docker:
        ```bash
        sudo pacman -S docker
        ```
    2.  Start and enable Docker service:
        ```bash
        sudo systemctl start docker.service
        sudo systemctl enable docker.service
        ```
    3.  Add your user to the docker group (to run without sudo):
        ```bash
        sudo usermod -aG docker $USER
        newgrp docker
        ```

**Important:** Ensure Docker is running before proceeding.

#### C. Install Serverpod CLI

Once Flutter and Docker are set up, install the Serverpod CLI tool globally:

```bash
dart pub global activate serverpod_cli
```

### 2. Setup Android Studio

Android Studio is the recommended IDE for Flutter development (along with VS Code).

1.  **Download & Install:** Download [Android Studio](https://developer.android.com/studio) and follow the installation wizard.
2.  **Install Flutter Plugin:**
    *   Open Android Studio.
    *   Go to **Plugins** in the generic settings or Welcome screen.
    *   Search for **Flutter** and install it (this will also install the Dart plugin).
    *   Restart the IDE.
3.  **Setup Android SDK & Emulator:**
    *   Open **SDK Manager** (More Actions > SDK Manager).
    *   Ensure the latest Android SDK Platform is checked.
    *   Go to **Virtual Device Manager** (More Actions > Virtual Device Manager).
    *   Create a new virtual device:
        *   Select **Pixel 9 Pro** as the hardware profile.
        *   Download a system image (e.g., **API 35** or latest stable).
        *   Finish the setup.

### 3. Project Setup (New Machine)

Follow these steps to set up the project on a fresh machine.

#### Step 1: Clone the Repository

```bash
git clone <repository-url>
cd jobly
```

#### Step 2: Backend Setup

Navigate to the server directory and start the backend.

1.  **Go to the server directory:**
    ```bash
    cd backend/jobly/jobly_server
    ```

2.  **Start Docker Containers:**
    This command starts the PostgreSQL and Redis containers required by Serverpod.
    ```bash
    docker compose up --build --detach
    ```

3.  **Apply Database Migrations:**
    Initialize the database schema.
    ```bash
    dart bin/main.dart --apply-migrations
    ```
    *Note: You might need to run `dart pub get` first if dependencies are missing.*

4.  **Start the Server:**
    ```bash
    dart bin/main.dart
    ```

#### Step 3: Frontend Setup

Open a new terminal window (keep the server running in the previous one).

1.  **Go to the frontend directory:**
    ```bash
    cd frontend
    ```
    *(Note: If the frontend code is located in `backend/jobly/jobly_client` or `backend/jobly/jobly_flutter`, verify the path. Assuming standard structure with a dedicated `frontend` folder at root as seen in file listing).*

2.  **Get Dependencies:**
    ```bash
    flutter pub get
    ```

3.  **Run the App:**
    Select your device (emulator or chrome) and run:
    ```bash
    flutter run
    ```

### Troubleshooting

*   **Serverpod command not found:** Ensure your pub cache is in your PATH.
    *   *Windows:* `C:\Users\<User>\AppData\Local\Pub\Cache\bin`
    *   *Linux/Mac:* `~/.pub-cache/bin`
*   **Docker permission denied:** On Linux, ensure you added your user to the `docker` group.
*   **Ports already in use:** Stop other containers using `docker stop $(docker ps -q)`.