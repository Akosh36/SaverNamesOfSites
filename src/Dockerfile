# Use the official nginx image as base
FROM nginx:alpine

# Set maintainer label
LABEL maintainer="akosh12g@gmail.com"

# Copy custom nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Copy your index.html file to nginx html directory
COPY ./index.html /usr/share/nginx/html/index.html

# Or copy entire directory if you have multiple files:
# COPY ./ /usr/share/nginx/html/

# Expose port 80
EXPOSE 80

# nginx will run in the foreground
CMD ["nginx", "-g", "daemon off;"]