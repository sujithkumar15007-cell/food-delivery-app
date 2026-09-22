# 🍔 TastyGo — Food Delivery Application (MERN Stack)

A full-stack food delivery platform where users can browse restaurants,
order food (including a dedicated **Diet / Healthy Food** section), track
orders in real time, and where restaurant owners can manage their menu and
incoming orders from a dashboard.

## ✨ Features

- **Attractive home page** with a hero banner, diet-food image gallery, "Shop by
  Diet Goal" categories (Vegan, Keto, Low-Calorie, High-Protein), featured
  healthy dishes, and popular restaurants.
- **JWT authentication** — register/login as a Customer or Restaurant owner.
- **Restaurant browsing** with search and filters (cuisine, diet tags, diet-friendly only).
- **Menu browsing** with category tabs, diet tags, calorie info, veg/non-veg indicators.
- **Cart & Checkout** — add items, adjust quantities, enter delivery address, choose payment method.
- **Real-time order tracking** (Socket.IO) — Placed → Confirmed → Preparing → Out for Delivery → Delivered.
- **Restaurant Dashboard** — manage menu items, view incoming orders live, update order status.
- **MongoDB models** for Users, Restaurants, Menu Items, and Orders.
- Seed script with demo restaurants, diet-special dishes, and demo login accounts.

## 🗂️ Project Structure

```
food-delivery-app/
├── backend/                # Node.js + Express + MongoDB API
│   ├── config/db.js
│   ├── models/              (User, Restaurant, MenuItem, Order)
│   ├── controllers/
│   ├── routes/
│   ├── middleware/          (JWT auth, error handling)
│   ├── utils/seeder.js       (demo data)
│   ├── server.js             (Express + Socket.IO server)
│   ├── package.json
│   └── .env.example
└── frontend/                # React.js client
    ├── public/
    ├── src/
    │   ├── components/       (Navbar, Footer, cards, ProtectedRoute)
    │   ├── context/           (AuthContext, CartContext)
    │   ├── pages/              (Home, Login, Register, Restaurants,
    │   │                        RestaurantDetail, Cart, Checkout,
    │   │                        MyOrders, OrderTracking, Dashboard)
    │   ├── services/          (api.js — axios, socket.js — Socket.IO client)
    │   ├── App.js
    │   └── index.js
    ├── package.json
    └── .env.example
```

## 🚀 Getting Started

### Prerequisites
- Node.js v18+
- MongoDB running locally OR a free MongoDB Atlas cluster

### 1. Backend Setup

```bash
cd backend
npm install
```

A working `.env` file is already included, pre-configured to connect to your
local MongoDB (the one visible in MongoDB Compass) and its **foodreceipe**
database:

```
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/foodreceipe
JWT_SECRET=tastygo_super_secret_jwt_key_change_in_production_123456
JWT_EXPIRE=7d
CLIENT_URL=http://localhost:3000
```

Just make sure your local MongoDB server is running (Compass shows it
connected already), then continue below. If your MongoDB requires a username/
password, update `MONGO_URI` to `mongodb://username:password@127.0.0.1:27017/foodreceipe`.

Seed the database with demo restaurants, diet-special dishes, and demo accounts:

```bash
npm run seed
```

Start the API server:

```bash
npm run dev
```

The API will run at `http://localhost:5000`. Test it: `http://localhost:5000/api/health`

### 2. Frontend Setup

Open a new terminal:

```bash
cd frontend
npm install
cp .env.example .env
npm start
```

The app opens at `http://localhost:3000`.

### 3. Demo Logins (after running `npm run seed`)

| Role       | Email                          | Password    |
|------------|---------------------------------|-------------|
| Customer   | customer-demo@fooddelivery.com | password123 |
| Restaurant | owner-demo@fooddelivery.com    | password123 |

Login as the restaurant owner to see the **Dashboard** with the seeded
restaurants ("Green Bowl Kitchen", "Spice Villa", "FitFuel Meals", "Pizza
Planet") and manage their menus/orders.

## 🔌 API Overview

| Method | Endpoint                              | Description                          |
|--------|-----------------------------------------|---------------------------------------|
| POST   | /api/auth/register                     | Register a user                      |
| POST   | /api/auth/login                        | Login                                 |
| GET    | /api/auth/profile                      | Get current user profile (auth)      |
| GET    | /api/restaurants                       | List restaurants (filters: search, cuisine, dietFriendly, tag) |
| GET    | /api/restaurants/:id                   | Restaurant details + menu             |
| POST   | /api/restaurants                       | Create restaurant (restaurant role)  |
| GET    | /api/menu/diet/featured                | Featured diet/healthy items (home page) |
| GET    | /api/menu/:restaurantId                | Menu for a restaurant                 |
| POST   | /api/orders                            | Place an order (auth)                |
| GET    | /api/orders/myorders                   | Logged-in user's orders               |
| GET    | /api/orders/:id                        | Order details (for tracking)          |
| PUT    | /api/orders/:id/status                 | Update order status (restaurant role) |

Real-time events (Socket.IO): `newOrder` (to restaurant room), `orderUpdate` (to user room).

## 🧩 Extending the Project

- **Payment gateway**: integrate Razorpay/Stripe in `Checkout.js` and `orderController.js`.
- **Live delivery map tracking**: add a delivery-agent role + location updates over Socket.IO, render with a maps library.
- **Ratings & reviews**: add a `Review` model linked to `Order` + `Restaurant`.
- **Image uploads**: `multer` is already included in backend dependencies for restaurant/menu image uploads.

## 🛠️ Tech Stack

**Frontend:** React 18, React Router v6, Axios, Socket.IO client, React Icons, React Toastify
**Backend:** Node.js, Express, MongoDB + Mongoose, JWT, bcryptjs, Socket.IO, Multer

---
Built as a demonstration of full-stack MERN architecture, REST API design, and real-time features.
"# sujith-" 
