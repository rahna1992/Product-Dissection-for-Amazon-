Amazon Data Model and Schema
This repository contains the data model and schema design for Amazon, showcasing how the platform manages its complex e-commerce functionalities. The schema includes entities such as Users, Products, Orders, Reviews, Sellers, and more, reflecting the intricate interactions and relationships that drive Amazon's robust platform.

Table of Contents
Introduction
Entities and Attributes
Entity-Relationship Diagram
Schema Definition
Usage
Contributing
License
Introduction
Amazon, founded in 1994 by Jeff Bezos, has transformed the e-commerce industry by offering a vast array of products and services to a global customer base. This repository presents the data model and schema for Amazon, illustrating how the platform manages users, products, orders, reviews, sellers, and payments to provide a seamless shopping experience.

Entities and Attributes
User Entity
UserID (Primary Key): A unique identifier for each user.
Username: The chosen username for the user's account.
Email: The user's email address for account-related communication.
Full_Name: The user's full name as provided during registration.
Registration_Date: The date when the user joined Amazon.
Seller Entity
SellerID (Primary Key): A unique identifier for each seller.
Name: The name of the seller or seller company.
Seller_Location: The location or address of the seller.
Seller_Join_Date: The date when the seller joined Amazon as a seller.
Product Entity
ProductID (Primary Key): A unique identifier for each product.
SellerID (Foreign Key): The seller offering the product.
Name: The title or name of the product.
Description: A brief description providing details about the product.
Price: The price of the product.
Category: The category or type of product (e.g., electronics, books, clothing).
Order Entity
OrderID (Primary Key): A unique identifier for each order.
UserID (Foreign Key): The user who placed the order.
ProductID (Foreign Key): The product purchased in the order.
Order_Date: The date when the order was placed.
Total_Amount: The total amount paid for the order.
Order_Status: The status of the order (e.g., pending, shipped, delivered).
Review Entity
ReviewID (Primary Key): A unique identifier for each review.
UserID (Foreign Key): The user who posted the review.
ProductID (Foreign Key): The product being reviewed.
Rating: The rating or score given by the user for the product.
Comment: The text of the review providing additional details and insights.
Review_Date: The date when the review was posted.
Payment Entity
PaymentID (Primary Key): A unique identifier for each payment.
OrderID (Foreign Key): The order associated with the payment.
Payment_Method: The method used for payment (e.g., credit card, PayPal).
Payment_Amount: The amount paid.
Payment_Date: The date when the payment was made.
Cart Entity
CartID (Primary Key): A unique identifier for each cart.
UserID (Foreign Key): The user who owns the cart.
Created_Date: The date when the cart was created.
Entity-Relationship Diagram
The ER diagram illustrates the relationships and attributes of the entities within the Amazon schema. This visual representation provides insights into the fundamental components of Amazon's data model, highlighting the intricate interactions and connections that drive the platform's functionality.

Schema Definition
The schema definitions for each entity are provided below:-- User Entity
CREATE TABLE Users (
    UserID SERIAL PRIMARY KEY,
    Username VARCHAR(50) NOT NULL,
    Email VARCHAR(100) NOT NULL,
    Full_Name VARCHAR(100),
    Registration_Date DATE
);

-- Seller Entity
CREATE TABLE Sellers (
    SellerID SERIAL PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Seller_Location VARCHAR(200),
    Seller_Join_Date DATE
);

-- Product Entity
CREATE TABLE Products (
    ProductID SERIAL PRIMARY KEY,
    SellerID INT REFERENCES Sellers(SellerID),
    Name VARCHAR(100) NOT NULL,
    Description TEXT,
    Price DECIMAL(10, 2),
    Category VARCHAR(50)
);

-- Order Entity
CREATE TABLE Orders (
    OrderID SERIAL PRIMARY KEY,
    UserID INT REFERENCES Users(UserID),
    ProductID INT REFERENCES Products(ProductID),
    Order_Date DATE,
    Total_Amount DECIMAL(10, 2),
    Order_Status VARCHAR(50)
);

-- Payment Entity
CREATE TABLE Payments (
    PaymentID SERIAL PRIMARY KEY,
    OrderID INT REFERENCES Orders(OrderID),
    Payment_Method VARCHAR(50),
    Payment_Amount DECIMAL(10, 2),
    Payment_Date DATE
);

-- Review Entity
CREATE TABLE Reviews (
    ReviewID SERIAL PRIMARY KEY,
    UserID INT REFERENCES Users(UserID),
    ProductID INT REFERENCES Products(ProductID),
    Rating INT CHECK (Rating BETWEEN 1 AND 5),
    Comment TEXT,
    Review_Date DATE
);

-- Cart Entity
CREATE TABLE Carts (
    CartID SERIAL PRIMARY KEY,
    UserID INT REFERENCES Users(UserID),
    Created_Date DATE
);
Usage
To use this schema, you can create the necessary tables in your database by running the provided SQL statements. This will set up the data model required to manage users, products, orders, reviews, sellers, payments, and carts on an e-commerce platform similar to Amazon.

Contributing
Contributions are welcome! If you have suggestions for improvements or find any issues, please create a pull request or open an issue on GitHub.
