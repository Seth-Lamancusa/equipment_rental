# Tables

## CUST_ORDER
Represents orders placed by customers.
* Order_Num: Unique identifier for each order (char, 8 characters, primary key, not null)
* Value: Total monetary value of the order, used for billing (int)
* Date: Date the order was placed, used for record-keeping (date)
* Return_Date: Date the order was returned, used for monitoring(date)
* Return_Status: Indicates whether the order was returned or not (int, 1 if returned, 0 if not)
* Model_Num: Model number of the rented equipment (char, 8 characters, not null, foreign key)
* Serial_Num: Serial number of the rented equipment (char, 8 characters, not null, foreign key)
* User_Id: User ID of the customer who placed the order (char, 8 characters, not null, foreign key)

## DRONE 
Represents drones in the fleet.
* Model_Num: Unique identifier for each drone model (char, 8 characters, primary key, not null)
* Serial_Num: Unique identifier for each individual drone (char, 8 characters, primary key, not null)
* Year: Production year, used for tracking the age of drones (char, 4 characters, not null)
* Desc: Description of the drone's (varchar, 50 characters)
* Fleet_Id: Identifier for the drone's fleet (char, 8 characters, not null)
* Weight_Cap: Maximum weight the drone can carry, for delivery planning (int)
* Volume_Cap: Maximum volume the drone can carry, for delivery planning (int)
* Dist_Auth: Authorized distance the drone can travel, for delivery planning (varchar, 4 characters)
* Max_Speed: Maximum speed the drone can achiev, for delivery planning (int)
* Status: Indicates if the drone is in use or discontinued (int, 1 if in use, 0 if discontinued, not null)
* Addr: Warehouse address where the drone is stored (varchar, 30 characters, not null, foreign key)
* City: Warehouse city where the drone is stored (varchar, 30 characters, not null, foreign key)
* Supp_Id: Identifier of the supplier who provided the drone (char, 8 characters, not null, foreign key)

## EMPLOYEE
Represents company employee.
* Ssn: Unique identifier for each employee (char, 9 characters, primary key, not null)
* Fname: Employee's first name (varchar, 15 characters, not null)
* Lname: Employee's last name (varchar, 15 characters, not null)
* Addr: Employee's address (varchar, 30 characters)
* Phone: Employee's phone number (char, 10 characters)
* Email: Employee's email address (varchar, 40 characters)
* Salary: Employee's salary, used for payroll (int)

## EQUIPMENT
Represents equipment in the inventory available for rental.
* Model_Num: Unique identifier for the equipment model (char, 8 characters, primary key, not null)
* Serial_Num: Unique identifier for each individual piece of equipment (char, 8 characters, primary key, not null)
* Year: Production year, used for tracking equipment age (char, 4 characters)
* Desc: Description of the equipment (varchar, 50 characters)
* Warr_Exp: Warranty expiration date, used to track equipment warranty (date)
* Inv_Id: Inventory ID, used to manage inventory (char, 8 characters, not null)
* Type: Equipment type, for categorizing equipment (varchar, 15 characters)
* Weight: Weight of the equipment, used for planning (int)
* Arrival_Date: Date the equipment arrived at the warehouse, used for record keeping (date)
* Size: Size category of the equipment, used for inventory management (varchar, 2 characters)
* Addr: Warehouse address where the equipment is stored (varchar, 30 characters, not null, foreign key)
* City: Warehouse city where the equipment is stored (varchar, 30 characters, not null, foreign key)
* Supp_Id: Identifier of the supplier who provided the equipment (char, 8 characters, not null, foreign key)

## FOR_DRONE
Represents inventory orders for drones.
* Order_Num: Unique identifier for each inventory order (char, 8 characters, not null, foreign key)
* Model_Num: Model number of the ordered drone (char, 8 characters, not null, foreign key)
* Serial_Num: Serial number of the ordered drone (char, 8 characters, not null, foreign key)

## FOR_EQUIP
Represents inventory orders for equipment.
* Order_Num: Unique identifier for each inventory order (char, 8 characters, not null, foreign key)
* Model_Num: Model number of the ordered equipment (char, 8 characters, not null, foreign key)
* Serial_Num: Serial number of the ordered equipment (char, 8 characters, not null, foreign key)

## INV_ORDER
Represents inventory orders placed by employees.
* Order_Num: Unique identifier for each inventory order (char, 8 characters, primary key, not null)
* Value: Total monetary value of the order, used for tracking costs (int)
* Order_Date: Date the order was placed, used for record keeping (date)
* Est_DOA: Estimated date of arrival for the order, used for planning (date)
* Num_Items: Number of items in the order, used for inventory management (int)
* Type: Type of items in the order, for categorizing items (varchar, 15 characters)
* Ssn: Social security number of the employee who placed the order (char, 9 characters, not null, foreign key)

## MEMBER
Represents customers who are members of the rental service.
* User_Id: Unique identifier for each customer (char, 8 characters, primary key, not null)
* Fname: Customer's first name (varchar, 15 characters, not null)
* Lname: Customer's last name (varchar, 15 characters, not null)
* Addr: Customer's address (varchar, 30 characters)
* Phone: Customer's phone number (char, 10 characters)
* Email: Customer's email address (varchar, 40 characters)
* Start_Date: Date the customer became a member, used for record keeping (date)
* Credit_Card: Customer's credit card number, used for billing (char, 16 characters)

## REVIEW
Represents customer reviews of rented equipment.
* Review_Id: Unique identifier for each review (char, 8 characters, primary key, not null)
* Rating: Rating given by the customer (char, 1 character)
* Text: Text in customer's review (varchar, 255 characters)
* User_Id: Identifier of the customer who wrote the review (char, 8 characters, not null, foreign key)
* Model_Num: Model number of the reviewed equipment (char, 8 characters, foreign key)
* Serial_Num: Serial number of the reviewed equipment (char, 8 characters, foreign key)

## SUPPLIER
Represents suppliers that provide equipment and drones to the company.
* Supp_Id: Unique identifier for each supplier (char, 8 characters, primary key, not null)
* Name: Supplier's name (varchar, 30 characters, not null)
* Addr: Supplier's address (varchar, 30 characters)
* City: Supplier's city (varchar, 30 characters)

## WAREHOUSE
Represents warehouses where equipment and drones are stored.
* Addr: Warehouse address (varchar, 30 characters, primary key, not null)
* City: Warehouse city (varchar, 30 characters, primary key, not null)
* Mgr_Fname: First name of the warehouse manager (varchar, 15 characters)
* Mgr_Lname: Last name of the warehouse manager (varchar, 15 characters)
* Phone: Warehouse contact phone number (char, 10 characters)
* Equip_Cap: Maximum capacity for storing equipment, used for inventory management (int)
* Drone_Cap: Maximum capacity for storing drones, used for inventory management (int)
