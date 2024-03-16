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

The final result
![Online shop page completed task](./assets/task-1/online-shop-page.png 'Online shop page completed task')

References:

- [Task one](https://resourcesone.blogspot.com/2023/12/design-stunning-woocommerce-shop.html)
