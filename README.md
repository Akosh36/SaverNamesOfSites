# 🌐 Site Saver - Docker Nginx Project

A lightweight, containerized web application for saving and managing your favorite websites. Built with Docker, Nginx, and vanilla JavaScript.

## 📋 Table of Contents

- [Why This Project?](#why-this-project)
- [Features](#features)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [How It Works](#how-it-works)
- [Installation & Setup](#installation--setup)
- [Usage](#usage)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)

## 🎯 Why This Project?

**Problem:** Managing bookmarks across different browsers and devices can be messy. Browser bookmarks aren't portable, and cloud solutions often require accounts and sync services.

**Solution:** Site Saver provides a simple, self-hosted bookmark manager that:
- Runs anywhere Docker is available
- Stores data locally in your browser
- Requires no backend database or authentication
- Can be deployed on any server or cloud platform
- Supports data export/import for portability
- Works offline once loaded

**Use Cases:**
- Personal bookmark management
- Quick access to frequently visited sites
- Team resource sharing (when deployed on shared server)
- Learning Docker and Nginx deployment
- Portfolio/demo project

## ✨ Features

- **Add Sites:** Save website names and URLs with one click
- **Search:** Real-time search through your saved sites
- **Delete:** Remove sites you no longer need
- **Export/Import:** Backup and restore your data as JSON
- **Responsive Design:** Works on desktop and mobile
- **Dark Theme:** Easy on the eyes with purple accents
- **Local Storage:** All data stored in browser (no server-side database needed)
- **Docker Containerized:** Easy deployment and portability

## 📁 Project Structure

```
site-saver/
├── Dockerfile              # Docker image configuration
├── nginx.conf             # Nginx web server configuration
├── index.html             # Main application (HTML + CSS + JS)
├── Makefile              # Build and deployment automation
```

### File Descriptions

**Dockerfile**
- Base image: `nginx:alpine` (lightweight Linux with Nginx)
- Copies configuration and application files
- Exposes port 80 for web traffic
- Runs Nginx in foreground mode

**nginx.conf**
- Web server configuration
- Enables gzip compression for faster loading
- Configures caching for static assets
- Sets security headers
- Handles error pages

**index.html**
- Single-page application
- No external dependencies
- Uses localStorage API for data persistence
- Vanilla JavaScript (no frameworks needed)

**Makefile**
- Automated build and deployment commands
- Creates all necessary files with `make init`
- Builds Docker image
- Runs and manages containers

## 🔧 Prerequisites

Before running this project, you need:

### Required Software

1. **Docker** (version 20.x or higher)
   - Download: https://docs.docker.com/get-docker/
   - Why: Containerizes the application for consistent deployment
   - Verify installation: `docker --version`

2. **Make** (usually pre-installed on Linux/Mac)
   - Linux: `sudo apt install make` or `sudo yum install make`
   - Mac: Comes with Xcode Command Line Tools
   - Windows: Install via chocolatey `choco install make` or use WSL
   - Why: Simplifies build and deployment commands
   - Verify installation: `make --version`

### Optional But Recommended

- **Git** - For version control
- **Text Editor** - VS Code, Sublime, or any editor
- **Web Browser** - Chrome, Firefox, Safari, Edge

### System Requirements

- **OS:** Linux, macOS, Windows (with WSL2 for best experience)
- **RAM:** 512MB minimum (Docker overhead)
- **Disk:** 100MB for Docker image
- **Ports:** Port 8080 available (or modify in Makefile)

## ⚙️ How It Works

### Architecture Overview

```
User Browser ←→ Docker Container ←→ Nginx ←→ index.html
                                              ↓
                                        localStorage
```

### Workflow

1. **Build Phase:**
   - Makefile creates Dockerfile, nginx.conf, and index.html
   - Docker builds image based on nginx:alpine
   - Application files are copied into the image

2. **Run Phase:**
   - Docker creates container from image
   - Nginx starts and serves index.html on port 80
   - Host port 8080 maps to container port 80

3. **Application Phase:**
   - User opens http://localhost:8080 in browser
   - JavaScript loads saved sites from localStorage
   - User can add, search, delete, export, or import sites
   - All data persists in browser's localStorage

### Data Flow

```
User Action → JavaScript Function → localStorage API → Browser Storage
                                                              ↓
                                                        Data persists
                                                              ↓
                                                    Available on reload
```

### Key Technologies

- **Docker:** Application containerization
- **Nginx:** High-performance web server
- **HTML5:** Structure and markup
- **CSS3:** Inline styling for simplicity
- **JavaScript (ES6+):** Application logic
- **localStorage API:** Client-side data persistence
- **JSON:** Data format for import/export

## 🚀 Installation & Setup

### Quick Start (One Command)

```bash
# Clone or create project directory
mkdir site-saver && cd site-saver

# Download the Makefile (or create it manually)
# Then run:
make all
```

This single command will:
1. ✅ Create Dockerfile
2. ✅ Create nginx.conf
3. ✅ Create index.html
4. ✅ Build Docker image
5. ✅ Run container
6. ✅ Start application on http://localhost:8080

### Step-by-Step Installation

If you prefer manual setup:

**Step 1: Create Project Directory**
```bash
mkdir site-saver
cd site-saver
```

**Step 2: Create Makefile**
```bash
# Copy the Makefile content into a file named 'Makefile'
# (No file extension)
```

**Step 3: Initialize Project**
```bash
make init
```

**Step 4: Build Docker Image**
```bash
make build
```

**Step 5: Run Container**
```bash
make run
```

**Step 6: Access Application**
```
Open browser: http://localhost:8080
```

## 📖 Usage

### Makefile Commands

```bash
make help       # Show all available commands
make init       # Create project files
make all        # Setup everything and run
make build      # Build Docker image
make run        # Start container
make start      # Build and run
make stop       # Stop container
make restart    # Restart container
make logs       # View container logs
make shell      # Open shell in container
make clean      # Remove container
make prune      # Remove container and image
make status     # Check container status
make rebuild    # Clean build from scratch
```

### Application Usage

**Adding a Site:**
1. Enter site name (e.g., "GitHub")
2. Enter URL (e.g., "https://github.com")
3. Click "Add" button

**Searching Sites:**
- Type in search box
- Results filter in real-time

**Deleting a Site:**
- Click red "delete" button
- Confirm deletion

**Exporting Data:**
- Click "Export JSON" button
- Save file to your computer

**Importing Data:**
- Click "Import JSON" button
- Select previously exported JSON file
- Data will be restored

### Customization

**Change Port:**
Edit Makefile:
```makefile
PORT = 9000  # Change from 8080 to 9000
```

**Modify Styling:**
Edit `index.html` inline styles or add external CSS

**Add Features:**
Extend JavaScript functions in `index.html`

**Change Container Name:**
Edit Makefile:
```makefile
CONTAINER_NAME = my-custom-name
```

## 🔧 Configuration

### Nginx Configuration Highlights

```nginx
# Performance
worker_processes auto;        # Use all CPU cores
gzip on;                      # Compress responses
sendfile on;                  # Efficient file serving

# Security
add_header X-Frame-Options "SAMEORIGIN";
add_header X-Content-Type-Options "nosniff";
add_header X-XSS-Protection "1; mode=block";

# Caching
location ~* \.(jpg|css|js)$ {
    expires 1y;
}
```

### Docker Configuration

```dockerfile
FROM nginx:alpine           # Lightweight base
COPY nginx.conf /etc/nginx/ # Custom config
COPY index.html /usr/share/nginx/html/
EXPOSE 80                   # HTTP port
```

## 🐛 Troubleshooting

### Port Already in Use

**Error:** `Bind for 0.0.0.0:8080 failed: port is already allocated`

**Solution:**
```bash
# Option 1: Stop conflicting service
sudo lsof -i :8080
sudo kill -9 <PID>

# Option 2: Use different port
# Edit Makefile: PORT = 8081
make restart
```

### Container Won't Start

**Check logs:**
```bash
make logs
```

**Common issues:**
- Nginx config syntax error: Validate nginx.conf
- File not found: Ensure all files exist
- Docker daemon not running: `sudo systemctl start docker`

### Cannot Access Site

**Verify container is running:**
```bash
make status
docker ps
```

**Test port:**
```bash
curl http://localhost:8080
```

**Check firewall:**
```bash
sudo ufw status
sudo ufw allow 8080
```

### Build Fails

**Clear Docker cache:**
```bash
make prune
docker system prune -a
make build
```

### Data Not Persisting

- localStorage is browser-specific
- Clear cache will delete data
- Use Export feature regularly for backups
- Data doesn't sync across browsers

## 🤝 Contributing

Contributions welcome! Areas for improvement:

- Add categories/tags for sites
- Implement server-side storage option
- Add authentication for shared deployments
- Create browser extension
- Add import from browser bookmarks
- Implement PWA features
- Add keyboard shortcuts
- Create API for external access

## 📄 License

This project is open source and available for educational purposes.

## 👨‍💻 Author

**AkobirBB**

- [Linkedin](https://www.linkedin.com/in/bozorovakobir/)
- [Telegram](https://t.me/Akobir36)

---

## 📚 Additional Resources

- [Docker Documentation](https://docs.docker.com/)
- [Nginx Documentation](https://nginx.org/en/docs/)
- [MDN Web Docs - localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
- [Makefile Tutorial](https://makefiletutorial.com/)

---

**Happy Coding! 🚀**

If you find this project useful, please give it a star ⭐