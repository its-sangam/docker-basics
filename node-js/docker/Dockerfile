# Dockerfile
FROM node:16

# Create and set working directory
WORKDIR /usr/src/app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy application files
COPY . .

# Expose port (for documentation, not runtime binding)
EXPOSE ${APP_PORT}

# Start the server
CMD ["node", "app.js"]
