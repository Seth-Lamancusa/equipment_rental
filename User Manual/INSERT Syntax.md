# INSERT Syntax

There are no specific order restrictions for adding a member, drone, equipment, employee, supplier, or warehouse record. Records can be inserted into these tables without any dependencies.

To add a rental, you must first have a member and equipment in your system. The member's user ID and the equipment's inventory ID are both foreign keys in the rental table. Therefore, you must first insert a member and an equipment record before inserting a rental record.

To add a drone order, you must first have an inventory order and a for_drone record. The inventory order record contains the order number and the number of items, while the for_drone record contains the order number and the fleet ID. Therefore, you must first insert an inventory order record and a for_drone record before inserting a drone order record.

To add an inventory order, you must first have an employee record. The employee's SSN is a foreign key in the inventory order table. Therefore, you must first insert an employee record before inserting an inventory order record.

To add a for_equipment record, you must first have an inventory order record. The inventory order number is a foreign key in the for_equipment table. Therefore, you must first insert an inventory order record before inserting a for_equipment record.

To add a review, you must first have a member and an equipment record. The member's user ID and the equipment's inventory ID are both foreign keys in the review table. Therefore, you must first insert a member and an equipment record before inserting a review record.

## Examples

    INSERT INTO CUST_ORDER (Order_Num, Value, Order_Date, Return_date, Return_Status, Inv_Id, Fleet_Id, User_Id) VALUES ('COR00001', 1500, '2022-01-01', '2022-01-05', 1, 'INV00001', 'F0000001', 'USR00001');

    INSERT INTO DRONE (Fleet_Id, Model_Num, Serial_Num, Year, "Desc", Warr_Exp, Weight_Cap, Volume_Cap, Dist_Auth, Max_Speed, Status, Addr, City, Supp_Id) VALUES ('F0000001', 'M1000000', 'S0000021', '2022', 'Small drone for personal use', NULL, 2, 4, '100', 80, 1, '456 Elm St', 'Othertown', 'SUP00001');

    INSERT INTO EMPLOYEE (Ssn, Fname, Lname, Addr, Phone, Email, Salary) VALUES ('123456789', 'John', 'Doe', '123 Main St', '1235551234', 'jdoe@email.com', 60000);

    INSERT INTO EQUIPMENT (Inv_Id, Model_Num, Serial_Num, Year, "Desc", Warr_Exp, Type, Weight, Arrival_Date, Size, Addr, City, Supp_Id) VALUES ('INV00001', 'MDL00001', 'SER00001', '2021', 'Laptop', '2025-03-10', 'Electronic', 5, '2021-03-01', 'M', '123 Main St', 'Anytown', 'SUP00001');

    INSERT INTO FOR_DRONE (Order_Num, Fleet_Id) VALUES ('ORD00001', 'F0000001');

    INSERT INTO FOR_EQUIP (Order_Num, Inv_Id) VALUES ('ORD00021', 'INV00001');

    INSERT INTO INV_ORDER (Order_Num, Value, Order_Date, Est_DOA, Num_Items, Type, Ssn) VALUES ('ORD00001', 500, '2022-01-01', '2022-01-15', 3, 'Drone', '123456789');

    INSERT INTO MEMBER (User_Id, Fname, Lname, Addr, Phone, Email, Start_Date, Credit_Card) VALUES ('USR00001', 'John', 'Doe', '123 Main St.', '1234567890', 'john.doe@example.com', '2022-01-01', '1234567890123456');

    INSERT INTO REVIEW (Review_Id, Rating, Text, User_Id, Inv_Id) VALUES ('REV00001', 5, 'This equipment is amazing!', 'USR00001', 'INV00001');

    INSERT INTO SUPPLIER (Supp_Id, Name, Addr, City) VALUES ('SUP00001', 'ABC Company', '123 Main St', 'New York');

    INSERT INTO WAREHOUSE (Addr, City, Mgr_Fname, Mgr_Lname, Phone, Equip_Cap, Drone_Cap) VALUES ('123 Main St', 'New York', 'John', 'Doe', '1234567890', 50, 20);

