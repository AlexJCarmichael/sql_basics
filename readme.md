How many users are there? 50 ```select count(*) from users;```

What are the 5 most expensive items?
`25    Small Cotton Gloves  Automotive, Shoes & Beauty  Multi-layered modular service-desk  9984`
`83    Small Wooden Computer  Health  Re-engineered fault-tolerant adapter  9859`
`100   Awesome Granite Pants  Toys & Books  Upgradable 24/7 access  9790`
`40    Sleek Wooden Hat  Music & Baby  Quality-focused heuristic info-mediaries  9390`
`60    Ergonomic Steel Car  Books & Outdoors  Enterprise-wide secondary firmware  9341`
`select * from items order by price desc limit 5;`

What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
`76    Ergonomic Granite Chair  Books  De-engineered bi-directional portal  1496`
`select * from items where category = "Books" order by price limit 1;`
`76    Ergonomic Granite Chair  Books  De-engineered bi-directional portal  1496`
`select * from items where category like "%book%" order by price limit 1;`

Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
`Corrine  Little         6439 Zetta Hills`
`select first_name, last_name, street from addresses join users  on users.id = addresses.user_id where user_id and street like "%6439 Zetta Hills%";`

```firs  last_name      stre
----  -------------  ----
Corrine  Little         6439 Zetta Hills
Corrine  Little         54369 Wolff Forges
```
`select first_name, last_name, street from addresses join users  on users.id = addresses.user_id where user_id in (select user_id from addresses where street like "%6439 Zetta Hills%");`

Correct Virginie Mitchell's address to "New York, NY, 10108".

```firs  last_name      stre  city  stat
----  -------------  ----  ----  ----
Virginie  Mitchell       12263 Jake Crossing  New York  NY
Virginie  Mitchell       83221 Mafalda Canyon  Bahringerland  WY
```
###Code
update addresses
...> set city = 'New York', zip = '10108'
...> where street = '12263 Jake Crossing' and user_id = "40";
###End of code

How much would it cost to buy one of each tool? 46477
`select sum(price) from items where category like "%tools%";`

How many total items did we sell? 2125
`select sum(quantity) from orders;`

How much was spent on books? 1081352
`select sum (items.price * orders.quantity) from items join orders on orders.item_id  = items.id where category like "%books%";`

Simulate buying an item by inserting a User for yourself and an Order for that User.
`insert into users values (55,"Dane", "Carmichael","me@me.me");`
`insert into orders (user_id, item_id, quantity) values (55, 1, 5);`
