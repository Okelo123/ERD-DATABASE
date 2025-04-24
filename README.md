📘 E-Commerce ERD Documentation
 Overview
This documentation describes the entity-relationship diagram (ERD) for an e-commerce database system. It outlines all major entities, their attributes, and relationships to support operations like user management, product listing, order processing, and merchant tracking.

 Entities & Attributes
1. public.users
Represents users who interact with the system.


Attribute	Data Type	Description
id	int	Primary Key
full_name	varchar	Full name of the user
created_at	timestamp	Account creation time
country_code	int	FK → countries.code
2. public.countries
Stores country and continent information.


Attribute	Data Type	Description
code	int	Primary Key
name	varchar	Country name
continent_name	varchar	Continent the country belongs to
3. ecommerce.merchants
Holds information about sellers/merchants on the platform.


Attribute	Data Type	Description
id	int	Composite PK with country_code
country_code	int	Composite PK, FK → countries.code
merchant_name	varchar	Merchant business name
created_at	varchar	Merchant registration date
admin_id	int	Admin responsible for this merchant
4. ecommerce.merchant_periods
Stores availability periods for merchants.


Attribute	Data Type	Description
id	int	Primary Key
merchant_id	int	FK → merchants.id
country_code	int	FK → merchants.country_code
start_date	datetime	Period start
end_date	datetime	Period end
5. ecommerce.products
Represents products listed on the platform.


Attribute	Data Type	Description
id	int	Primary Key
name	varchar	Product name
merchant_id	int	FK → merchants.id
price	int	Price in local currency
status	enum	Product availability status
created_at	datetime	Product creation timestamp
Enum ecommerce.products_status:

in_stock

out_of_stock

running_low (less than 20 items left)

6. ecommerce.product_tags
Supports tagging for product categorization and searchability.


Attribute	Data Type	Description
id	int	Primary Key
name	varchar	Tag label
7. ecommerce.orders
Captures details of customer orders.


Attribute	Data Type	Description
id	int	Primary Key
user_id	int	FK → users.id
status	varchar	e.g., pending, completed
created_at	varchar	Order placement timestamp
8. ecommerce.order_items
Connects products to orders, allowing for multiple items per order.


Attribute	Data Type	Description
order_id	int	FK → orders.id
product_id	int	FK → products.id
quantity	int	Units of the product
