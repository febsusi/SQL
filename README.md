# SQL
This repository to showcase SQL skills.

- A customer complained for her failed order to our customer service, and the customer service ask data team to provide the order information (price, order_id, product name, when the product is bought). The customer only informs the CS her email id. Please write the syntax to get the information about the failed order.

 
SELECT

	a.name, a.price, b.order_id

FROM

	products a LEFT JOIN order_items b 
    
	    ON a.id = b.product_id
    
	LEFT JOIN orders d
    
	    ON d.id = b.order_id
	
    LEFT JOIN users c
	
        ON c.id = d.user_id

WHERE
	
    c.email =’email_id_cust’ AND d.status = ‘Failed’

- To get the top 5 of merchants in this month (May) based on the highest successful orders (successful can be seen by order status)


SELECT TOP 5

	a.merchant_name

FROM

	merchants a LEFT JOIN orders b 
    
        ON a.admin_id = b.user_id
	
    LEFT JOIN  order_items c
	
        ON b.id = c.order_id

WHERE
	
    b.created_at= ‘May’ and b.status=’Success’

GROUP BY 
	
    a.merchant_name

ORDER BY 

    SUM(c.quantity) DESC

- List of customers with average money spent per order is above Rp 1 million
 

SELECT 

    a.full_name, a.id, AVG(b.quantity*c.price) as Average_Amount

FROM

	Users a INNER JOIN orders d

    ON a.id = d.user_id JOIN order_items b
	
    ON d.id = b.order_id JOIN products c
	
    ON b.product_id = c.id

GROUP BY

    a.full_name, a.id 

HAVING
	
    AVG(b.quantity*c.price) > 1000000 

- Customers’ most purchased products


SELECT TOP 1
    
    a.name, SUM(b.quantity) as Total_Quantity
    
FROM
    
    products a 

JOIN order_items b 

    ON a. id = b.product_id
    
GROUP BY 
    
    a.name

ORDER BY 
    
    SUM(b.quantity) DESC


