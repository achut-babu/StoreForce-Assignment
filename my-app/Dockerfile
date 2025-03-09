# Step 1: Use Node.js image to build the app
FROM node:16 as build

# Step 2: Set the working directory inside the container
WORKDIR /app

# Step 3: Copy package.json and package-lock.json and install dependencies
COPY package.json package-lock.json ./
RUN npm install

# Step 4: Copy the rest of the React app's source code
COPY . ./

# Step 5: Build the React application for production
RUN npm run build

# Step 6: Serve the built app using Nginx
FROM nginx:alpine

# Step 7: Copy the built React app from the build stage to the Nginx server
COPY --from=build /app/build /usr/share/nginx/html

# Step 8: Expose port 80 to access the app
EXPOSE 80

# Step 9: Start Nginx
CMD ["nginx", "-g", "daemon off;"]
