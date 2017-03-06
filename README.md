# How many users are there?#
    select count(*) from users;
        50

# What are the 5 most expensive items?#
    select * from items order by items.price asc;
        60|Ergonomic Steel Car|Books & Outdoors|Enterprise-wide secondary firmware|9341
        40|Sleek Wooden Hat|Music & Baby|Quality-focused heuristic info-mediaries|9390
        100|Awesome Granite Pants|Toys & Books|Upgradable 24/7 access|9790
        83|Small Wooden Computer|Health|Re-engineered fault-tolerant adapter|9859
        25|Small Cotton Gloves|Automotive, Shoes & Beauty|Multi-layered modular service-desk|9984

# What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)#
    select * from items where category like '%book%' order by price asc limit 1;
        76|Ergonomic Granite Chair|Books|De-engineered bi-directional portal|1496
# Does that change for "category is exactly 'book'" versus "category contains 'book'"?#
    No.

# Who lives at "6439 Zetta Hills, Willmouth, WY"? #
    select * from addresses where street='6439 Zetta Hills';
        43|40|6439 Zetta Hills|Willmouth|WY|15029

    select first_name, last_name from users where id=40;
        Corrine|Little
# Do they have another address? #
        select street from addresses where user_id=40;
            6439 Zetta Hills
            54369 Wolff Forges

# Correct Virginie Mitchell's address to "New York, NY, 10108". #
    select id from users where first_name='Virginie';
        39
    update addresses set city='New York', state='NY', zip='10108' where id=41;
        41|39|12263 Jake Crossing|New York|NY|10108

# How much would it cost to buy one of each tool? #
    select sum(price) from items where category like '%tools%';
        46477

# How many total items did we sell? #
    select sum(quantity) from orders;
        2125
# How much was spent on books? #
    select sum((items.price * orders.quantity)) as total from orders join items on items.id = orders.item_id where items.category like '%Books%';
        1081352

# Simulate buying an item by inserting a User for yourself and an Order for that User. #
    insert into users (id, first_name, last_name, email) values ('51', 'Jennifer', 'Bonner', 'jenniferbonner12@gmail.com');
        51|Jennifer|Bonner|jenniferbonner12@gmail.com

    sqlite> insert into orders(user_id, item_id, quantity, created_at) values('51', '47', '100', '2015-02-09 00:40:31.27227');
        378|51|47|100|2015-02-09 00:40:31.27227