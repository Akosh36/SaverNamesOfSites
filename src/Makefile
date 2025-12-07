# Makefile for nginx Docker container

# Variables
IMAGE_NAME = my-nginx
CONTAINER_NAME = nginx-container
PORT = 8080

# Default target
.PHONY: help
help:
	@echo "Available commands:"
	@echo "  make init       - Create all necessary files (Dockerfile, nginx.conf, index.html)"
	@echo "  make all        - Create files, build, and run everything"
	@echo "  make build      - Build the Docker image"
	@echo "  make run        - Run the container"
	@echo "  make start      - Build and run the container"
	@echo "  make stop       - Stop the running container"
	@echo "  make restart    - Restart the container"
	@echo "  make logs       - Show container logs"
	@echo "  make shell      - Open shell in running container"
	@echo "  make clean      - Stop and remove container"
	@echo "  make prune      - Remove container and image"
	@echo "  make status     - Show container status"

# Create all necessary files
.PHONY: init
init:
	@echo "Creating project files..."
	@if [ ! -f Dockerfile ]; then \
		echo "Creating Dockerfile..."; \
		echo '# Use the official nginx image as base' > Dockerfile; \
		echo 'FROM nginx:alpine' >> Dockerfile; \
		echo '' >> Dockerfile; \
		echo '# Set maintainer label' >> Dockerfile; \
		echo 'LABEL maintainer="your-email@example.com"' >> Dockerfile; \
		echo '' >> Dockerfile; \
		echo '# Copy custom nginx configuration' >> Dockerfile; \
		echo 'COPY nginx.conf /etc/nginx/nginx.conf' >> Dockerfile; \
		echo '' >> Dockerfile; \
		echo '# Copy your index.html file to nginx html directory' >> Dockerfile; \
		echo 'COPY index.html /usr/share/nginx/html/index.html' >> Dockerfile; \
		echo '' >> Dockerfile; \
		echo '# Or copy entire directory if you have multiple files:' >> Dockerfile; \
		echo '# COPY ./ /usr/share/nginx/html/' >> Dockerfile; \
		echo '' >> Dockerfile; \
		echo '# Expose port 80' >> Dockerfile; \
		echo 'EXPOSE 80' >> Dockerfile; \
		echo '' >> Dockerfile; \
		echo '# nginx will run in the foreground' >> Dockerfile; \
		echo 'CMD ["nginx", "-g", "daemon off;"]' >> Dockerfile; \
	fi
	@if [ ! -f nginx.conf ]; then \
		echo "Creating nginx.conf..."; \
		echo '# Main nginx configuration' > nginx.conf; \
		echo 'user nginx;' >> nginx.conf; \
		echo 'worker_processes auto;' >> nginx.conf; \
		echo 'error_log /var/log/nginx/error.log warn;' >> nginx.conf; \
		echo 'pid /var/run/nginx.pid;' >> nginx.conf; \
		echo '' >> nginx.conf; \
		echo 'events {' >> nginx.conf; \
		echo '    worker_connections 1024;' >> nginx.conf; \
		echo '}' >> nginx.conf; \
		echo '' >> nginx.conf; \
		echo 'http {' >> nginx.conf; \
		echo '    include /etc/nginx/mime.types;' >> nginx.conf; \
		echo '    default_type application/octet-stream;' >> nginx.conf; \
		echo '' >> nginx.conf; \
		echo '    log_format main '"'"'$remote_addr - $remote_user [$time_local] "$request" '"'"'' >> nginx.conf; \
		echo '                    '"'"'$status $body_bytes_sent "$http_referer" '"'"'' >> nginx.conf; \
		echo '                    '"'"'"$http_user_agent" "$http_x_forwarded_for"'"'"';' >> nginx.conf; \
		echo '' >> nginx.conf; \
		echo '    access_log /var/log/nginx/access.log main;' >> nginx.conf; \
		echo '' >> nginx.conf; \
		echo '    sendfile on;' >> nginx.conf; \
		echo '    tcp_nopush on;' >> nginx.conf; \
		echo '    tcp_nodelay on;' >> nginx.conf; \
		echo '    keepalive_timeout 65;' >> nginx.conf; \
		echo '    types_hash_max_size 2048;' >> nginx.conf; \
		echo '' >> nginx.conf; \
		echo '    gzip on;' >> nginx.conf; \
		echo '    gzip_vary on;' >> nginx.conf; \
		echo '    gzip_min_length 1000;' >> nginx.conf; \
		echo '    gzip_types text/plain text/css text/xml text/javascript application/x-javascript application/xml+rss application/json application/javascript;' >> nginx.conf; \
		echo '' >> nginx.conf; \
		echo '    server {' >> nginx.conf; \
		echo '        listen 80;' >> nginx.conf; \
		echo '        server_name localhost;' >> nginx.conf; \
		echo '        root /usr/share/nginx/html;' >> nginx.conf; \
		echo '        index index.html index.htm;' >> nginx.conf; \
		echo '' >> nginx.conf; \
		echo '        location / {' >> nginx.conf; \
		echo '            try_files $uri $uri/ =404;' >> nginx.conf; \
		echo '        }' >> nginx.conf; \
		echo '' >> nginx.conf; \
		echo '        location ~* \.(jpg|jpeg|png|gif|ico|css|js|svg|woff|woff2|ttf|eot)$ {' >> nginx.conf; \
		echo '            expires 1y;' >> nginx.conf; \
		echo '            add_header Cache-Control "public, immutable";' >> nginx.conf; \
		echo '        }' >> nginx.conf; \
		echo '' >> nginx.conf; \
		echo '        error_page 404 /404.html;' >> nginx.conf; \
		echo '        error_page 500 502 503 504 /50x.html;' >> nginx.conf; \
		echo '' >> nginx.conf; \
		echo '        add_header X-Frame-Options "SAMEORIGIN" always;' >> nginx.conf; \
		echo '        add_header X-Content-Type-Options "nosniff" always;' >> nginx.conf; \
		echo '        add_header X-XSS-Protection "1; mode=block" always;' >> nginx.conf; \
		echo '' >> nginx.conf; \
		echo '        location ~ /\. {' >> nginx.conf; \
		echo '            deny all;' >> nginx.conf; \
		echo '            access_log off;' >> nginx.conf; \
		echo '            log_not_found off;' >> nginx.conf; \
		echo '        }' >> nginx.conf; \
		echo '    }' >> nginx.conf; \
		echo '}' >> nginx.conf; \
	fi
	@if [ ! -f index.html ]; then \
		echo "Creating index.html..."; \
		echo '<!DOCTYPE html>' > index.html; \
		echo '<html lang="en">' >> index.html; \
		echo '<head>' >> index.html; \
		echo '    <meta charset="UTF-8">' >> index.html; \
		echo '    <meta name="viewport" content="width=device-width, initial-scale=1.0">' >> index.html; \
		echo '    <title>Welcome to Nginx</title>' >> index.html; \
		echo '    <style>' >> index.html; \
		echo '        body {' >> index.html; \
		echo '            font-family: Arial, sans-serif;' >> index.html; \
		echo '            display: flex;' >> index.html; \
		echo '            justify-content: center;' >> index.html; \
		echo '            align-items: center;' >> index.html; \
		echo '            height: 100vh;' >> index.html; \
		echo '            margin: 0;' >> index.html; \
		echo '            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);' >> index.html; \
		echo '            color: white;' >> index.html; \
		echo '        }' >> index.html; \
		echo '        .container {' >> index.html; \
		echo '            text-align: center;' >> index.html; \
		echo '        }' >> index.html; \
		echo '        h1 { font-size: 3em; margin: 0; }' >> index.html; \
		echo '        p { font-size: 1.2em; }' >> index.html; \
		echo '    </style>' >> index.html; \
		echo '</head>' >> index.html; \
		echo '<body>' >> index.html; \
		echo '    <div class="container">' >> index.html; \
		echo '        <h1>🚀 Hello from Nginx!</h1>' >> index.html; \
		echo '        <p>Your Docker container is running successfully.</p>' >> index.html; \
		echo '    </div>' >> index.html; \
		echo '</body>' >> index.html; \
		echo '</html>' >> index.html; \
	fi
	@echo "✓ All files created successfully!"

# Create everything and run
.PHONY: all
all: init start
	@echo ""
	@echo "================================================"
	@echo "✓ Setup complete!"
	@echo "✓ Your nginx server is running at http://localhost:$(PORT)"
	@echo "================================================"

# Build the Docker image
.PHONY: build
build:
	@echo "Building Docker image..."
	docker build -t $(IMAGE_NAME) .
	@echo "Build complete!"

# Run the container
.PHONY: run
run:
	@echo "Starting container..."
	docker run -d \
		--name $(CONTAINER_NAME) \
		-p $(PORT):80 \
		$(IMAGE_NAME)
	@echo "Container started on http://localhost:$(PORT)"

# Build and run
.PHONY: start
start: build run

# Stop the container
.PHONY: stop
stop:
	@echo "Stopping container..."
	docker stop $(CONTAINER_NAME)
	@echo "Container stopped"

# Restart the container
.PHONY: restart
restart: stop start

# Show logs
.PHONY: logs
logs:
	docker logs -f $(CONTAINER_NAME)

# Open shell in container
.PHONY: shell
shell:
	docker exec -it $(CONTAINER_NAME) /bin/sh

# Stop and remove container
.PHONY: clean
clean:
	@echo "Cleaning up..."
	-docker stop $(CONTAINER_NAME)
	-docker rm $(CONTAINER_NAME)
	@echo "Cleanup complete"

# Remove container and image
.PHONY: prune
prune: clean
	@echo "Removing image..."
	-docker rmi $(IMAGE_NAME)
	@echo "Prune complete"

# Show container status
.PHONY: status
status:
	@docker ps -a | grep $(CONTAINER_NAME) || echo "Container not found"

# Rebuild (clean build)
.PHONY: rebuild
rebuild: clean build run