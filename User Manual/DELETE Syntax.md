# DELETE Syntax

To delete a record from the EQUIPMENT table, any associated records in the REVIEW and FOR_EQUIP tables should be deleted first.

To delete a record from the DRONE table, any associated records in the FOR_DRONE table should be deleted first.

To delete a record from the CUST_ORDER table, any associated records in the FOR_EQUIP and FOR_DRONE tables should be deleted first.

To delete a record from the INV_ORDER table, any associated records in the FOR_EQUIP and FOR_DRONE tables should be deleted first.

To delete a record from the REVIEW table, no other dependencies need to be considered.

To delete a record from the MEMBER table, any associated records in the CUST_ORDER and REVIEW tables should be deleted first.

To delete a record from the EMPLOYEE table, any associated records in the INV_ORDER table should be deleted first.

To delete a record from the SUPPLIER table, any associated records in the EQUIPMENT table should be deleted first.

To delete a record from the WAREHOUSE table, any associated records in the DRONE and EQUIPMENT tables should be deleted first.


## Examples

    DELETE FROM MEMBER WHERE User_Id = 'USR00001';

    DELETE FROM DRONE WHERE Fleet_Id = 'F0000001';

    DELETE FROM EQUIPMENT WHERE Inv_Id = 'INV00001';

    DELETE FROM CUST_ORDER WHERE Order_Num = 'COR00001';

    DELETE FROM EMPLOYEE WHERE Ssn = '123456789';

    DELETE FROM WAREHOUSE WHERE Addr = '123 Main St' AND City = 'New York';

    DELETE FROM REVIEW WHERE Review_Id = 'REV00001';

    DELETE FROM SUPPLIER WHERE Supp_Id = 'SUP00001';
