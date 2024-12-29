# Use an official Node.js runtime as the base image
FROM node:18

# Set the working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json package-lock.json ./
RUN npm install --force

# Copy application files
COPY . .

# Build the Angular application
RUN npm run build --prod

# Expose the port the app runs on
EXPOSE 4200

# Start the application
CMD ["npm", "start"]
