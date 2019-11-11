Users table -


http://localhost/store/api/users/create.php?ticket=04e52805f7fdce3c42b2d1a792f86ade840ce8391200&raida=raida1&email=2222ram@protonmail.com&phone=118004353333

Note - Email Id should be unique User can update email and phone number only, the condition will follow by coins generated by raida server. The system will automatically check if the user exists or not, then perform create or update the user. coins field will use as an identifier.
Add user => Verified Update User => Verified


Add user => Verified
Update User => Verified


http://localhost/store/api/users/details.php?ticket=04e52805f7fdce3c42b2d1a792f86ade840ce8391200&raida=raida1&user_sn=6301000&action=download_profile

To get another user profile -
URL - http://localhost/store/api/users/details.php?ticket=04e52805f7fdce3c42b2d1a792f86ade840ce8391200&raida=raida1&user_sn=6301000

Get Another User details => Verified
Note - if user_sn will not parse then the system will fetch the existing record.



Get my own profile => verified
URL - http://localhost/store/api/users/details.php?ticket=04e52805f7fdce3c42b2d1a792f86ade840ce8391200&raida=raida1


Download Another user profile image => Verified 
http://localhost/store/api/users/details.php?ticket=04e52805f7fdce3c42b2d1a792f86ade840ce8391200&raida=raida1&user_sn=6301000&action=download_profile

Download my own profile -

http://localhost/store/api/users/details.php?ticket=04e52805f7fdce3c42b2d1a792f86ade840ce8391200&raida=raida1&action=download_profile


Upload profile pic -

Method = POST

localhost/store/api/users/user_upload.php?ticket=1418e5356381bb5d3119c2f5a5c1bc6b276bc25cad00&raida=raida1


----POST Ads---
http://localhost/store/api/ads/create.php?owner_user_sn=2225&ticket=1f92dc616650fda58ed49245232dc67705a75e76d3b6&top_catagory=1&latitude=39.733657&longitute=-121.775251&country=20&region_state=California&city=San%20Diego&title=Testing%20ad%20title&price=300&description=add%20desc&sub_catagory=7

Note - As per current flow, If the network is not available, then ad_owner_id will take.
Onwer_user_sn not mandatory, but make sure raida responding
The description is not compulsory. Apart from the above two, all fields are to post a new ad.

----Update Existing Ad---


-----Get Ad details ----

http://localhost/store/api/ads/details.php?ad_id={63E6A9551-AFB9-051D-EB7A-CF38004A2CBA}&raida=raida1&ticket=1234567

Ad_id will use to get ad details
ad_id is mandatory


----Get all others ads-----
http://localhost/store/api/ads/list.php?raida=raida1&ticket=1f92dc616650fda58ed49245232dc67705a75e76d3b6&opt=all



Get all my ads

http://localhost/store/api/ads/list.php?raida=raida1&ticket=1f92dc616650fda58ed49245232dc67705a75e76d3b6


opt=all


----Review on ads--

--------------Post review----

http://localhost/store/api/ads/review.php?ticket=1234432&raida=raida1&ad_id=124&comment=nice&rating=4
reating should between 1-5
A user not allow to ad more then one time reviews
Comments shopuld not be blank
ad_id must be available
ad_id must be valid


------Ad images ----

Upload ads
Upload image
Store image in db

------------Get all images-------

------------Delete images----------


# P2P-Exchange-Server
This server will allow the advanced client to connect and get trading data.

[Create a New User](README.md#create-a-new-user)

[Create a New Sell Order](README.md#create-a-new-sell-order)

[Create a New Buy Order](README.md#create-a-new-buy-order)

[List Buy Orders](README.md#list-buy-orders)

[List Sell Orders](README.md#list-sell-orders)

[Delete Buy Order](README.md#delete-buy-order)

[Delete Sell Order](README.md#delete-sell-order)

[Post a Transaction](README.md#post-a-transaction)

[List Transactions](README.md#list-a-transaction)

[Rate a Transaction](README.md#rate-a-transaction)

## Database Scheema
```sql
CREATE TABLE `users` (
  `coinsn` int(10) unsigned NOT NULL DEFAULT '0',
  `username` varchar(16) NOT NULL,
  `email` varchar(60) NOT NULL,
  `dateofjoining` datetime NOT NULL,
  PRIMARY KEY (`coinsn`),
  UNIQUE KEY `UC_username` (`username`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

For review -

http://localhost/store/api/ads/review.php?ticket=1234432&raida=raida1&ad_id={EE5744B0-01A0-B098-79FE-50972962F908}&comment=nice&rating=4

Note - One user is always allowed once to ad review.
Ad_id should be valid.
Fields should not blank.
Rate value should be between 1-5

CREATE TABLE `reviews` (
  `review_id` varchar(50) NOT NULL DEFAULT '0',
  `poster_sn` varchar(50) NOT NULL,
  `reviewee_sn` varchar(60) NOT NULL,
  `rating_in_starts` varchar(60) NOT NULL,
  `review_text` varchar(60) NOT NULL,
  `response_text` varchar(60) NULL,
  `date_posted` datetime NOT NULL,
  PRIMARY KEY (`review_id`),
  UNIQUE KEY `UC_username` (`review_id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;



CREATE TABLE `users` ( 
  `coinsn` int(10) unsigned NOT NULL DEFAULT '0',
     `email` varchar(60) NOT NULL,
        `phone` varchar(16) NOT NULL,
           `code_name` varchar(16) NOT NULL,
              `banned` BOOLEAN NOT NULL,
                 `dateofjoining` datetime NOT NULL,
                    PRIMARY KEY (`coinsn`),
                       UNIQUE KEY `UC_username` (`email`) ) ENGINE=InnoDB DEFAULT CHARSET=latin1;



CREATE TABLE `ads` (
  `ad_id` VARCHAR(200),
  `owner_user_sn` INT(11),
  `date_posted` DATETIME,
  `top_catagory` INT,
  `sub_catagory` INT,
  `latitude` DECIMAL(9,6),
  `longitute` DECIMAL(9,6),
  `country` INT,
  `region_state` VARCHAR(200),
  `city` VARCHAR(200),
  `title` VARCHAR(200),
  `price` DECIMAL,
  `description` TEXT(200),
  `prohibited` INT
) ENGINE=InnoDB;


http://localhost/store/api/ads/create.php?owner_user_sn=16777215&ticket=1f92dc616650fda58ed49245232dc67705a75e76d3b6&top_catagory=1&sub_catagory=5&latitude=39.733657&longitute=-121.775251&country=20&region_state=California&city=San%20Diego&title=Will%20Program%20for%20CloudCoins&price=5000&description=bla%20bla%20bla

-------------Update ads -----

http://localhost/store/api/ads/create.php?ad_id=3232323232&owner_user_sn=16777215&ticket=1f92dc616650fda58ed49245232dc67705a75e76d3b6&top_catagory=1&sub_catagory=5&latitude=39.733657&longitute=-121.775251&country=20&region_state=California&city=San%20Diego&title=Will%20Program%20for%20CloudCoins&price=5000&description=bla%20bla%20bla


-----Delete Ads------ 
http://localhost/store/api/ads/delete.php?raida=raida1&ad_id={43F0AB5E-99E8-6D19-6852-B3B3EE2A8243}&ticket=1f92dc616650fda58ed49245232dc67705a75e76d3b6

----Get All Ads -----

http://localhost/store/api/ads/list.php?raida=raida1&owner_user_sn=16777215&ticket=1f92dc616650fda58ed49245232dc67705a75e76d3b6&opt=all

Note -
opt=all to return all ads.

----Get my ads----

-----Get 

---Alter table for multiple images in db ---

alter table ads add images varchar(200) after description;




CREATE TABLE `users` (
  `coinsn` int(10) unsigned NOT NULL DEFAULT '0',
  `email` varchar(60) NOT NULL,
  `phone` varchar(16) NOT NULL,
  `code_name` varchar(16) NOT NULL,
  `banned` BOOLEAN NOT NULL,
  `dateofjoining` datetime NOT NULL,
  PRIMARY KEY (`coinsn`),
  UNIQUE KEY `UC_username` (`username`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;


CREATE TABLE `sellorders` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `coinsn` int(11) NOT NULL,
  `qty` int(10) unsigned NOT NULL,
  `price` decimal(8,2) NOT NULL,
  `currency` varchar(10) NOT NULL DEFAULT 'USD',
  `dateposted` datetime NOT NULL,
  `paymentmethod` varchar(12) NOT NULL,
  `status` int(10) unsigned NOT NULL DEFAULT '0',
  `lastmodified` datetime NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=9 DEFAULT CHARSET=latin1;


TABLE `buyorders` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `coinsn` int(10) unsigned NOT NULL DEFAULT '0',
  `qty` int(10) unsigned NOT NULL DEFAULT '0',
  `price` decimal(10,2) NOT NULL,
  `dateposted` datetime NOT NULL,
  `currency` varchar(20) NOT NULL,
  `sellorderid` int(10) unsigned DEFAULT '0',
  `paymentmethod` varchar(100) NOT NULL,
  `lastmodified` datetime NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=9 DEFAULT CHARSET=latin1;


CREATE TABLE `transactions` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `sellorderid` int(10) unsigned NOT NULL,
  `buyerid` int(10) unsigned NOT NULL,
  `sellerid` int(10) unsigned NOT NULL,
  `qty` int(10) unsigned NOT NULL DEFAULT '0',
  `price` decimal(10,2) NOT NULL,
  `transactiondate` datetime NOT NULL,
  `buyerrating` int(10) unsigned NOT NULL,
  `sellerrating` int(10) unsigned NOT NULL,
  `transactionnumber` varchar(20) NOT NULL,
  `recieptnumber` varchar(20) NOT NULL,
  `buyercomment` text NOT NULL,
  `sellercomment` text NOT NULL,
  `buyorderid` int(10) unsigned NOT NULL,
  `currency` varchar(10) NOT NULL,
  `paymentmethod` varchar(45) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=latin1;


```
## Create a New User
This service allows a user to create or update their information. 
The ticket and RAIDA number are required to allow the user to establish their identity. The email and username are not required

Sample Get Request
```html
https://www.cloudcoin.exchange/api/users/create.php/?ticket=cb9db1c1b622bebde6ae7958c924f1fc9c7dec24cc00&raida=0&email=username@email.com&username=usernamevalue

```
Response
```json
{
      "username": "",
       "sn": "",
        "dateofjoining": "",
          "email": ""
}
```

```json

{
     "Message": "Error Message"
}
```



## Create a New Sell Order 
Advertises to others that the user wants to sell CloudCoins.

qty: How many CloudCoins the user wants to sell. 

price: the price in the currency specified

currency: Which currency the person has listed the price in. 

Payment Method: Maybe many payment methods separated by commas. 
 
url: The location of the sales page that the seller is using (usually their local machine)

```html
https://www.cloudcoin.exchange/api/sellorder/create.php/?raida=0&ticket=6511a0cbb4c3d6576d62c8a51dc532187be49b5d0b00&qty=25000&price=0.035&currency=AUD&paymentmethod=Paypal&url=http%3A%2F%2Fmyserver.com%2Findex.html%0D%0A
```

```json
Success : Status Code : 200
Response: {
      “id”,
      “sellordernumber”: “”,
       “quantity”: “”,
        “price”: “”,
        “dateposted”: “”,
         “currency”: “”,
         “paymentmethod”: “”
}

Failure : Status Code : 400
Response: {
     Message: “Error Message”
}

```

## Create New Buy Order
It allows the user to advertise their willingness to buy. 

Sell Order id is the ID of the order against which the buy order is being placed.                                                      If it is not put against any particular sell order, then the sell order id can be left out.

```html
https://www.cloudcoin.exchange/api/buyorder/create.php/?raida=0&ticket=6511a0cbb4c3d6576d62c8a51dc532187be49b5d0b00&qty=25000&price=0.035&currency=AUD&paymentmethod=Paypal&sellorderid=1
```
```json
Success : Status Code : 200
Response: {
      “id”,
      “buyordernumber”: “”,
       “quantity”: “”,
        “price”: “”,
        “dateposted”: “”,
         “currency”: “”
}

Failure : Status Code : 400
Response: {
     Message: “Error Message”
}

```

## List Sell Orders
Lists the Sell orders with the offset and page sizes. By default, it shows sell orders posted by the current user.
If the optional parameter opt=all is used, then it shows all the sell orders. The list is given in descending orders of the sell orders timestamp.

```html
https://www.cloudcoin.exchange/api/sellorder/list.php/?offset=0&pagesize=10&opt=all&raida=0&ticket=6511a0cbb4c3d6576d62c8a51dc532187be49b5d0b00
```
```json
Success : Status Code : 200
Response: [{
     “id”, “”,
     “quantity”, “”,
     “price”: “”,
     “dateposted”: “”,
     “currency”: “”,
     “username”: “”
}]

Failure : Status Code : 400
Response: {
     Message: “Error Message”
}

```


## List Buy Orders
Lists the Buy orders with offset and page sizes. By default, it shows buy orders posted by the current user.
If the optional parameter opt=all is used, then it shows all the buy orders. The list is given in descending orders of buy orders timestamp.

```html
https://www.cloudcoin.exchange/api/buyorder/list.php/?offset=0&pagesize=10&opt=all&raida=0&ticket=6511a0cbb4c3d6576d62c8a51dc532187be49b5d0b00
```
```json
Success : Status Code : 200
Response: [{
     “id”, “”,
     “quantity”, “”,
     “price”: “”,
     “dateposted”: “”,
     “currency”: “”,
     “username”: “”
}]

Failure : Status Code : 400
Response: {
     Message: “Error Message”
}


```



## Delete Sell Order
t allows users to delete their sell orders. 
A sell order can only be deleted if it is in an Open state. That means if a transaction has not been executed against the sell order, it can be deleted. You can pass the id parameter to delete a sell order.
```html
https://www.cloudcoin.exchange/api/sellorder/delete.php/?opt=all&raida=0&ticket=6511a0cbb4c3d6576d62c8a51dc532187be49b5d0b00&id=101
```

```json
Success : Status Code : 200
Response: {
       “MESSAGE”: “Sell Order Deleted successfully”
      “id”,
      “sellordernumber”: “”,
       “quantity”: “”,
        “price”: “”,
        “dateposted”: “”,
         “currency”: “”,
         “paymentmethod”: “”
}

Failure : Status Code : 400
Response: {
     Message: “Error Message”
}

```


## Delete Buy Order
A buy order can only be deleted if it is in an Open state. That means if a transaction has not been executed against the buy order, it can be deleted. You can pass the id parameter to delete a buy order.


```html
https://www.cloudcoin.exchange/api/buyorder/delete.php/?opt=all&raida=0&ticket=6511a0cbb4c3d6576d62c8a51dc532187be49b5d0b00&id=101
```
```json
Success : Status Code : 200
Response: {
       “MESSAGE”: “Buy Order Deleted successfully”
      “id”,
      “buyordernumber”: “”,
       “quantity”: “”,
        “price”: “”,
        “dateposted”: “”,
         “sellordernumber”: “”
         “currency”: “”
}

Failure : Status Code : 400
Response: {
     Message: “Error Message”
}

```
## Post a Transaction
This will be plugged into the sellers' webpage on their webserver. When someone buys, the page will post the transaction.. 
```html
https://www.cloudcoin.exchange/api/transaction/post.php/?raida=0&ticket=6511a0cbb4c3d6576d62c8a51dc532187be49b5d0b00&qty=25000&price=0.035&currency=AUD&paymentmethod=Paypal&sellorderid=1&buyorderid=2&buyerid=1&sellerid=2&buyercomment=buyercomment&sellercomment=sellercomment&buyerrating=3.0&sellerrating=4.0&transactionno=trnno&recieptno=recno
```
```json
Success : Status Code : 200
Response: {
      “id”,
      “sellordernumber”: “”,
       “quantity”: “”,
        “price”: “”,
        “dateposted”: “”,
         “currency”: “”,
         “paymentmethod”: “”
}

Failure : Status Code : 400
Response: {
     Message: “Error Message”
}

```

## List Transactions
The user can sell all the transactions that have taken place recently so that they can be rated by the people involved.d. 

```html
https://www.cloudcoin.exchange/api/transaction/list.php/?raida=0&ticket=6511a0cbb4c3d6576d62c8a51dc532187be49b5d0b00
```
```json
Success : Status Code : 200
Response: [{
     “id”, “”,
      “buyerid”: “”,
      “sellerid”: “”,
     “quantity”, “”,
     “price”: “”,
     “dateposted”: “”,
     “currency”: “”,
     “Recieptnumber”: “”,
      “buyorderid”: “”,
      “sellorderid”:””
}]

Failure : Status Code : 400
Response: {
     Message: “Error Message”
}

```


## Rate a Transaction
Rate a transaction after its posted. It can be used for both the seller and buyer.                                                  
There is no need for separate parameters for the buyer rating and the seller rating.                                                    Same goes for the buyer comments and the seller comments.

```html
https://www.cloudcoin.exchange/api/transaction/post.php/?raida=0&ticket=6511a0cbb4c3d6576d62c8a51dc532187be49b5d0b00&rating=4.0&comment=comment
```
```json
Success : Status Code : 200
Response: [{
“transactionid”: “”,
      “rating”: “”,
       “comment”: “”
}]

Failure : Status Code : 400
Response: {
     Message: “Error Message”
}


```







