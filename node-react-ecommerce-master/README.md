# Node + React E‑Commerce (MERN)

Full‑stack e‑commerce app built with **Node/Express + MongoDB** on the backend and **React + Redux** on the frontend.

Repository (GitHub): `https://github.com/adityasharma84640-rgb/node-react-ecommerce`

This repo is based on Basir Jafarzadeh’s “Amazona” tutorial project (2020) and has been kept as a runnable reference/portfolio project.

## Features
- Product listing, search, category filter, and sort
- Product details + reviews/ratings
- Cart + checkout flow
- User authentication (JWT)
- Admin product management (create/update/delete)
- Image upload (local `uploads/` and optional AWS S3)
- PayPal client id endpoint (PayPal integration depends on your client id)

## Tech Stack
- Backend: Node.js, Express, MongoDB (Mongoose), JWT, Multer
- Frontend: React, Redux, React Router, Axios

## Project Structure
- `backend/` – Express API + MongoDB models
- `frontend/` – React app (Create React App)
- `uploads/` – local upload folder (ignored in git)

## Prerequisites
- Node.js (the project `engines` specify Node **12.4.0** and npm **6.9.0**)
  - Recommended: use `nvm` to match the required version.
- MongoDB (local) or a MongoDB Atlas connection string

## Environment Variables
Create a `.env` file in the project root (same folder as the root `package.json`). Example:

```bash
PORT=5000
MONGODB_URL=mongodb://localhost/amazona
JWT_SECRET=change_me
PAYPAL_CLIENT_ID=sb
# Optional (only needed if using S3 upload endpoint)
accessKeyId=YOUR_AWS_ACCESS_KEY_ID
secretAccessKey=YOUR_AWS_SECRET_ACCESS_KEY
```

Notes:
- If you don’t provide a `.env`, the backend uses reasonable defaults (see `backend/config.js`).
- The frontend proxies API requests to `http://127.0.0.1:5000` (see `frontend/package.json`).

## Run Locally (Development)

### 1) Start MongoDB
Make sure MongoDB is running (local service) or set `MONGODB_URL` to your Atlas URI.

### 2) Install and start the backend
From the project root:

```bash
npm install
npm start
```

Backend runs at: `http://localhost:5000`

### 3) Install and start the frontend
In a new terminal:

```bash
cd frontend
npm install
npm start
```

Frontend runs at: `http://localhost:3000`

## Bootstrap / Admin Setup

### Create an admin user (one-time)
Open this URL in your browser (or use curl):
- `http://localhost:5000/api/users/createadmin`

Default credentials created by this endpoint:
- Email: `admin@example.com`
- Password: `1234`

### Login (admin)
- `http://localhost:3000/signin`

### Create products
- `http://localhost:3000/products`

## Production Build
The backend is written using ES modules and compiled to `dist/` for production.

```bash
npm run build
node dist/server.js
```

The production server serves the React build from `frontend/build/`.

## Deployment (Render.com)
This app can be deployed as a single Node web service that serves both the API and the built React frontend.

1) Create a MongoDB database (recommended: MongoDB Atlas) and copy the connection string.
2) On Render, create a new **Web Service** from this GitHub repo.
3) Set the following in Render:
- Build Command: `npm install && npm run build`
- Start Command: `node dist/server.js`
4) Add environment variables:
- `MONGODB_URL` = your Atlas URI
- `JWT_SECRET` = a long random string
- `PAYPAL_CLIENT_ID` = your PayPal client id (or keep `sb` for sandbox)

Note: this project was originally built for Node 12.x; if your deploy platform does not support Node 12, you may need to upgrade Node/dependencies.

## Common Issues
- **Node version mismatch**: if `npm install` fails, switch to Node 12.x (recommended: `nvm install 12.4.0 && nvm use 12.4.0`).
- **Mongo connection errors**: confirm MongoDB is running and that `MONGODB_URL` is correct.
- **AWS S3 uploads**: the `/api/uploads/s3` endpoint requires valid AWS credentials and an existing S3 bucket (see `backend/routes/uploadRoute.js`).

## License
ISC (see `package.json`).
