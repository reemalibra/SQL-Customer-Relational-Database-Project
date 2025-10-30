**#Customer Orders Relational Database (Oracle SQL)**
Developed a relational database using Oracle SQL to organize and manage customer, order, and address infromation. Designed multiple related tables with primary and foreign key constraints to maintain data integrity and used SQL commands for table creation, data insertion, and updates. This project enhanced my understanding of relational database design, normalization, and how SQL supports real-world data organization and accuracy.

**View project on Oracle Live SQL**
https://livesql.oracle.com/ords/livesql/s/c4ii254ipfpoql82fvtc4q4rh

**SQL Script - Table Creation and Relationships**
CREATE TABLE Customers ( 
    customer_id NUMBER(10), 
    last_name VARCHAR2(50) NOT NULL, 
    first_name VARCHAR2(50) NOT NULL, 
    middle_name VARCHAR2(50), 
    suffix VARCHAR2(10), 
    phone_number VARCHAR2(15), 
    email_address VARCHAR2(100), 
    first_seen_date DATE NOT NULL, 
    CONSTRAINT Customers_customer_id_pk PRIMARY KEY (customer_id), 
    CONSTRAINT Customers_email_address_uk UNIQUE (email_address) 
);

CREATE TABLE Addresses ( 
    address_id NUMBER(10), 
    customer_id NUMBER(10), 
    address_street1 VARCHAR2(100), 
    address_street2 VARCHAR2(100), 
    address_city VARCHAR2(50), 
    address_state VARCHAR2(2), 
    address_zip VARCHAR2(10), 
    address_last_modified_date DATE DEFAULT SYSDATE NOT NULL, 
    CONSTRAINT Addresses_address_id_pk PRIMARY KEY (address_id), 
    CONSTRAINT Addresses_customer_id_fk FOREIGN KEY (customer_id) REFERENCES Customers(customer_id) 
);

CREATE TABLE Orders ( 
    order_number NUMBER(10), 
    customer_id NUMBER NOT NULL, 
    product_name VARCHAR2(100) NOT NULL, 
    list_price NUMBER(10,2) NOT NULL, 
    sell_price NUMBER(10,2) NOT NULL, 
    sell_date DATE NOT NULL, 
    ship_date DATE NOT NULL, 
    CONSTRAINT Orders_pk PRIMARY KEY (order_number), 
    CONSTRAINT Orders_customer_id_fk FOREIGN KEY (customer_id) REFERENCES Customers(customer_id) 
);

ALTER TABLE Orders 
ADD CONSTRAINT sell_date_ck CHECK (sell_date <= ship_date);

INSERT INTO Customers (customer_id, last_name, first_name, middle_name, suffix, phone_number, email_address, first_seen_date) 
VALUES (1000, 'Meisner', 'Ryder', 'Scott', 'Jr.', '8465309', 'dogs@lol.com', TO_DATE('03-09-2025', 'MM-DD-YYYY'));

INSERT INTO Customers (customer_id, last_name, first_name, middle_name, suffix, phone_number, email_address, first_seen_date) 
VALUES (1001, 'Johnson', 'Mary', NULL, NULL, '555-0102', 'mary.j@email.com', TO_DATE('2023-02-10', 'YYYY-MM-DD'));

INSERT INTO Customers (customer_id, last_name, first_name, middle_name, suffix, phone_number, email_address, first_seen_date) 
VALUES (1002, 'Brown', 'Robert', 'T', NULL, '555-0103', 'robert.brown@email.com', TO_DATE('2023-03-05', 'YYYY-MM-DD'));

INSERT INTO Customers (customer_id, last_name, first_name, middle_name, suffix, phone_number, email_address, first_seen_date) 
VALUES (1003, 'Davis', 'Sarah', NULL, 'Sr', '555-0104', 'sarah.d@email.com', TO_DATE('2023-04-12', 'YYYY-MM-DD'));

INSERT INTO Customers (customer_id, last_name, first_name, middle_name, suffix, phone_number, email_address, first_seen_date) 
VALUES (1004, 'Wilson', 'Michael', 'J', NULL, '555-0105', 'michael.w@email.com', TO_DATE('2023-05-20', 'YYYY-MM-DD'));

COMMIT;

INSERT INTO Addresses (address_id, customer_id, address_street1, address_street2, address_city, address_state, address_zip) 
VALUES (4000, 1000, '1000 Owl Street Drive', 'Apt. 206', 'Miami', 'FL', '43567');

INSERT INTO Addresses (address_id, customer_id, address_street1, address_street2, address_city, address_state, address_zip) 
VALUES (4001, 1001, '456 Oak Ave', 'Apt 4B', 'New York', 'NY', '10001');

INSERT INTO Addresses (address_id, customer_id, address_street1, address_city, address_state, address_zip) 
VALUES (4002, 1002, '789 Pine Rd', 'Chicago', 'IL', '60601');

INSERT INTO Addresses (address_id, customer_id, address_street1, address_city, address_state, address_zip) 
VALUES (4003, 1003, '101 Elm St', 'Seattle', 'WA', '98101');

INSERT INTO Addresses (address_id, customer_id, address_street1, address_city, address_state, address_zip) 
VALUES (4004, 1004, '202 Maple Dr', 'Denver', 'CO', '80202');

COMMIT;

INSERT INTO Orders (order_number, customer_id, product_name, list_price, sell_price, sell_date, ship_date) 
VALUES (2123456789, 1000, 'Cats', 20000.00, 15000.00, TO_DATE('03-09-2025', 'MM-DD-YYYY'), TO_DATE('03-10-2025', 'MM-DD-YYYY'));

INSERT INTO Orders (order_number, customer_id, product_name, list_price, sell_price, sell_date, ship_date) 
VALUES (2123456790, 1001, 'Dogs', 800.00, 750.00, TO_DATE('2023-06-11', 'YYYY-MM-DD'), TO_DATE('2023-06-13', 'YYYY-MM-DD'));

INSERT INTO Orders (order_number, customer_id, product_name, list_price, sell_price, sell_date, ship_date) 
VALUES (2123456791, 1002, 'Birds', 400.00, 350.00, TO_DATE('2023-06-12', 'YYYY-MM-DD'), TO_DATE('2023-06-14', 'YYYY-MM-DD'));

INSERT INTO Orders (order_number, customer_id, product_name, list_price, sell_price, sell_date, ship_date) 
VALUES (2123456792, 1003, 'Fish', 150.00, 130.00, TO_DATE('2023-06-13', 'YYYY-MM-DD'), TO_DATE('2023-06-15', 'YYYY-MM-DD'));

INSERT INTO Orders (order_number, customer_id, product_name, list_price, sell_price, sell_date, ship_date) 
VALUES (2123456793, 1004, 'Hamsters', 300.00, 280.00, TO_DATE('2023-06-14', 'YYYY-MM-DD'), TO_DATE('2023-06-16', 'YYYY-MM-DD'));

COMMIT;

SELECT * FROM Customers;

SELECT * FROM Addresses;

SELECT * FROM Orders;

UPDATE Customers 
SET phone_number = '846-530-9000' 
WHERE customer_id = 1000;

UPDATE Addresses 
SET address_city = 'Sunshine State' 
WHERE address_city = 'Miami';

UPDATE Orders 
SET product_name = 'LION KING' 
WHERE product_name = 'Cats';

COMMIT;


