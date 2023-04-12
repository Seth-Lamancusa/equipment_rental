# Indexes

# CUST_ORDER: Date

The following code generates an index on the CUST_ORDER table on the Date column in order to speed up queries which filter orders by date. Such queries would be frequent for the purpose of analyzing trends in purchase customer, volume, and value.

    CREATE INDEX idx_cust_order_date ON CUST_ORDER(Date);

# REVIEW: Rating

The following code generates an index on the REVIEW table on the Rating column in order to speed up queries which filter by rating. Such queries would be frequent for the purpose of analyzing customer satisfaction or displaying ratings to a user.

    CREATE INDEX idx_review_rating ON REVIEW(Rating);

# EQUIPMENT: Year

The following code generates an index on the EQUIPMENT table on the Year column in order to speed up queries which filter by Year. Such queries would be frequent for the purpose of equipment maintenence and estimation of the need for new inventory.

    CREATE INDEX idx_equipment_year ON EQUIPMENT(Year);
