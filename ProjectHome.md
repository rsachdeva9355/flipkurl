**Note: Flipkart's site has changed a lot in last 2 years. The API does not work anymore.**

# What is flipkurl ? #
Flipkart is an awesome india based online book shopping site.

Flipkurl is a **php** - **curl** based library to access the contents of flipkart.com site, login into it, search book listings, add books to cart, move books from to wishlist, read contents of cart, etc.

Usually shopping carts don't persist the user's selection across logins, but this one does. So whatever books you add via the library will stay in your account, so you can checkout/pay later from there.

## What can it be used for ? ##
  * Custom & Personalized user interface
  * It can probably be used to create a mobile based interface as the site already doesn't have one.
  * Mashups along with API's of other sites
  * Automate stuff

## Where can i get it? ##
Its just 1 file, grab/browse the code from the **[svn repository](http://code.google.com/p/flipkurl/source/browse/trunk)** or the [downloads page](http://code.google.com/p/flipkurl/downloads/list)

## Are there any bugs? ##
I am a human. Feel free to condemn my humanness in the [issue tracker](http://code.google.com/p/flipkurl/issues/list) or [here](http://kalyanchakravarthy.net/?page_id=8)

## Requirements ##
  * PHP 5.x
  * PHP Extensions
    * cURL
    * DomDocument
    * DOMXPath
  * Access to a folder to store cookies

# Examples #
### Basic login ###
```
<?php
include( "Flipkurl.php" );

//Create a new object
$fk = new Flipkurl();

//Optionally set the cookie directory. Default is current dir.
$fk->cookies_dir = "cookiesdump/";

//Login
$result = $fk->login( "username", "password" );
if( $result )
    echo "Login successful";
else
    echo "Login failed";
?>
```

### Search flipkart ###
```
<?php
$listing = $fk->getSearchListing( "chetan bhagat" );
print_r( $listing );
?>
Array
(
    [from] => 1
    [to] => 10
    [total] => 12
    [pages] => 2
    [page] => 1
    [results] => Array
        (
            [0] => Array
                (
                    [mrp] => 95
                    [price] => 80
                    [saving] => 15
                    [discount] => 16
                    [status] => In Stock
                    [summary] => The novel starts with the meeting of Chetan Bhagat...
                    [eid] => 2KW3FGDVQC
                    [title] => One Night At The Call Center
                    [link] => /one-night-call-center-chetan/0004133056-2kw3fgdvqc/chetan-bhagat/1
                    [author] => Array
                        (
                            [0] => Chetan Bhagat
                        )

                )
...
...
)
```

### Add a book ###
```
<?php
$pageBooks = $listing["results"];

$book1 = $pageBooks[0];
$fk->addBook( $book1["eid"] );

$book2 = $pageBooks[1];
$fk->addToWishList( $book1["eid"] );
?>
```

### Fetch cart contents ###
```
<?php
$contents = $fk->getCartContents();
echo "Grand Total : Rs." . $contents["summary"]["total"];
echo "You are saving : Rs." . $contents["summary"]["saving"];
echo "Total items in cart : " . count($contents["items"]);
?>
```

### Logout ###
```
<?php
$fk->logout();
?>
```

## Why was it created ? ##
It was created just for fun, blame the boring sunday.

## Who am i? ##
i am [kalyan](http://kalyanchakravarthy.net)!