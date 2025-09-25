# frontend/Dockerfile

# Use a base image with a shell and envsubst
FROM alpine AS builder

# Install gettext to get envsubst
RUN apk add --no-cache gettext

# Copy the static web content
COPY . /app

# Now use the final nginx image
FROM nginx:alpine

# Copy the Nginx configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copy the static web content from the builder stage
COPY --from=builder /app /usr/share/nginx/html

# The original CMD is now executed by the entrypoint script
EXPOSE 80

# This command uses envsubst at runtime to replace the placeholders
CMD ["/bin/sh", "-c", "envsubst < /usr/share/nginx/html/main.js > /usr/share/nginx/html/main.js.tmp && mv /usr/share/nginx/html/main.js.tmp /usr/share/nginx/html/main.js && nginx -g 'daemon off;'"]