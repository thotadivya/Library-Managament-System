# Library-Managament-System

# Project Overview
This Library Management System (LMS) is a simple Java-based application built using Swing for the Graphical User Interface (GUI) and MySQL as the database. It is designed to manage library operations such as adding new books, adding new borrowers, borrowing books, returning books, searching for books, and viewing the borrowing history. The system is modular, with each responsibility divided into separate classes for better organization and maintenance.

# Features
# Add New Book:

Allows the librarian to add a new book to the system by entering the book's ISBN, title, author, genre, and publication year.
The book is stored in the books table in the MySQL database.
# Add New Borrower:

Allows the librarian to add a new borrower by entering the borrower's name, email, and contact number.
The borrower is stored in the borrowers table in the MySQL database.
# Borrow a Book:

A borrower can borrow a book by providing their borrower ID and the ISBN of the book.
Before borrowing, the system checks the book_copies table to ensure the book is available for borrowing.
A new borrowing transaction is created in the borrowing_transactions table, and the availability of the book is updated.
# Return a Book:

The borrower can return a book by entering the transaction ID.
The system updates the return date in the borrowing_transactions table and marks the book as available in the book_copies table.
# Search for Books:

Allows the librarian or borrower to search for books by entering keywords such as title, author, genre, or publication year.
The system retrieves matching books from the books table and displays their availability status.
# View Borrowing History:

Allows the librarian or borrower to view the borrowing history for a specific borrower ID.
Displays details such as ISBN, borrowing date, and return date (if returned).
# Technologies Used
Java: Core programming language for building the application logic and GUI.
Swing: Java framework used for building desktop GUI components such as buttons, text fields, and panels.
JDBC (Java Database Connectivity): API used to interact with the MySQL database and execute SQL queries.
MySQL: Relational database that stores data about books, borrowers, and borrowing transactions.
SQL: Used to perform CRUD (Create, Read, Update, Delete) operations on the MySQL database.
# Database Design
The application uses a MySQL database with the following tables:

books:

Stores information about the books in the library, including:
isbn: Unique identifier for the book.
title: Title of the book.
author: Author of the book.
genre: Genre of the book.
publication_year: Year the book was published.
borrowers:

Stores information about the borrowers, including:
borrower_id: Unique ID for each borrower.
name: Name of the borrower.
email: Email of the borrower.
contact_number: Contact number of the borrower.
borrowing_transactions:

Stores borrowing and returning transactions:
transaction_id: Unique ID for each transaction.
borrower_id: ID of the borrower.
isbn: ISBN of the book borrowed.
borrowing_date: Date the book was borrowed.
return_date: Date the book was returned.
book_copies:

Tracks the availability of books:
isbn: ISBN of the book.
serial_number: Serial number for each copy of the book.
availability: Boolean value indicating whether the book is available for borrowing.
# Application Flow
Start the Application:

When the application starts, it connects to the MySQL database using JDBC.
The main GUI is displayed with buttons for different operations (Add Book, Borrow Book, etc.).
# User Interactions:

When a button is clicked, the corresponding method is called:
For example, clicking "Add New Book" opens a form to input book details, and the data is inserted into the books table upon submission.
Database Operations:

The application interacts with the MySQL database using prepared SQL statements.
Operations like adding a book, searching for books, borrowing, and returning are handled via CRUD operations (Create, Read, Update, Delete).
Result Handling:

After each operation (e.g., borrowing a book), a confirmation message is shown to the user using JOptionPane.
If an operation fails (e.g., a book is unavailable for borrowing), an error message is displayed.
Code Structure
# Main.java:

This is the entry point of the application.
It sets up the main GUI and connects buttons to event listeners that trigger the respective CRUD operations.
# DatabaseConnection.java:

Handles connecting to the MySQL database using JDBC.
This class establishes and manages the database connection.
# BookOperations.java:

Contains methods to handle book-related operations such as adding a new book and searching for books in the database.
# BorrowerOperations.java:

Manages operations related to borrowers, such as adding new borrowers to the system.
# TransactionOperations.java:

Handles borrowing and returning books.
Contains logic for recording borrowing transactions and updating book availability.
# Setup Instructions
Clone the repository:

bash
Copy code
git clone <url>
Install MySQL:

Install MySQL on your machine and create a database named LMS_FDB.
Create the necessary tables:

sql
Copy code
CREATE TABLE books (
    isbn VARCHAR(13) PRIMARY KEY,
    title VARCHAR(100),
    author VARCHAR(100),
    genre VARCHAR(50),
    publication_year INT
);

CREATE TABLE borrowers (
    borrower_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    contact_number VARCHAR(15)
);

CREATE TABLE borrowing_transactions (
    transaction_id INT AUTO_INCREMENT PRIMARY KEY,
    borrower_id INT,
    isbn VARCHAR(13),
    borrowing_date DATE,
    return_date DATE,
    FOREIGN KEY (borrower_id) REFERENCES borrowers(borrower_id),
    FOREIGN KEY (isbn) REFERENCES books(isbn)
);

CREATE TABLE book_copies (
    isbn VARCHAR(13),
    serial_number VARCHAR(20) PRIMARY KEY,
    availability BOOLEAN,
    FOREIGN KEY (isbn) REFERENCES books(isbn)
);
# Configure Database Credentials:

Modify the DatabaseConnection.java file to update the database URL, username, and password.
Run the Application:

Compile and run the Main.java file using any Java IDE (e.g., IntelliJ IDEA, Eclipse).
This project is a simple and effective way to manage a library's basic operations through a GUI. Feel free to explore and extend this project for more advanced features!

