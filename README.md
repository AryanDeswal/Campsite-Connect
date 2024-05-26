# Campsite Connect 

## Overview
Campsite Connect is a web application designed to enhance the camping experience by providing a platform for users to list, review, and rate campsites. Built with Node.js, Express.js, Bootstrap, and MongoDB, Campsite Connect offers seamless CRUD (Create, Read, Update, Delete) operations to facilitate user engagement and interaction with campsite data.

## Features

- **User Authentication**: Utilizes Passport for secure user authentication, ensuring that only authorized users can access the platform.
  
- **Interactive Map**: Integrated Mapbox SDK to provide users with an interactive global map, allowing them to explore campsites visually.

- **CRUD Operations**: Enables users to perform CRUD operations on campsites, empowering them to add new campsites, view existing ones, update campsite information, and delete outdated entries.

- **Data Validation**: Implements robust client and server-side data validation using Bootstrap, JOI Library, and Mongoose middleware, ensuring data integrity and reliability.

## Technologies Used

- **Node.js**: A JavaScript runtime used for building scalable and efficient server-side applications.
  
- **Express.js**: A minimalist web framework for Node.js used to build the web application and handle HTTP requests.

- **MongoDB**: A NoSQL database used for storing and managing campsite data.

- **Passport**: An authentication middleware used for user authentication and session management.

- **Mapbox SDK**: Provides mapping and location services, used to create an interactive map for visualizing campsites.

- **Bootstrap**: A front-end framework used for designing responsive and visually appealing user interfaces.

- **JOI Library**: A schema validation library for JavaScript used for validating and sanitizing user input data.

- **Mongoose**: An object modeling tool for MongoDB and Node.js, used for data modeling and interacting with the MongoDB database.

## Installation

1. Clone the repository:

   ```
   git clone https://github.com/AryanDeswal/Campsite-Connect.git
   ```

2. Navigate to the project directory:

   ```
   cd campsite-connect
   ```

3. Install dependencies:

   ```
   npm install
   ```

4. Set up environment variables:

   - Create a `.env` file in the root directory.
   - Add the following environment variables:

     ```
     CLOUDINARY_CLOUD_NAME
     CLOUDINARY_KEY
     CLOUDINARY_SECRET
     DB_URL
     MAPBOX_TOKEN
     SECRET
     ```

5. Start the server:

   ```
   npm start
   ```

6. Open a web browser and visit `http://localhost:3000` to access Campsite Connect.
