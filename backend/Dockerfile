# Base image: Node (alpine = small)
FROM node:22-alpine

# Work inside /app in the container
WORKDIR /app

# Copy package files first so the install layer is cached
COPY package*.json ./

# Install exact versions, skip dev packages (nodemon)
RUN npm ci --omit=dev

# Copy the rest of the backend code
COPY . .

# Backend port
EXPOSE 8000

# Run as non-root user (already exists in the node image)
USER node

# Start command (from package.json "start")
CMD ["node", "index.js"]
