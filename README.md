# Grocery App

A simple **Grocery Management Application** with a **Node.js backend** and **MySQL database**. The app allows users to login, view grocery items, add them to their cart, and track orders.

## 📂 Project Structure
```
grocery-app/
├── server.js             # Entry point for the Node.js server
├── package.json          # Project dependencies
├── config/               # Configuration files
│   └── db.js             # MySQL database connection
├── public/               # Frontend files
│   ├── index.html        # Login page
│   ├── cart.html         # Cart page
│   └── grocery.html      # Grocery list page
└── routes/               # Route handlers
    └── api.js            # API endpoints for login, cart, grocery
```

## 🗄️ Database Setup (MySQL)
### Create Database
```sql
CREATE DATABASE grocery_app;
USE grocery_app;
```
### Create Tables
```sql
-- Users Table
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    password VARCHAR(255) NOT NULL,
    email VARCHAR(100)
);

-- Cart Table
CREATE TABLE cart (
    id INT AUTO_INCREMENT PRIMARY KEY,
    item_name VARCHAR(100) NOT NULL,
    quantity INT DEFAULT 1
);

-- Grocery List Table
CREATE TABLE grocery_list (
    id INT AUTO_INCREMENT PRIMARY KEY,
    item_name VARCHAR(100) NOT NULL,
    quantity INT DEFAULT 1,
    price DECIMAL(10, 2),
    purchased BOOLEAN DEFAULT FALSE
);

-- Insert Sample Data
INSERT INTO grocery_list (item_name, quantity, price) VALUES
('Apple', 10, 20.50),
('Banana', 5, 15.00),
('Milk', 2, 50.00),
('Bread', 1, 30.00);

-- Signin Table
CREATE TABLE signin (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    password VARCHAR(255) NOT NULL,
    email VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Login Table
CREATE TABLE login (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    password VARCHAR(255) NOT NULL
);

-- Order Details Table
CREATE TABLE order_details (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    item_name VARCHAR(100),
    quantity INT,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
### Trigger to Sync Users with Login and Signin Tables
```sql
DELIMITER //
CREATE TRIGGER after_user_insert
AFTER INSERT ON users
FOR EACH ROW
BEGIN
    INSERT INTO signin (username, password, email)
    VALUES (NEW.username, NEW.password, NEW.email);
    
    INSERT INTO login (username, password)
    VALUES (NEW.username, NEW.password);
END //
DELIMITER ;
```

## 🚀 Getting Started
### 1️⃣ Install Dependencies
```sh
mkdir grocery-app
cd grocery-app
npm init -y
npm install express mysql body-parser
npm install mysql2
```

### 2️⃣ Start the Server
```sh
node server.js
```

## 🌍 Access the Application
- **Login Page:** [http://localhost:3000/index.html](http://localhost:3000/index.html)
- **Cart Page:** [http://localhost:3000/cart.html](http://localhost:3000/cart.html)
- **Grocery List Page:** [http://localhost:3000/grocery.html](http://localhost:3000/grocery.html)
- **Sign-up Page:** [http://localhost:3000/signup.html](http://localhost:3000/signup.html)

## 📌 Features
✅ User Authentication (Signup & Login)
✅ View Grocery Items
✅ Add Items to Cart
✅ Order Tracking
✅ MySQL Database Integration

## 🤝 Contributing
If you want to contribute, fork this repo and submit a pull request. Happy coding!



