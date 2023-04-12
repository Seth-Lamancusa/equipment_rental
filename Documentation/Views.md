# Views

## Members and total spent

This view displays each member and the total amount they have spent on rentals since joining, useful for identifying the customers who are responsible for the businesses revenue. The view can be created using the following SQL:

	CREATE VIEW Cust_Orders_Value AS
	SELECT M.User_Id, Fname, Lname, Start_Date, SUM(Value) "Total_Orders_Value"
	FROM MEMBER AS M, CUST_ORDER AS O
	WHERE M.User_Id = O.User_Id
	GROUP BY M.User_Id;

The query implements the following relational algebra: $$\text{Cust\_Orders\_Value}\leftarrow\gamma_{\text{User\_Id},\text{Fname},\text{Lname},\text{Start\_Date},\text{SUM(Value)}}(\text{MEMBER}\bowtie_{\text{User\_Id}=\text{User\_Id}}\text{CUST\_ORDER})$$

Following are several line of example output.
	
|	User_Id   |  Fname|	Lname	|	Start_Date	|	Total_Orders_Value|
--------------|-------|---------|---------------|--------------------
|	USR00001|	John|	Doe		|	2022-01-01	|	3000|
|	USR00002|	Jane|	Smith	|	2022-01-02	|	2000|
|	USR00003|	Bob	|	Johnson	|	2022-01-03	|	500|
|	USR00004|	Alice|	Williams|	2022-01-04	|	1000|
|	USR00005|	Tom	|	Brown	|	2022-01-05	|	750|

## Drones, total orders, and manufacturer

This view displays each drone, the total number of orders it has delivered, its description, and its manufacturer, useful for tracking drone use and predicting when drones will need to be ordered. The view can be created using the following SQL:

	CREATE VIEW Drone_Deliveries AS
	SELECT D.Model_Num, D.Serial_Num, D.Desc, S.Name, SUM(I.Num_Items) AS Orders_Delivered
	FROM DRONE AS D
		JOIN FOR_DRONE AS F ON D.Fleet_Id = F.Fleet_Id
		JOIN INV_ORDER AS I ON F.Order_Num = I.Order_Num
		JOIN SUPPLIER AS S ON D.Supp_Id = S.Supp_Id
	GROUP BY D.Model_Num, D.Serial_Num, S.Name, D.Desc;

The query implements the following relational algebra: $$\text{Drone\_Deliveries}\leftarrow\pi_{D.\text{Model\_Num},D.\text{Serial\_Num},D.\text{Desc},S.\text{Name},\text{SUM(I.Num\_Items)}\to\text{Orders\_Delivered}}\left(\sigma_{D.\text{Supp\_Id}=S.\text{Supp\_Id}\land D.\text{Fleet\_Id}=F.\text{Fleet\_Id}\land F.\text{Order\_Num}=I.\text{Order\_Num}}(D\bowtie F\bowtie I\bowtie S)\right)$$

Following are several lines of example output.

|Model_Num	|Serial_Num	|Desc								|Name			|Orders_Delivered|
|-----------|-----------|-----------------------------------|---------------|--------|
|M1000000	|S0000021	|Small drone for personal use		|ABC Company		|3|
|M1100000	|S0000030	|Small drone for surveying			|ABC Company		|2|
|M1200000	|S0000031	|Medium drone for aerial photography	|XYZ Corporation	|4|
|M1300000	|S0000032	|Large drone for military use		|Acme Inc.		|3|
|M1400000	|S0000033	|Small drone for personal use		|Acme Inc.		|6|