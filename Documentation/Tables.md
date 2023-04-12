# Tables

For each table, all non-trivial functional dependencies include either full or partial dependence on the primary key, so all tables satisfy BCNF.

## CUST_ORDER:
* Primary Key: Order_Num
* Columns: Order_Num, Value, Date, Return_Date, Return_Status, Model_Num, Serial_Num, User_Id
* Foreign Keys: Model_Num, Serial_Num, User_Id
* Normal Form: BCNF

## DRONE:
* Primary Key: Model_Num, Serial_Num
* Columns: Model_Num, Serial_Num, Year, Desc, Fleet_Id, Weight_Cap, Volume_Cap, Dist_Auth, Max_Speed, Status, Addr, City, Supp_Id
* Foreign Keys: Addr, City, Supp_Id
* Normal Form: BCNF

## EMPLOYEE:
* Primary Key: Ssn
* Columns: Ssn, Fname, Lname, Addr, Phone, Email, Salary
* Foreign Keys: None
* Normal Form: BCNF

## EQUIPMENT:
* Primary Key: Model_Num, Serial_Num
* Columns: Model_Num, Serial_Num, Year, Desc, Warr_Exp, Inv_Id, Type, Weight, Arrival_Date, Size, Addr, City, Supp_Id
* Foreign Keys: Addr, City, Supp_Id
* Normal Form: BCNF

## FOR_DRONE:
* Primary Key: Order_Num, Model_Num, Serial_Num
* Columns: Order_Num, Model_Num, Serial_Num
* Foreign Keys: Order_Num, Model_Num, Serial_Num
* Normal Form: BCNF

## FOR_EQUIP:
* Primary Key: Order_Num, Model_Num, Serial_Num
* Columns: Order_Num, Model_Num, Serial_Num
* Foreign Keys: Order_Num, Model_Num, Serial_Num
* Normal Form: BCNF

## INV_ORDER:
* Primary Key: Order_Num
* Columns: Order_Num, Value, Order_Date, Est_DOA, Num_Items, Type, Ssn
* Foreign Keys: Ssn
* Normal Form: BCNF

## MEMBER:
* Primary Key: User_Id
* Columns: User_Id, Fname, Lname, Addr, Phone, Email, Start_Date, Credit_Card
* Foreign Keys: None
* Normal Form: BCNF

## REVIEW:
* Primary Key: Review_Id
* Columns: Review_Id, Rating, Text, User_Id, Model_Num, Serial_Num
* Foreign Keys: User_Id, Model_Num, Serial_Num
* Normal Form: BCNF

## SUPPLIER:
* Primary Key: Supp_Id
* Columns: Supp_Id, Name, Addr, City
* Foreign Keys: None
* Normal Form: BCNF

## WAREHOUSE:
* Primary Key: Addr, City
* Columns: Addr, City, Mgr_Fname, Mgr_Lname, Phone, Equip_Cap, Drone_Cap
* Foreign Keys: None
* Normal Form: BCNF
