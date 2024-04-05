# My journey of [GAOTek Inc.](https://www.linkedin.com/company/gao-tek-inc-/)

## Table of contents

- [Task 1: Creating an Online Shop Page](#task-1-creating-an-online-shop-page)
- [Task 2: Enhance the Single Product Page](#task-2-enhance-the-single-product-page)
- [Task 3: The Carousel Transformation](#task-3-the-carousel-transformation)
- [Task 4: Crafting the Perfect Contact Form](#task-4-crafting-the-perfect-contact-form)
- [Task 5: The Magic of Live AJAX WooCommerce Product Search](#task-5-the-magic-of-live-ajax-woocommerce-product-search)


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

## Task 3: The Carousel Transformation

Imagine walking into an art gallery, where each painting is a product thumbnail. Now, imagine that instead of walking from painting to painting, you could simply press a button and the paintings would come to you, one after another. That's the magic we're about to create in this task.

Our first step is to add some custom PHP code. This will conjure up a pair of buttons - one for the previous image and one for the next - right after the thumbnail images.

But we're not quite satisfied with ordinary buttons. We want something sleeker, more elegant. So, we summon the power of the Font Awesome plugin to transform these buttons into stylish arrows. Then, like an interior designer adjusting the placement of a piece of furniture, we move these arrow buttons to the perfect spot that suits our design needs.

Now, we face a challenge. There are too many thumbnail images - it's overwhelming. So, we decide to limit the number of visible thumbnail images to just four, tucking the rest out of sight. It's like having a private collection of paintings in the back room.

Finally, we breathe life into the arrow buttons. With a click of functionality, these buttons can now dynamically bring forth the next image or take you back to the previous one when clicked.

And voila! We've transformed our WooCommerce Product Thumbnails into a dynamic carousel.
![WooCommerce Product Thumbnails dynamic carousel](./assets/task-3/thumbnail-slider.png 'WooCommerce Product Thumbnails dynamic carousel')

Enable arrow for product thumbnail slider (php)

```php
//Filter WooCommerce Flexslider options - Add Navigation Arrows
add_filter( 'woocommerce_single_product_carousel_options', 'sf_update_woo_flexslider_options' );
function sf_update_woo_flexslider_options( $options ) {
    $options['directionNav'] = true;
    return $options;
}
```

Hide Previous and Next default label and add new icon with font awesome

```css
a.flex-next, a.flex-prev {
  visibility: hidden;
}

/* Set height so that it displays four image and hide other images */
.woocommerce-product-gallery .flex-control-thumbs {
  position: relative;
  display: flex;
  flex-wrap: wrap;
  width: 590px;
  height: 110px;
}

/* Set the direction of arrows*/
ul.flex-direction-nav {
  margin: 0;
  padding: 0px;
  list-style: none;
  display: flex;
}

/* set position of previous arrow*/
li.flex-nav-prev {
  position: absolute;
  bottom: 40px;
  left: -50px;
}

/* set position of next arrow*/
li.flex-nav-next {
  position: absolute;
  bottom: 40px;
  right: 60px;
}

/* next arrow appear */
a.flex-next::after {
  visibility: visible;
  content: '\f105';
  font-family: 'Font Awesome 5 Free';
  margin-top: 0px;
  font-size: 20px;
  font-weight: bold;
}

/* previous arrow appear*/
a.flex-prev::before {
  visibility: visible;
  content: '\f104';
  font-family: 'Font Awesome 5 Free';
  margin-top: 0px;
  margin-left: 30px;
  font-size: 20px;
  font-weight: bold;
}

ul.flex-direction-nav li a {
  color: #ccc;
}

ul.flex-direction-nav li a:hover {
  text-decoration: none;
}

ul.flex-direction-nav li a:hover {
  text-decoration: none;
}

.flex-control-nav {
  top: 0px;
}
```

WooCommerce - Product - Image - Magnify glass (CSS)

```css
.woocommerce-js div.product div.images .woocommerce-product-gallery__trigger {
  right:4.5em
}
```

WooCommerce - Product - Image Section - Thumbnail Slider (JS)

```js
// scroll the images through images index
const updateCarousel = (selectedImgIndex, lastImgIndex) => {
    let indexOfImgToScroll = selectedImgIndex - 3;
    if (selectedImgIndex < 3 || lastImgIndex <= 3) indexOfImgToScroll = -1;
    else if (selectedImgIndex === lastImgIndex) indexOfImgToScroll = indexOfImgToScroll-1;

    document.querySelectorAll(".flex-control-thumbs li").forEach((li, i) => {
        if (i <= indexOfImgToScroll) {li.style.transform = 'translateX(-150px)'; li.style.display='none';}
        else {li.style.transform = 'translateX(0)'; li.style.display='list-item';}
        li.style.transition = 'transform 0.4s linear';
    });
};

// Mutation observer is used to keep the record of active images
// and change the image accordingly
document.addEventListener("DOMContentLoaded", (event) => {
    setTimeout(() => {
        let observer = new MutationObserver((mutations) => {
            mutations.forEach((mutationRecord) => {
                if (mutationRecord.target.className === "flex-active") {
                    const allElements = mutationRecord.target.parentNode.parentNode.children;
                    const targetedElement = mutationRecord.target.parentNode;
                    const indexOfTargetedElement = Array.from(allElements).indexOf(targetedElement);
                    const lastElementIndex = document.querySelectorAll(".flex-control-thumbs li").length - 1;

                    updateCarousel(indexOfTargetedElement, lastElementIndex);
                }
            });
        });

        document.querySelectorAll(".flex-control-thumbs li img").forEach((img, i) => {
            observer.observe(img, {
                attributes: true,
                attributeFilter: ['style', 'class'],
            });
        });
    }, 0);
});
```

Prerequisites:

- Font Awesome plugin
- WPCode Lite by WPCode

## Task 4: Crafting the Perfect Contact Form

Imagine you're a skilled artisan, and your craft is creating contact forms. Your tools are the Contact Form 7 plugin and the Contact Form CFDB7.

With these tools in hand, you begin your work. You shape the form using the syntax provided by Contact Form 7, like a sculptor working with a block of marble. Each field, each button, each element is carefully carved out, following the blueprint provided by the plugin's official documentation.

But your work doesn't stop there. You then style the form, tailoring it to fit your specific needs. It's like painting the sculpture, adding color and life to the previously blank canvas.

And finally, you ensure that every piece of user data entered into the form is safely stored with the help of Contact Form CFDB7. It's like adding a protective varnish to your sculpture, preserving it for the future.

And there you have it - a beautifully crafted, functional, and secure contact form.
![Crafting the Perfect Contact Form completed task](./assets/task-4/contact-form-part-1.png 'Crafting the Perfect Contact Form completed task')

Prerequisites:

- Contact Form 7 by Takayuki Miyoshi
- Contact Form CFDB7 by Arshid

## Task 5: The Art of Crafting a Custom Contact Form

Imagine you're a skilled artisan, tasked with crafting a unique contact form. We got a blueprint by a YouTuber. This blueprint isn't for a building or a machine, but for a contact form. **Your task is to bring this design to life in a way that is independent of both the browser and the theme.** Your tools? Not the usual HTML code, but the syntax of Contact Form 7.

This form isn't just any form - it's a custom design. The default design offered by the browser is too ordinary, too plain. So, you roll up your sleeves and get creative. You redesign the HTML select elements, the radio buttons, and the checkboxes, transforming them into something unique. It's like being an architect, reshaping the landscape of your form.

But there's a catch. You can't use HTML code to create the form. It's like being asked to sculpt a statue without a chisel. So, you turn to CSS code, adjusting it to fit the HTML elements generated by the Contact Form 7 syntax code.

But your task doesn't end there. This form has to be a chameleon, able to adapt to any theme. If you change the themes, the form should still look the same. It's a theme-independent design, a form that remains constant amidst change.

And of course, it should look the same in all browsers, a testament to its adaptability and resilience.

And so, you embark on this journey of crafting a custom contact form, turning a YouTuber's design into a functional reality. It's a challenging task, but one that you're more than capable of handling. After all, you're not just any artisan - you're a master of your craft.

Contact form 7 syntax elements

```sh
<label for="cu-first-name">First name</label>
[text* first-name id:cu-first-name class:cu-first-name]

<label for="cu-last-name">Last name</label>
[text* last-name id:cu-last-name class:cu-last-name]

<label for="cu-email-address">Email address</label>
[email* email-address id:cu-email-address class:cu-email-address]

<label for="cu-favorite-browser">Favorite Browser?</label>
[select favorite-browser id:cu-favorite-browser class:cu-favorite-browser include_blank default:4 "Google Chrome" "Mozilla Firefox" "Safari" "Microsoft Edge"]

<label for="cu-gender">Gender</label>
[radio gender id:cu-gender class:cu-gender default:1 "Male" "Female"]

<label for="cu-js-framework">Favorite JS framework</label>
[radio js-framework id:cu-js-framework class:cu-js-framework default:1 "React" "Vue" "Angular"]

<label for="cu-css-framework">Favorite CSS framework</label>
[radio css-framework id:cu-css-framework class:cu-css-framework default:1 "Bootstrap" "Foundation" "Material Design"]

<label for="cu-frequent-apps">Which apps do you use frequently?</label>
[checkbox frequent-apps id:cu-frequent-apps class:cu-frequent-apps default:1 "Whatsapp" "Instagram" "Snapchat" "Tiktok"]

<label for="cu-frequent-sports">Sports?</label>
[checkbox frequent-sports id:cu-frequent-sports class:cu-frequent-sports default:1 "Football" "Cricket" "Golf" "Swimming"]

<label for="cu-acceptance" class="switch"></label>
[checkbox consent id:cu-acceptance class:cu-acceptance "."]

[submit class:btn-primary "Submit"]
```

Contact form (CSS)

```css
:root {
  --white: hsl(0, 0%, 100%);
  --lighter-gray: hsl(201, 100%, 96%);
  --light-gray: hsl(0, 0%, 80%);
  --dark-gray: hsl(0, 0%, 65%);
  --darker-gray: hsl(0, 0%, 20%);
  --primary-light: hsl(201, 100%, 81%);
  --primary: hsl(200, 100%, 61%);
  --primary-dark: hsl(201, 100%, 36%);
  --shadow: hsla(0, 0%, 0%, 0.1);

  /* Form settings */
  --form-width: 800px;
  --form-padding: 2rem;
  --form-margin-Y: 4rem;
  --form-margin-X: 1rem;
  --form-shadow: 0 0 40px 0 var(--shadow);
  --form-bg-color: var(--white);

  /* Form label settings */
  --form-label-fs: 1rem;
  --form-label-mb: 2px;

  /* Form Submit button settings */
  --submit-button-padding: 12px 24px;
  --submit-button-border-radius: 50px;
  --submit-button-width: 80%;
  --submit-button-text: uppercase; /* capitalize | lowercase */

  /* Custom radio button and checkbox position setting */
  --gender-circle: 2px;
  --gender-check: 6px;
  --apps-circle: 3px;
  --apps-check: 4px;

  /* Custom radio button and checkbox Height and width setting */
  --gender-apps-height: 30px;
  --gender-apps-width: 65px;
  --js-css-sports-padding: 5px 10px;
  --js-css-sports-height: 40px;
  --js-sports-height: 75px;
  --css-apps-width: 100px;
  --css-tab-dek-width: 125px;

  /* Switch setting */
  --switch-container: var(--light-gray);
  --switch-container-height: 25px;
  --switch-container-width: 45px;
  --switch-container-border-radius: 35px;
  --switch-circle: var(--white);
  --switch-circle-size: 18px;
  --switch-circle-border-radius: 50%;
  --switch-circle-top-position: 3px;
  --switch-circle-left-position: 4px;

  --border: 1px solid var(--dark-gray);
  --border-primary: 1px solid var(--primary);
}
/* For Tablet and desktop devices */
@media screen and (min-width: 768px) {
  :root {
    --form-padding: 3.125rem;
    --form-margin-Y: 6rem;
    --form-label-fs: 1.3125rem;
    --form-label-mb: 5px;
    --submit-button-padding: 15px 30px;
    --js-css-sports-padding: 10px 20px;
    --js-css-sports-height: 50px;
    --js-sports-height: 90px;
  }
}
/* Because form width is 800 pixels, margin-inline
auto does not work within 800 pixels devices.
Now, it will use the default 1rem from mobile devices. */
@media screen and (min-width: 830px) {
  :root {
    --form-margin-X: auto;
  }
}

/* Theme specific codes */

/* For Twenty Twenty-[<year>] theme start */
.is-layout-constrained {
  --wp--style--global--content-size: 100dvw;
  padding: 0;
}
/* For Twenty Twenty-[<year>] theme end */
.theme-twentytwentytwo .wp-site-blocks {
  padding: 0;
}
/* For Twenty Twenty-One theme */
.wpcf7-form input.wpcf7-form-control.btn-primary:is([type="submit"]) {
  background-color: var(--primary);
}
.theme-twentytwentyone {
  --responsive--aligndefault-width: 100dvw;
  --gender-circle: 6px;
  --gender-check: 10px;
  --apps-circle: 6px;
  --apps-check: 7px;
}
.theme-oceanwp {
  --gender-circle: -1px;
  --gender-check: 3px;
  --apps-circle: -1px;
  --apps-check: 1px;
}
.theme-neve .wpcf7-form input.wpcf7-form-control:not([type="submit"]):focus {
  box-shadow: none;
}
/* Kadence theme start */
.theme-kadence :is(.entry-content-wrap, .content-container) {
  padding-inline: 0; /* So that content take full width */
}
/* Increase specificity */
form.wpcf7-form {
  margin-block: var(--form-margin-Y);
}
/* Kadence theme end */
.wpcf7-form {
  padding: var(--form-padding);
  box-shadow: var(--form-shadow);
  max-width: var(--form-width);
  margin-block: var(--form-margin-Y);
  margin-inline: var(--form-margin-X);
  background-color: var(--form-bg-color);
}
.wpcf7-form p br {
  display: none;
}
.wpcf7-form p {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 1.3125rem;
}
.wpcf7-form label {
  color: var(--primary);
  display: block;
  font-size: var(--form-label-fs);
  margin-bottom: var(--form-label-mb);
}
.wpcf7-form .wpcf7-form-control-wrap {
  display: block;
  width: 100%;
}
.wpcf7-form input.wpcf7-form-control:not([type="submit"]) {
  border: none;
  border-bottom: var(--border);
  transition: border 0.3s linear;
  background-color: transparent;
  padding-block: 0;
  width: 100%;
}
.wpcf7-form input[type="submit"] {
  border: none;
  background-color: var(--primary);
  color: var(--white);
  text-transform: var(--submit-button-text);
  letter-spacing: 2px;
  margin-inline: auto;
  width: var(--submit-button-width);
  transition: background-color 0.3s linear;
  border-radius: var(--submit-button-border-radius);
  padding: var(--submit-button-padding);
}
.wpcf7-form .btn-primary:hover {
  background-color: var(--primary-dark);
}

/* For select element */
.wpcf7-form [data-name="favorite-browser"] {
  position: relative;
  height: 45px;
  width: 100%;
}

/* Creates the Triangle Start */
/*
Notes: Not valid syntax
* :is(::before, ::after)
* tag:is(::before, ::after)
* :is(tag::before, tag::after)
*/
.wpcf7-form [data-name="favorite-browser"]::before,
.wpcf7-form [data-name="favorite-browser"]::after {
  content: "";
  position: absolute;
  pointer-events: none;
}
.wpcf7-form [data-name="favorite-browser"]::before {
  top: 1px;
  right: 1px;
  bottom: 1px;
  width: 30px;
  background-color: var(--primary-light);
}
.wpcf7-form [data-name="favorite-browser"]::after {
  top: 0;
  width: 0;
  height: 0;
  right: 10px;
  bottom: 0;
  margin: auto;
  border-style: solid;
  border-width: 5px 5px 0 5px;
  border-color: var(--white) transparent transparent transparent;
}
/* Creates triangle End */
.wpcf7-form [data-name="favorite-browser"] select {
  background-color: var(--lighter-gray);
  color: var(--darker-gray);
  border: 1px solid var(--primary-light);
  height: 100%;
  width: 100%;
  cursor: pointer;
  padding: 0 45px 0 15px;
  appearance: none;
}
[data-name="favorite-browser"] select::-ms-expand {
  display: none;
}
[data-name="favorite-browser"] select:focus {
  outline: none;
}

/* Radio and checkbox COMMON PROPERTY start */
.wpcf7-list-item {
  margin: 0;
}
.cu-gender,
.cu-js-framework,
.cu-css-framework,
.cu-frequent-apps,
.cu-frequent-sports {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  flex-direction: var(--direction, row);
}
:is(.cu-js-framework, .cu-css-framework, .cu-frequent-sports)
  :is(input[type="radio"], input[type="checkbox"])
  + :is(.wpcf7-list-item-label, span) {
  color: var(--darker-gray);
  display: inline-block;
  cursor: pointer;
  transition: background-color 0.3s linear;
  padding: var(--js-css-sports-padding);
}
:is(
    .cu-gender,
    .cu-js-framework,
    .cu-css-framework,
    .cu-frequent-apps,
    .cu-frequent-sports,
    .cu-acceptance
  )
  :is(input[type="radio"], input[type="checkbox"]) {
  position: absolute;
  z-index: 1;
  display: inline-block;
  opacity: 0;
}
:is(.cu-gender, .cu-frequent-apps)
  :is(input[type="radio"], input[type="checkbox"]) {
  height: var(--gender-apps-height);
}
.cu-gender input[type="radio"] {
  width: var(--gender-apps-width);
}
:is(.cu-js-framework, .cu-css-framework, .cu-frequent-sports)
  :is(input[type="radio"], input[type="checkbox"]) {
  height: var(--js-css-sports-height);
}
:is(.cu-css-framework, .cu-frequent-apps)
  :is(input[type="radio"], input[type="checkbox"]) {
  width: var(--css-apps-width);
}
:is(.cu-js-framework, .cu-frequent-sports)
  :is(input[type="radio"], input[type="checkbox"]) {
  width: var(--js-sports-height);
}
:is(.cu-gender, .cu-frequent-apps)
  :is(input[type="radio"], input[type="checkbox"])
  + span {
  position: relative;
  padding-left: 25px;
  cursor: pointer;
}
:is(.cu-gender, .cu-frequent-apps)
  :is(input[type="radio"], input[type="checkbox"])
  + span::before,
:is(.cu-gender, .cu-frequent-apps)
  :is(input[type="radio"], input[type="checkbox"])
  + span::after,
.cu-acceptance .wpcf7-list-item-label::before {
  content: "";
  position: absolute;
}
:is(.cu-gender, .cu-frequent-apps)
  :is(input[type="radio"], input[type="checkbox"]):checked
  + span::after {
  opacity: 1;
}
:is(.cu-js-framework, .cu-css-framework, .cu-frequent-sports)
  :is(input[type="radio"], input[type="checkbox"]):checked
  + :is(.wpcf7-list-item-label, span) {
  color: var(--white);
  background-color: var(--primary);
}
.wpcf7-form input.wpcf7-form-control:not([type="submit"]):focus,
.wpcf7-form input[type="submit"]:active {
  border: none;
  outline: none;
}
.wpcf7-form input.wpcf7-form-control:not([type="submit"]):focus {
  border-bottom: var(--border-primary);
}
/* Radio and checkbox COMMON PROPERTY end */

/* For gender */
.cu-gender input[type="radio"] + span::before {
  display: inline-block;
  width: 18px;
  height: 18px;
  left: 0;
  top: var(--gender-circle);
  border: var(--border);
  border-radius: 100%;
  background-color: var(--white);
}
.cu-gender input[type="radio"] + span::after {
  display: inline-block;
  width: 10px;
  height: 10px;
  top: var(--gender-check);
  left: 4px;
  opacity: 0;
  background-color: var(--primary);
  border-radius: 100%;
  transition: background-color 0.2s linear;
}

/* For js framework */
.cu-js-framework input[type="radio"] + .wpcf7-list-item-label {
  background-color: var(--lighter-gray);
  border: var(--border-primary);
}

/* For css framework */
.cu-css-framework {
  background-color: var(--lighter-gray);
  border: var(--border-primary);
  padding: 5px 10px;
}

/* For frequent apps */
.cu-frequent-apps input[type="checkbox"] + span::before {
  left: 0;
  top: var(--apps-circle);
  width: 18px;
  height: 18px;
  border: var(--border);
  border-radius: 3px;
  background-color: var(--white);
}
.cu-frequent-apps input[type="checkbox"] + span::after {
  content: "\f00c";
  font-family: "Font Awesome 5 Free";
  font-weight: 900;
  position: absolute;
  top: var(--apps-check);
  left: 3px;
  font-size: 14px;
  line-height: 1;
  color: var(--primary);
  opacity: 0;
  transform: scale(0);
  transition: background-color 0.2s linear;
}
.cu-frequent-apps input[type="checkbox"]:checked + span::after {
  transform: scale(1);
}

/* For sports */
.cu-frequent-sports input[type="checkbox"] + span {
  background-color: var(--lighter-gray);
  border: var(--border-primary);
}

/* For switch */
.wpcf7-form .switch ~ .wpcf7-form-control-wrap {
  position: relative;
  width: var(--switch-container-width);
  height: var(--switch-container-height);
}
.cu-acceptance input[type="checkbox"] {
  width: var(--switch-container-width);
  height: var(--switch-container-height);
  top: 0;
  left: 0;
}
.cu-acceptance .wpcf7-list-item-label {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  color: var(--switch-container);
  background-color: var(--switch-container);
  border-radius: var(--switch-container-border-radius);
  transition: background-color 0.3s linear;
}
.cu-acceptance .wpcf7-list-item-label::before {
  height: var(--switch-circle-size);
  width: var(--switch-circle-size);
  left: var(--switch-circle-left-position);
  top: var(--switch-circle-top-position);
  background-color: var(--switch-circle);
  border-radius: var(--switch-circle-border-radius);
  transition: background-color 0.3s linear;
}
.cu-acceptance input[type="checkbox"]:checked + .wpcf7-list-item-label {
  background-color: var(--primary);
}
.cu-acceptance input[type="checkbox"]:checked + .wpcf7-list-item-label::before {
  transform: translateX(18px);
}

/* For foldable phones */
@media screen and (max-width: 350px) {
  :is(.cu-js-framework, .cu-css-framework, .cu-frequent-sports)
    :is(input[type="radio"], input[type="checkbox"]) {
    width: calc(100% - 10px);
  }
  :is(.cu-js-framework, .cu-css-framework, .cu-frequent-sports)
    :is(
      :is(input[type="radio"], input[type="checkbox"]),
      :is(input[type="radio"], input[type="checkbox"]):checked
    )
    + :is(.wpcf7-list-item-label, span) {
    width: 100%;
  }
  :root {
    --direction: column;
  }
}

/* For tablet and desktop */
@media screen and (min-width: 768px) {
  .wpcf7-form > :is(p:nth-child(2), p:nth-child(3)) {
    display: inline-block;
    width: 45%;
  }
  .wpcf7-form > p:nth-child(2) {
    margin-right: 8%;
  }
  .cu-css-framework input[type="radio"] {
    width: var(--css-tab-dek-width);
  }
}

```


## Task 5: The Magic of Live AJAX WooCommerce Product Search

Imagine being a magician, and your magic trick is to conjure up a live AJAX WooCommerce product search. But there's a twist - you have to perform this trick without using any plugins, only with the power of PHP code.

This isn't just any search - it's a live search. As soon as the user starts typing, the search results begin to appear, like magic. It's as if the search bar can read the user's mind, predicting what they're looking for before they even finish typing.

And the magic doesn't stop there. This live search is powered by AJAX, a powerful tool that allows the page to update without needing to be refreshed. It's like having a magic wand that can change the content of the page without disturbing anything else.

So, you roll up your sleeves and get to work, crafting this live AJAX WooCommerce product search with the precision and skill of a master magician. And when you're done, you step back and watch as your magic trick comes to life.

And there you have it - a beautiful, functional, and secure AJAX live search.
![The Magic of Live AJAX WooCommerce Product Search completed task](./assets/task-5/ajax-search.png 'The Magic of Live AJAX WooCommerce Product Search completed task')

AJAX search (css)

```css
.asearch select {
  padding: 0 1rem;
}
.asearch #keyword,
.asearch select,
.asearch #mybtn {
  border: 1px solid #e5e5e5;
}
form.asearch {
  width: 470px;
}
.asearch select {
  width: 40%;
}
.ast-primary-header-bar .ast-builder-grid-row.ast-grid-center-col-layout {
  grid-template-columns: max-content auto 1fr;
  grid-template-columns: max-content auto auto; /* New */
}
.ast-primary-header-bar .site-primary-header-wrap .ast-builder-grid-row {
  grid-column-gap: 10px;
}
.ast-primary-header-bar .ast-grid-right-center-section {
  display: none;
}
.ast-primary-header-bar .site-header-focus-item {
  padding: 0;
}
@media screen and (min-width: 900px) {
  .ast-primary-header-bar .ast-grid-right-section {
    max-width: max-content;
    justify-self: end;
  }
}
```

AJAX search (php)

```php
add_shortcode( 'asearch', 'asearch_func' );
function asearch_func( $atts ) {
    $atts = shortcode_atts( array(
        'source' => 'categories,product',
        'image' => 'true'
    ), $atts, 'asearch' );
static $asearch_first_call = 1;
$source = $atts["source"];
$image = $atts["image"];
$sForam = '<div class="search_bar">
    <form class="asearch" id="asearch'.$asearch_first_call.'" action="/" method="get" autocomplete="off">
        <input type="text" name="s" placeholder="Search ..." id="keyword" class="input_search" onkeyup="searchFetch(this)"><select><option value="All category" selected="selected">All category</option><option value="Clothing">Clothing</option><option value="Hoodies">Hoodies</option><option value="Albums">Albums</option><option value="Music">Music</option></select><button id="mybtn"><i class="fa-solid fa-magnifying-glass search-icon"></i></button>
    </form><div class="search_result" id="datafetch" style="display: none;">
        <ul>
            <li>Please wait..</li>
        </ul>
    </div></div>';
$javaScript = '<script>
function searchFetch(e) {
var datafetch = e.parentElement.nextSibling
if (e.value.trim().length > 0) { datafetch.style.display = "block"; } else { datafetch.style.display = "none"; }
const searchForm = e.parentElement;
e.nextSibling.value = "Please wait..."
var formdata'.$asearch_first_call.' = new FormData(searchForm);
formdata'.$asearch_first_call.'.append("source", "'.$source.'")
formdata'.$asearch_first_call.'.append("image", "'.$image.'")
formdata'.$asearch_first_call.'.append("action", "asearch")
AjaxAsearch(formdata'.$asearch_first_call.',e)
}
async function AjaxAsearch(formdata,e) {
  const url = "'.admin_url("admin-ajax.php").'?action=asearch";
  const response = await fetch(url, {
      method: "POST",
      body: formdata,
  });
  const data = await response.text();
if (data){	e.parentElement.nextSibling.innerHTML = data}else  {
e.parentElement.nextSibling.innerHTML = `<ul><a href="#"><li>Sorry, nothing found</li></a></ul>`
}}
document.addEventListener("click", function(e) { if (document.activeElement.classList.contains("input_search") == false ) { [...document.querySelectorAll("div.search_result")].forEach(e => e.style.display = "none") } else {if  (e.target.value.trim().length > 0) { e.target.parentElement.nextSibling.style.display = "block"}} })
</script>';
$css = '<style>form.asearch {display: flex;flex-wrap: nowrap;}
.asearch #mybtn {padding: 10px;cursor: pointer;background: none;}
.asearch .search-icon {color: #a0a0a0;}
div#datafetch {
    background: white;
    z-index: 10;
    position: absolute;
    overflow: auto;
    box-shadow: 0px 15px 15px #00000036;
    right: 0;
    left: 0;
    top: 50px;
}
div.search_bar {
    position: relative;
}

div.search_result ul a li {
    margin: 0px;
    padding: 5px 0px;
    padding-inline-start: 18px;
    color: #3f3f3f;
    font-weight: bold;
}
div.search_result li {
    margin-inline-start: 20px;
}
div.search_result ul {
    padding: 13px 0px 0px 0px;
    list-style: none;
    margin: auto;
}

div.search_result ul a {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 5px;
}
div.search_result ul a:hover {
    background-color: #f3f3f3;
}
.asearch input#keyword {
    width: 100%;
}
</style>';
if ( $asearch_first_call == 1 ){
	 $asearch_first_call++;
	 return "{$sForam}{$javaScript}{$css}"; } elseif  ( $asearch_first_call > 1 ) {
		$asearch_first_call++;
		return "{$sForam}"; }}

add_action('wp_ajax_asearch' , 'asearch');
add_action('wp_ajax_nopriv_asearch','asearch');
function asearch(){
    $the_query = new WP_Query( array( 'posts_per_page' => 10, 's' => esc_attr( $_POST['s'] ), 'post_type' =>  explode(",", esc_attr( $_POST['source'] )))  );
    if( $the_query->have_posts() ) :
        echo '<ul>';
        while( $the_query->have_posts() ): $the_query->the_post(); ?>
            <a href="<?php echo esc_url( post_permalink() ); ?>"><li><?php the_title();?></li>
<?php $image = wp_get_attachment_image_src( get_post_thumbnail_id(), 'single-post-thumbnail' );?>
<?php if ( $image[0] && trim(esc_attr( $_POST['image'] )) == "true" ) {  ?>  <img src="<?php the_post_thumbnail_url('thumbnail'); ?>" style="height: 60px;padding: 0px 5px;"> <?php }  ?> </a>
        <?php endwhile;
       echo '</ul>';
        wp_reset_postdata();
    endif;
    die();
}
```

References:

- [Task 1: Creating an Online Shop Page](https://resourcesone.blogspot.com/2023/12/design-stunning-woocommerce-shop.html)
- [Task 2: Enhance the Single Product Page](https://resourcesone.blogspot.com/2023/12/captivating-woocommerce-product-page.html)
- [Task 3: The Carousel Transformation](https://resourcesone.blogspot.com/2023/12/blog-post_26.html)
