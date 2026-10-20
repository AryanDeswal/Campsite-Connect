# Campsite Connect

A full-stack web app for listing, reviewing and rating campgrounds, with photo uploads and an interactive cluster map.

![Node.js](https://img.shields.io/badge/Node.js-339933?logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?logo=mongodb&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap_5-7952B3?logo=bootstrap&logoColor=white)
![Mapbox](https://img.shields.io/badge/Mapbox-000000?logo=mapbox&logoColor=white)
![Cloudinary](https://img.shields.io/badge/Cloudinary-3448C5?logo=cloudinary&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

**Live demo:** https://campsiteconnect.onrender.com

## About

Campsite Connect lets people share campgrounds and help others find good places to stay. Signed-in users can add a campground with a price, description, location and photos; the location is geocoded with Mapbox and shown on a map. Other users can leave a 1 to 5 star rating and a written review. It is a server-rendered Express app using EJS templates, MongoDB for storage and Cloudinary for images.

## Features

- **Authentication** with Passport (local strategy) and `passport-local-mongoose`: register, log in, log out, and return to the page you were on after logging in.
- **Campground CRUD**: create, view, edit and delete campgrounds. Only the author can edit or delete a campground.
- **Image uploads** to Cloudinary via Multer (JPEG/PNG, multiple images per campground), with the option to delete selected images when editing.
- **Geocoding and maps**: locations are converted to coordinates with the Mapbox Geocoding API. The index page shows all campgrounds on a clustered Mapbox GL map; each campground page shows its own map.
- **Reviews and star ratings** (Starability). Only the review's author can delete it.
- **Validation** on the client (Bootstrap form validation) and server (Joi schemas with an HTML-sanitizing extension).
- **Security middleware**: Helmet, `express-mongo-sanitize` against query injection, and sessions stored in MongoDB with `connect-mongo`.
- **Flash messages** and a custom error page for unknown routes and errors.

## Tech Stack

| Layer     | Technology                                                       |
| --------- | ---------------------------------------------------------------- |
| Runtime   | Node.js                                                          |
| Server    | Express 4, express-session, connect-flash, method-override, Helmet |
| Auth      | Passport, passport-local, passport-local-mongoose                |
| Database  | MongoDB with Mongoose 7, connect-mongo (session store)           |
| Views     | EJS with ejs-mate layouts, Bootstrap 5                           |
| Media     | Cloudinary, Multer, multer-storage-cloudinary                    |
| Maps      | Mapbox SDK (geocoding), Mapbox GL JS                             |
| Validation| Joi, sanitize-html                                               |

## Project Structure

```
Campsite-Connect/
├── app.js              # App setup: DB, sessions, Passport, middleware, routes
├── middleware.js       # isLoggedIn, isAuthor, isReviewAuthor, Joi validators
├── schemas.js          # Joi schemas for campgrounds and reviews
├── cloudinary/
│   └── index.js        # Cloudinary config and Multer storage
├── controllers/        # Route handlers: campgrounds, reviews, users
├── models/             # Mongoose models: Campground, Review, User
├── routes/             # Express routers: campgrounds, reviews, users
├── utils/              # ExpressError class and catchAsync wrapper
├── views/              # EJS templates (layouts, partials, campgrounds, users)
└── public/
    ├── javascripts/    # Cluster map, show-page map, form validation
    └── stylesheets/    # App, home page and star rating styles
```

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) and npm
- A MongoDB instance (local or MongoDB Atlas)
- A [Cloudinary](https://cloudinary.com/) account
- A [Mapbox](https://www.mapbox.com/) access token

### Installation

```bash
git clone https://github.com/AryanDeswal/Campsite-Connect.git
cd Campsite-Connect
npm install
```

### Environment Variables

Create a `.env` file in the project root. It is loaded with `dotenv` when `NODE_ENV` is not `production`.

| Variable                | Purpose                                                                                 |
| ----------------------- | --------------------------------------------------------------------------------------- |
| `DB_URL`                | MongoDB connection string. Defaults to `mongodb://127.0.0.1:27017/campsite-connect`.    |
| `SECRET`                | Secret for signing and encrypting sessions. Has an insecure fallback, so always set it. |
| `CLOUDINARY_CLOUD_NAME` | Cloudinary cloud name                                                                   |
| `CLOUDINARY_KEY`        | Cloudinary API key                                                                      |
| `CLOUDINARY_SECRET`     | Cloudinary API secret                                                                   |
| `MAPBOX_TOKEN`          | Mapbox access token, used for geocoding and for the maps in the browser                 |

### Run

```bash
npm start
```

Then open http://localhost:3000. The port is fixed at 3000 in `app.js`.

For development with auto-reload, `nodemon` is included as a dev dependency:

```bash
npx nodemon app.js
```

## Routes

### Users

| Method | Route       | Description                       |
| ------ | ----------- | --------------------------------- |
| GET    | `/register` | Registration form                 |
| POST   | `/register` | Create an account and log in      |
| GET    | `/login`    | Login form                        |
| POST   | `/login`    | Log in with username and password |
| GET    | `/logout`   | Log out                           |

### Campgrounds

| Method | Route                  | Description                                 | Access          |
| ------ | ---------------------- | ------------------------------------------- | --------------- |
| GET    | `/campgrounds`         | List all campgrounds with the cluster map   | Public          |
| GET    | `/campgrounds/new`     | New campground form                         | Logged in       |
| POST   | `/campgrounds`         | Create a campground (with image uploads)    | Logged in       |
| GET    | `/campgrounds/:id`     | Campground details, map and reviews         | Public          |
| GET    | `/campgrounds/:id/edit`| Edit form                                   | Author only     |
| PUT    | `/campgrounds/:id`     | Update a campground, add or remove images   | Author only     |
| DELETE | `/campgrounds/:id`     | Delete a campground and its reviews         | Author only     |

### Reviews

| Method | Route                                   | Description     | Access          |
| ------ | --------------------------------------- | --------------- | --------------- |
| POST   | `/campgrounds/:id/reviews`              | Add a review    | Logged in       |
| DELETE | `/campgrounds/:id/reviews/:reviewId`    | Delete a review | Review author   |

PUT and DELETE are sent from HTML forms using `method-override` (`?_method=PUT` / `?_method=DELETE`).

## License

Released under the [MIT License](LICENSE).
