# Step 1: Use an official Node.js runtime as a parent image
FROM node:18 AS builder

# Step 2: Set the working directory in the container
WORKDIR /app

# Step 3: Copy package.json and package-lock.json to leverage Docker cache
COPY package*.json ./

# Step 4: Install the Node.js dependencies inside the container
RUN npm install

# Step 5: Copy the rest of the application code to the container
COPY . .

# Step 6: Expose the port that your Node.js app will run on
EXPOSE 3000

# Step 7: Define the command to run your app
CMD ["npm", "start"]
