View 1: list the members and the total value of all of the orders they have placed since they joined.
Code:
CREATE VIEW Cust_Orders_Value AS
SELECT M.User_Id, Fname, Lname, Start_Date, SUM(Value) "Total_Orders_Value"
FROM MEMBER AS M, CUST_ORDER AS O
WHERE M.User_Id = O.User_Id
GROUP BY M.User_Id;


View 2: list the drones and the total number of orders they have delievered and what company they were manufactured by
Code:
CREATE VIEW Drone_Deliveries AS
SELECT D.Model_Num, D.Serial_Num, Desc, Name, Sum(Num_Items) "Orders_Delivered"
FROM DRONE AS D, FOR_DRONE AS F, INV_ORDER AS I, SUPPLIER AS S
WHERE   D.Supp_Id = S.Supp_Id
	D.Model_Num = F.Model_Num 
	AND D.Serial_Num = F.Serial_Num
	AND F.Order_Num = I.Order_Num
GROUP BY D.Model_Num, D.Serial_Num;

