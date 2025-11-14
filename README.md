# ☍ Site Saver ☍

A simple, elegant bookmark manager web application that allows you to save, search, and organize your favorite websites. Built with vanilla JavaScript and deployed using Docker + Nginx.

## 🌟 Features

- **Add Websites**: Save websites with custom names and URLs
- **Search Functionality**: Quickly find saved sites by name or URL
- **Export/Import**: Backup and restore your bookmarks as JSON files
- **Responsive Design**: Works seamlessly on desktop and mobile devices
- **Local Storage**: All data is stored locally in your browser
- **Dark Theme**: Easy on the eyes with a purple-themed dark interface
- **Docker Ready**: Quick deployment with Docker Compose

## 🛠️ Tech Stack

- **Frontend**: HTML, CSS (inline), Vanilla JavaScript
- **Storage**: Browser LocalStorage
- **Server**: Nginx
- **Container**: Docker & Docker Compose

## 📋 Prerequisites

Before you begin, ensure you have the following installed on your computer:

- [Docker](https://docs.docker.com/get-docker/) (version 20.10 or higher)
- [Docker Compose](https://docs.docker.com/compose/install/) (version 1.29 or higher)
- Git (optional, for cloning the repository)

### Verify Installation

```bash
docker --version
docker-compose --version
```

## 🚀 Quick Start

### Option 1: Clone the Repository

```bash
# Clone the repository
git clone <your-repository-url>
cd site-saver

# Navigate to the src directory
cd src

# Start the application
docker-compose up -d

# Access the application
# Open your browser and go to: http://localhost:8080
```

### Option 2: Manual Setup

If you want to build this project from scratch on another computer, follow these steps:

## 📦 Step-by-Step Setup on a New Computer

### Step 1: Create Project Structure

```bash
# Create the main project directory
mkdir site-saver
cd site-saver

# Create the necessary subdirectories
mkdir -p src/static-dashboard
```

### Step 2: Create the HTML File

Create a file named `index.html` inside `src/static-dashboard/`:

```bash
# Navigate to the static-dashboard directory
cd src/static-dashboard

# Create index.html (use your preferred text editor)
nano index.html  # or vim, code, etc.
```

Copy the entire HTML content from the document provided (the HTML file with the Site Saver application).

### Step 3: Create Docker Compose Configuration

Navigate back to the `src` directory and create `docker-compose.yml`:

```bash
# Go back to src directory
cd ..

# Create docker-compose.yml
nano docker-compose.yml
```

Add the following content:

```yaml
services:
  nginx:
    image: nginx:latest
    container_name: nginx_server
    ports:
      - "8080:80"
    volumes:
      - ./static-dashboard:/usr/share/nginx/html
```

### Step 4: Create README (Optional)

Navigate to the project root and create `README.md`:

```bash
# Go to project root
cd ..

# Create README.md
nano README.md
```

### Step 5: Verify Project Structure

Your project structure should look like this:

```
site-saver/
├── README.md
└── src/
    ├── docker-compose.yml
    └── static-dashboard/
        └── index.html
```

Verify with:

```bash
# From the project root
tree
# or
find . -type f
```

### Step 6: Build and Run the Application

```bash
# Navigate to the src directory
cd src

# Start the Docker containers
docker-compose up -d

# Verify the container is running
docker ps
```

You should see output similar to:

```
CONTAINER ID   IMAGE          COMMAND                  STATUS         PORTS                  NAMES
xxxxxxxxxxxx   nginx:latest   "/docker-entrypoint.…"   Up 2 seconds   0.0.0.0:8080->80/tcp   nginx_server
```

### Step 7: Access the Application

Open your web browser and navigate to:

```
http://localhost:8080
```

You should see the Site Saver application!

## 📖 Usage Guide

### Adding a Website

1. Enter the website name in the "Sayt nomi" field
2. Enter the URL in the "https://..." field (you can omit `https://` - it will be added automatically)
3. Click the "Qo'shish" (Add) button
4. The site will appear in the list below

### Searching for Websites

- Type in the "Qidirish..." (Search) field
- The list will automatically filter based on your search query
- Search works on both website names and URLs

### Deleting a Website

- Click the red "delete" button next to any saved website
- Confirm the deletion in the popup dialog

### Exporting Your Bookmarks

1. Click the "Export JSON" button
2. A JSON file named `sites_backup.json` will be downloaded
3. Save this file in a secure location as a backup

### Importing Bookmarks

1. Click the "Import JSON" button
2. Select a previously exported JSON file
3. Your bookmarks will be restored

## 🔧 Docker Commands

### Start the Application

```bash
cd src
docker-compose up -d
```

### Stop the Application

```bash
docker-compose down
```

### View Logs

```bash
docker-compose logs -f nginx
```

### Restart the Application

```bash
docker-compose restart
```

### Remove Container and Clean Up

```bash
docker-compose down -v
```

## 🌐 Changing the Port

If port 8080 is already in use on your system, you can change it:

1. Edit `docker-compose.yml`
2. Change the ports line from `"8080:80"` to `"YOUR_PORT:80"`
3. For example: `"3000:80"` to use port 3000
4. Restart the container: `docker-compose down && docker-compose up -d`
5. Access at: `http://localhost:YOUR_PORT`

## 💾 Data Storage

All bookmark data is stored in your browser's LocalStorage under the key `sitesDB_minimal`. This means:

- ✅ No server-side database required
- ✅ Fast and responsive
- ✅ Works offline
- ⚠️ Data is specific to the browser you're using
- ⚠️ Clearing browser data will delete your bookmarks (use Export feature to backup!)

## 🔒 Security Notes

- This application stores data only in your browser
- No data is sent to any external servers
- All URLs open in new tabs for security
- Always verify URLs before adding them

## 🐛 Troubleshooting

### Port Already in Use

**Error**: `Bind for 0.0.0.0:8080 failed: port is already allocated`

**Solution**: Change the port in `docker-compose.yml` as described above.

### Container Won't Start

```bash
# Check if Docker is running
docker info

# Check container logs
docker-compose logs nginx

# Restart Docker service (Linux)
sudo systemctl restart docker

# Restart Docker Desktop (Mac/Windows)
```

### Can't Access the Application

1. Verify the container is running: `docker ps`
2. Check if you're using the correct URL: `http://localhost:8080`
3. Try using `http://127.0.0.1:8080` instead
4. Check firewall settings

### Empty Page or 404 Error

1. Verify the file structure is correct
2. Ensure `index.html` is in `src/static-dashboard/`
3. Restart the container: `docker-compose restart`

## 🤝 Contributing

Feel free to fork this project and submit pull requests for any improvements!

## 📄 License

This project is open source and available for personal and commercial use.

## 👤 Author

**Akobir**

## 🙏 Acknowledgments

- Built with ❤️ using vanilla JavaScript
- Deployed with Docker and Nginx
- Purple theme inspired by modern dark mode designs

---

**Enjoy saving your favorite sites! ☍**
