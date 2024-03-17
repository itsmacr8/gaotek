# My journey of [GAOTek Inc.](https://www.linkedin.com/company/gao-tek-inc-/)

## Task 1: Creating an Online Shop Page

The first task involves setting up a shop page for my online store. I've established the website on my local host using [XAMPP](https://www.apachefriends.org/download.html). I download and activate [Astra](https://wpastra.com/) theme and use started template.

To accomplish this task, I need to install three plugins:

- WooCommerce by Automattic
- WPCode Lite by WPCode
- YITH Request a Quote for WooCommerce by YITH

Next, I need to import all the products from a provided .csv file.

Following that, I need to replace the **"Add to Cart"** button with an **"Add to Quote"** button. This is done with the assistance of the **YITH and WPCode Lite** plugins.

- I disable the add to cart and price option using the YITH plugin.
- I add the "Add to Quote" option using raw PHP and CSS code with the WPCode Lite plugin.

Finally, I truncate the **product title** to two lines and I enable the **short description**n from the WooCommerce settings and truncate it to four lines.

Task one final result
![Online shop page completed task](./assets/task-1/online-shop-page.png 'Online shop page completed task')

WooCommerce - shop - Add to Quote (php)

```php
add_action( 'woocommerce_after_shop_loop_item', 'add_to_quote_button', 11 );

function add_to_quote_button() {
global $product;
$id = $product->get_id();
$title = $product->get_title();
$sku = $product->get_sku();
$site_url = get_site_url();

echo '<a
    href="' . $site_url . '/request-quote/?add-to-quote=' . $id . '"
    data-quantity="1"
    class="button"
    data-product_id="' . $id . '"
    data-product_sku="' . $sku . '"
    aria-label="Add “' . $title . '” to your quote"
    aria-describedby=""
    rel="nofollow"
>
    Add to quote
</a>';
}
```

WooCommerce - Shop (CSS)

```css
/* Customize product card */
.products .product {
 background-color: #F0F0F7;
 padding: 18px !important;
 border-radius: 12px;
}

/* Customize product image */
.products .product img {
 border-radius: 8px;
}

/* Customize product category text */
.astra-shop-summary-wrap .ast-woo-product-category {
  margin-top: 5px;
  font-weight: 600;
  color: #1E1B4B !important;
}

/* Truncate product title by 2 lines */
.astra-shop-summary-wrap h2 {
 overflow: hidden;
 display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  margin-top: 10px !important;
  font-size: 17px !important;
}

/* Truncate product description by 4 lines */
.astra-shop-summary-wrap .ast-woo-shop-product-description {
  overflow: hidden;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 4;
  margin-bottom: 30px;
}

/* Remove the price and star ratings from product card */
.astra-shop-summary-wrap .price, .astra-shop-summary-wrap .star-rating {
  display: none !important;
}

/* Adjust add to quote button width and push it at the bottom of the card */
.products .product .button {
  width: fit-content;
  margin-top: auto !important;
}

/* Customize sorting dropdown */
.woocommerce-ordering select {
  background-color: #F5F5FA !important;
  border: 3px solid #F0F0F7 !important;
  border-radius: 8px !important;
}
```

## Task 2: Enhance the Single Product Page

Imagine you're an artist, and your canvas is the single product page of an online store. Your task is to transform this page into a masterpiece of user experience and design.

Firstly, you dive into the settings of WooCommerce's single product page. Here, you find the **product category** displayed prominently. But you decide to hide it, allowing the product itself to take center stage.

Next, you notice the meta information. It's currently nestled after the **"Add to Quote"** button, but you feel it would serve better right after the **product title**. So, you move it, like rearranging furniture in a room for better flow.

Now, you turn your attention to readability. You decide to make the product title bold, making it stand out more. You also introduce some white space between the **meta description** and the **"Add to Quote"** button. This gives the page a cleaner, more streamlined appearance. You also ensure that the Add to Quote button aligns perfectly with the quantity button, like aligning a picture frame on a wall.

Your next move is to the product cart. You decide to soften its sharp corners with a rounded edge, giving it a more appealing look.

Lastly, you turn your artistic eye to the product table on the product page. You customize it, transforming it into a more visually appealing presentation.

And there you have it - a single product page, transformed into a work of art.
![Single product page completed task](./assets/task-2/single-product-page.png 'Single product page completed task')

WooCommerce - Product - Image Section (CSS)

```css
/* Make the thumbnail images' corners a bit rounded to match brand design */
.flex-control-thumbs li img {
  border-radius: 6px;
}
/* Add borders to the active thumbnail image for clear indication */
.flex-active {
  border: 2px solid #4338ca;
}
.woocommerce-js div.product div.woocommerce-product-gallery--columns-4 .flex-control-thumbs li {
  margin: 0;
}
```

WooCommerce - Product - Info and CTA Section (CSS)

```css
/* Increase font weight of breadcrumb texts */
.woocommerce-breadcrumb {
  font-weight: 500;
}

/* Hightlight the links in breadcrumb for design purpose */
.woocommerce-js .woocommerce-breadcrumb a {
  color: #4338CA;
}

/* Increase font weight of product title and add some space at top */
.entry-title {
  font-weight: 600;
}

/* Add another border below the product meta information (SKU and categories) */
.product_meta {
  border-bottom: 1px solid var(--ast-border-color);
  padding-bottom: 0.5em;
}

/* Customize the quantity selector */
.product .quantity input[type=number] {
  padding: 8px;
  border-radius: 6px;
  border: 2px solid var(--ast-border-color);
}

/* Remove margin and float from quantity selector */
.woocommerce-js div.product form.cart div.quantity {
  float: none;
  margin: 0;
}

/* They don't have parent element that's why cannot use flexbox */
form.cart, .yith-ywraq-add-to-quote {
  display: inline-block;
}

/* They don't have parent element that's why cannot use flexbox */
form.cart, .yith-ywraq-add-to-quote {
  display: inline-block;
}

/* Decrease font-size of the text of add to quote button */
.yith-ywraq-add-to-quote a {
  font-size: 14px !important;
}

/* Decrease padding of the text of add to quote button */
.woocommerce-js a.button {
  padding-inline: 16px;
  padding-block: 12px;
}
```

WooCommerce - Product - Table (CSS)

```css
/* Increase the width of the top and left borders of the table */
.wc-tab table {
  border-top: 2px solid #E0E0E0;
  border-left: 2px solid #E0E0E0;
}

/* Increase the width of the bottom and right borders of each cell */
.wc-tab tr td {
  border-bottom: 2px solid #E0E0E0;
  border-right: 2px solid #E0E0E0;
  padding: 10px;
}

/* Additional styles for the table headers to make them stand out */
.wc-tab tr td:first-child {
  font-weight: 900;
  width: 25%;
  background-color: #F5F5FA;
}
```

References:

- [Task 1: Creating an Online Shop Page](https://resourcesone.blogspot.com/2023/12/design-stunning-woocommerce-shop.html)
- [Task 2: Enhance the Single Product Page](https://resourcesone.blogspot.com/2023/12/captivating-woocommerce-product-page.html)
