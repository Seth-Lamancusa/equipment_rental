# Transactions

## Remove bad equipment

This transaction deletes records from the EQUIPMENT table where the associated Inv_Id has a warranty expiration date after '2026-01-01' and a rating of 1.

    BEGIN TRANSACTION RemoveBadEquipment;

    -- Savepoint for rollback
    SAVEPOINT before_deletion;

    DELETE FROM EQUIPMENT
    WHERE Inv_Id IN (
        SELECT REVIEW.Inv_Id AS BadEquip
        FROM EQUIPMENT
        JOIN REVIEW ON REVIEW.Inv_Id = EQUIPMENT.Inv_Id
        WHERE Warr_Exp > '2026-01-01' AND Rating = 1
    );

    -- Error handling
    -- IF error THEN GO TO UNDO; END IF (replace this comment with the specific error handling condition for your SQL environment)

    -- UNDO:
    ROLLBACK TO before_deletion;

    -- COMMIT (if no error occurred)
    COMMIT;

    END TRANSACTION;


## Add popular equipment order

This transaction inserts a new record into INV_ORDER with a new order number, a value of $500, today's date as the order date, an estimated delivery date 2 weeks from now, 5 items in the order, the most popular equipment type, and an employee's Social Security Number.

    BEGIN TRANSACTION Order_PopularEquip;

    -- Savepoint for rollback
    SAVEPOINT before_insertion;

    INSERT INTO INV_ORDER
        (Order_Num, Value, Order_date, Est_DOA, Num_Items, Type, Ssn)
    VALUES (
        -- Selects maximum order number + 1, to give us the next unused order number.
        (SELECT 'ORD' || printf("%05d", substr(MAX(Order_Num), 4) + 1) AS OrderNum FROM INV_ORDER),
        -- Value of $500, will have to manually put in for each case as value changes
        500,
        -- Inserts today's date as the order date
        DATE('now'),
        -- Estimated DOA 2 weeks from now
        DATE('now', '+14 day'),
        -- Order 5 items
        5,
        -- Selects the most popular equipment type
        (
            SELECT Type
            FROM (
                SELECT Type, SUM((julianday(Return_Date) - julianday(Order_Date))) AS Time_Rented
                FROM CUST_ORDER
                JOIN EQUIPMENT ON CUST_ORDER.Inv_Id = EQUIPMENT.Inv_Id
                GROUP BY Type
                ORDER BY Time_Rented DESC
                LIMIT 1
            ) subquery
        ),
        -- Employee will have to manually enter their ssn when running the transaction. Arbitrary ssn picked here.
        '123456789'
    );

    -- UNDO:
    ROLLBACK TO before_insertion;

    -- COMMIT (if no error occurred)
    COMMIT;

    END TRANSACTION;

## Add employee

This transaction adds a new employee to EMPLOYEE and updates the salaries of existing employees accordingly, so that when a new employee is added salaries will always be updated if they are less than 30000.

    BEGIN TRANSACTION Update_Salary;

    -- Savepoint for rollback
    SAVEPOINT before_update;

    INSERT INTO EMPLOYEE
        VALUES ('123099990', 'Joe', 'Smith', '25 Valley Place', '6147362535', 'Joe@gmail.com', 30000);
    -- IF error THEN GO TO UNDO; END IF (replace this comment with the specific error handling condition for your SQL environment)

    UPDATE EMPLOYEE
    SET Salary = Salary + 1000
    WHERE Salary <= 30000 AND EMPLOYEE.Ssn != '123099990';
    -- IF error THEN GO TO UNDO; END IF (replace this comment with the specific error handling condition for your SQL environment)

    -- UNDO:
    ROLLBACK TO before_update;

    -- COMMIT (if no error occurred)
    COMMIT;

    END TRANSACTION;
