# Install Windows Subsystem for Linux:

The Windows Subsystem for Linux (WSL) is a compatibility layer designed by Microsoft that enables Windows 10 and Windows 11 to run Linux binary executables (in ELF format) natively on a Windows system, without the need for a traditional virtual machine or dual-boot setup. WSL provides a Linux-compatible kernel interface developed by Microsoft (which can run a GNU/Linux environment directly), allowing users to choose from multiple Linux distributions available in the Microsoft Store.

### Key Features and Benefits of WSL:

- **Run Linux Tools on Windows**: WSL allows users to run Linux command-line tools, utilities, and applications alongside their Windows applications, enabling a seamless cross-platform workflow.
- **Development and Testing**: It's particularly useful for developers who need to build, test, or run applications that are designed to run on Linux. WSL supports most command-line tools, utilities, and applications, making it a robust environment for development and testing.
- **Multiple Linux Distributions**: Users can install multiple Linux distributions from the Microsoft Store, and run them simultaneously, providing flexibility in testing and development across different environments.
- **Integration with Windows File System**: WSL provides integration with the Windows file system, allowing users to access Windows files from within the Linux environment and vice versa.
- **No Overhead of a Traditional VM**: Since WSL is a compatibility layer, it doesn't have the overhead typically associated with a virtual machine, which means it uses fewer system resources and boots faster.

### Setting Up WSL:

Setting up WSL on a Windows 10 or Windows 11 machine typically involves enabling the feature through the Windows Features dialog or using PowerShell commands, and then installing a Linux distribution of choice from the Microsoft Store. Windows 11 has made the process even simpler with improved integration and support for WSL.

Getting started with the Windows Subsystem for Linux (WSL) involves several steps, from enabling the feature in Windows to installing a Linux distribution. Here's a beginner's guide to setting up and using WSL:

### Step 1: Enable WSL

#### On Windows 10:

1. **Open PowerShell as Administrator**: Right-click the Start button, select "Windows PowerShell (Admin)" or "Command Prompt (Admin)".
   
2. **Enable WSL**: Execute the following command:
   ```powershell
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   ```

3. **Enable Virtual Machine Platform** (for WSL 2): Execute:
   ```powershell
   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   ```

4. **Restart your PC**.

#### On Windows 11:

- WSL is integrated more seamlessly and can be installed with a single command. Open PowerShell as Administrator and run:
  ```powershell
  wsl --install
  ```
- This command will install WSL with the default Linux distribution. For more control over the installation, proceed with the manual installation steps.

### Step 2: Update to WSL 2 (Recommended)

WSL 2 offers significant improvements over WSL 1. To set WSL 2 as your default version:

1. **Download and Install the Linux Kernel Update Package**:
   - For Windows 10, download the package from the official Microsoft link.
   - Windows 11 users typically don't need this step as WSL 2 comes by default.

2. **Set WSL 2 as Default**: Open PowerShell as Administrator and run:
   ```powershell
   wsl --set-default-version 2
   ```

### Step 3: Install a Linux Distribution

1. **Open the Microsoft Store**: Search for "Linux" or the specific Linux distribution you want to install (e.g., Ubuntu, Debian, Fedora).

2. **Select and Install a Distribution**: Click "Get" or "Install" on the distribution page.

### Step 4: Initialize Your Linux Distribution

1. **Launch the Installed Distribution**: After installation, open the Start menu, search for the installed Linux distribution (e.g., "Ubuntu"), and open it.

2. **Create a User Account and Password**: The first time you launch your Linux distribution, you'll be prompted to create a new user account and password. This account is separate from your Windows account.

### Step 5: Update and Upgrade Packages

To ensure all packages are up to date, run:
```bash
sudo apt update && sudo apt upgrade
```
This command works for Debian-based distributions like Ubuntu. For others, use the respective package manager commands.

### Step 6: Explore and Install Software

Now that you have a running Linux environment, you can explore and install various Linux software using the package manager, experiment with Linux commands, and even develop and run Linux applications.

### Tips for Using WSL:

- **Accessing Windows Files from Linux**: Your Windows filesystem is mounted under `/mnt/` in WSL. For example, your `C:` drive is at `/mnt/c/`.
  
- **Running Windows Applications from Linux**: You can run Windows executables from within WSL by specifying the full path to the executable or by navigating to `/mnt/c/` and running the executable.

- **Running Linux Applications from Windows**: Use the `wsl` command from PowerShell or Command Prompt, followed by the Linux command you wish to run.

- **Configuring WSL Settings**: WSL settings can be configured in the `.wslconfig` file located in your Windows user directory.

- **Upgrading Distributions**: You can upgrade your WSL 1 distributions to WSL 2 using the `wsl --set-version <DistroName> 2` command.

WSL provides a powerful environment for developing cross-platform applications, running Linux tools on Windows, and learning Linux commands and scripts. Experiment with different commands, install software packages, and explore the Linux environment at your own pace.

# Docker (for Geoserver from https://github.com/geoserver/docker)

Installing Docker Desktop on Windows involves several steps. Here's a guide to help you through the process:

### 1. Check System Requirements
Before installing Docker Desktop, ensure your Windows system meets the following requirements:
- For Windows 10: 
  - Pro, Enterprise, or Education editions with 64-bit processor.
  - Hyper-V and Containers Windows features must be enabled.
- For Windows 11:
  - Any edition with 64-bit processor.
  - WSL 2 (Windows Subsystem for Linux version 2) for Linux container support.

### 2. Enable WSL 2 (Windows Subsystem for Linux version 2)
WSL 2 is required for running Linux containers. To install WSL 2:
1. Open PowerShell as Administrator and run:
   ```powershell
   wsl --install
   ```
2. Restart your computer if required.

### 3. Enable Hyper-V (Windows 10 only)
Hyper-V is required for Windows 10. To enable it:
1. Open Control Panel.
2. Go to "Programs" and then "Turn Windows features on or off".
3. Check "Hyper-V" and click OK.
4. Reboot windows computer

### 4. Download Docker Desktop for Windows
Download the Docker Desktop installer from the [official Docker website](https://www.docker.com/products/docker-desktop).

### 5. Install Docker Desktop
1. Run the installer you downloaded.
2. Follow the on-screen instructions to install Docker Desktop. During installation, you can choose whether to use Windows containers instead of Linux containers (you can switch between them later).
3. After installation, Docker Desktop will start automatically.

### 6. Verify Installation
1. Search for Docker Desktop in your Windows search bar and open the application.
2. You may be asked to log out and log back in, or to reboot your machine to complete the WSL 2 installation.
3. After Docker Desktop starts, it will display an icon in the system tray, indicating that it's running.

### 7. Run the Docker Command
1. Open a terminal window (you can use PowerShell, Command Prompt, or Windows Terminal).
2. Type `docker --version` to check if Docker was installed correctly. You should see the Docker version number if the installation was successful.
3. Optionally, you can run `docker run hello-world` to download and run the "hello-world" Docker image, verifying that Docker can pull images and run containers.

### Additional Notes
- Docker Desktop requires an account for Docker Hub, so you might need to create one if you don't already have it.
- Depending on your version of Windows, you might encounter variations in the installation process, especially between Windows 10 and Windows 11.
- Make sure to keep your Docker Desktop application updated to take advantage of new features and security updates.


# Download and Start Geoserver Docker 

By following these steps, you should be able to install Docker Desktop on Windows and start running Docker containers.

Great, it sounds like you've identified the correct command to pull the GeoServer Docker image you need. To proceed with installing GeoServer using Docker on your Windows machine with Docker Desktop, follow these steps:

### Step 1: Open a Command-Line Interface
- You can use PowerShell, Command Prompt, or a terminal within a WSL 2 Linux distribution. Ensure Docker Desktop is running and is configured to use WSL 2 (if you're using WSL 2 for Docker).

### Step 2: Pull the GeoServer Docker Image
- Execute the command you mentioned to pull the specific version of GeoServer you need:
  ```sh
  docker pull docker.osgeo.org/geoserver:2.24.1
  ```
- This command contacts the Docker registry at `docker.osgeo.org` and pulls the `geoserver` image tagged `2.24.1`.

### Step 3: Run the GeoServer Container
- After pulling the image, you can start a GeoServer container with the following command:
  ```sh
  docker run -d -p 8080:8080 docker.osgeo.org/geoserver:2.24.1
  ```
- This command runs the container in detached mode (`-d`), maps port 8080 of the container to port 8080 on your host machine (`-p 8080:8080`), and uses the `docker.osgeo.org/geoserver:2.24.1` image.

### Step 4: Access GeoServer
- Once the container is up and running, open a web browser and navigate to `http://localhost:8080/geoserver` to access the GeoServer web interface.
- The default credentials for GeoServer are typically `admin` for the username and `geoserver` for the password, unless otherwise specified.

### Optional: Custom Configuration and Data Persistence
- If you need to customize your GeoServer setup or ensure data persistence (for things like GeoServer configurations, data stores, etc.), you can mount a volume to the container:
  ```sh
  docker run -d -p 8080:8080 -v your_local_directory:/opt/geoserver/data_dir docker.osgeo.org/geoserver:2.24.1
  ```
- Replace `your_local_directory` with the path to a directory on your host machine where you want to store the GeoServer data directory persistently.

By following these steps, you've successfully deployed GeoServer using Docker on your Windows machine. You can now begin configuring GeoServer for your specific needs, uploading geospatial data, and serving maps and data through OGC services like WMS, WFS, and WCS.
