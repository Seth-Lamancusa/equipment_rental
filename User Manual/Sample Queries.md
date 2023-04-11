-- Find the description of all equipment by MANUFACTURER released before YEAR:
SELECT Desc
FROM EQUIPMENT as E, SUPPLIER as S
WHERE YEAR < Year AND MANUFACTURER = S.Name

-- Give all the watering equipment and their date of their checkout (renting) from a single member (you choose how to designate the member)
SELECT EQUIPMENT.Type, CUST_ORDER.Date
FROM EQUIPMENT as E, CUST_ORDER as C
JOIN MEMBER ON Member.User_Id = C.User_Id
WHERE E.Type = Watering AND Member.Fname = 'John'

-- List all the gardening equipment and their unique identifiers with less than 2 units held by the warehouse. 
SELECT EQUIPMENT.Type, EQUIPMENT.Model_Num, EQUIPMENT.Serial_Num
FROM Equipment
WHERE EQUIPMENT.Addr = WAREHOUSE.Addr AND EQUIPMENT.City = WAREHOUSE.City
LIMIT 0,2

-- Give all the members who checked out (rented) an electric equipment delivered by DRONE and the electric equipment they checked out. 
SELECT MEMBER.Name
FROM MEMBER
WHERE MEMBER.Ssn = INV_ORDER.SSn AND INV_Order.Order_Num = CUST_ORDER.Order_NUM AND Type = 'electric'

-- Find the total number of items rented by a single member (you choose how to designate the member) 
SELECT User_Id AS User, COUNT(*) AS NumOrders
FROM CUST_ORDER
WHERE User_Id = 'USR00001'
GROUP BY User_Id;

-- Find the member who has rented the most items and the number of items rented.
SELECT User_Id AS User, COUNT(*) AS NumOrders
FROM CUST_ORDER
GROUP BY User_Id
ORDER BY COUNT(*) DESC
LIMIT 1;

-- List all orders placed by a given employee:
SELECT INV_ORDER.Order_Num
FROM INV_ORDER
JOIN EMPLOYEE ON EMPLOYEE_Ssn = INV_Order.Ssn AND EMPLOYEE.Ssn = 222117777 (Given Social)

-- List the average value of a customer order:
SELECT avg(Value)
FROM INV_ORDER
WHERE CUST_ORDER.Order_Num = INV_ORDER.Order_Num

-- List all drones and their max speed in a given warehouse:
SELECT DRONE.Model_Num, DRONE.Serial_Num, DRONE.Max-Speed
FROM DRONE
WHERE DRONE.Addr = '55 W Lane' AND DRONE.City = 'COLUMBUS'

-- This query provides a list of all member names alongside the total number of items they ordered
SELECT Fname, Lname, COUNT(*) AS Items_Ordered
FROM Member AS M, Cust_Order as C
WHERE M.User_Id = C.User_Id
GROUP BY M.User_Id
ORDER BY 1 Asc;

-- This query provides a list of member names and their email for members who have rented more equipment that the average member
SELECT Fname, Lname, Email
FROM Member AS M, Cust_Order as C
WHERE M.User_Id = C.User_Id
GROUP BY M.User_Id
HAVING COUNT(*) > (SELECT AVG(Items_Ordered)
FROM (SELECT COUNT(*) AS Items_Ordered
FROM Member AS M, Cust_Order as C
WHERE M.User_Id = C.User_Id
GROUP BY M.User_Id))
ORDER BY 1 Asc;

-- This query selects the description and type of all equipment, ordering them by popularity, as well as listing the copies that have been rented
SELECT E.Desc, E.Type, CASE WHEN O.NumOrders IS NULL THEN 0 ELSE O.NumOrders END AS NumOrders
FROM EQUIPMENT E
LEFT JOIN FOR_EQUIP F ON E.Inv_Id = F.Inv_Id
LEFT JOIN (
  SELECT Inv_Id, COUNT(*) AS NumOrders
  FROM CUST_ORDER
  GROUP BY Inv_Id
) O ON F.Inv_Id = O.Inv_Id
ORDER BY NumOrders DESC, E.Desc ASC;

-- This selects all drones and orders them by most delivers, to least. As well as the extra functionality of the NumOrders of every drone.
SELECT CUST_ORDER.Fleet_Id, COUNT(*) AS NumOrders
FROM CUST_ORDER
INNER JOIN DRONE ON CUST_ORDER.Fleet_Id = DRONE.Fleet_Id
GROUP BY CUST_ORDER.Fleet_Id;

-- This finds the most popular manufacturer in the database (i.e. the one who has had the most rented items).
SELECT Supp_Id, Name, COUNT(*) AS Num_Orders
FROM EQUIPMENT
JOIN CUST_ORDER ON EQUIPMENT.Inv_Id = CUST_ORDER.Inv_Id
JOIN SUPPLIER ON SUPPLIER.Supp_Id = EQUIPMENT.Supp_Id
GROUP BY SUPPLIER.Supp_Id
ORDER BY 3 DESC
LIMIT 1;

-- This finds the most used items in the database.
SELECT Inv_Id, SUM((julianday(Return_Date) - julianday(Order_Date))) AS Time_Rented_Days
FROM CUST_ORDER
GROUP BY CUST_ORDER.Inv_Id
ORDER BY Time_Rented DESC;

-- Provide a list of members information for members who have rented out anything by the most demanded equipment in the database.
SELECT DISTINCT M.*
FROM MEMBER M
JOIN CUST_ORDER CO ON M.User_Id = CO.User_Id
WHERE CO.Inv_Id IN (
    SELECT Inv_Id
    FROM CUST_ORDER
    GROUP BY Inv_Id
    ORDER BY COUNT(Order_Num) DESC
    LIMIT 1
); 

-- Provide a list of manufacturers who provided the items rented out by members who have rented more items than the average customer.
SELECT DISTINCT S.*
FROM SUPPLIER S
JOIN EQUIPMENT E ON S.Supp_Id = E.Supp_Id
JOIN CUST_ORDER CO ON E.Inv_Id = CO.Inv_Id
WHERE CO.User_Id IN (
    SELECT User_Id
    FROM CUST_ORDER
    GROUP BY User_Id
    HAVING COUNT(Order_Num) > (
        SELECT AVG(Rentals) as Avg_Rentals
        FROM (
            SELECT COUNT(Order_Num) as Rentals
            FROM CUST_ORDER
            GROUP BY User_Id
        )
    )
);

