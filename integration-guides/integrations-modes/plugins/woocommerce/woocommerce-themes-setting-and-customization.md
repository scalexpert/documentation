---
description: Themes & Templates guidelines
---

# 🆕 WooCommerce themes setting and customization

### Why do I need to do something?

The plugin "scalexpert"  override the natives WooCommerce templates to display the scalexpert financing on the following pages:\
\- product\
\- shopping cart\
\- order details (returned page after financing customer journey

{% hint style="warning" %}
Normally, the standard "[hierarchy mechanism](https://developer.wordpress.org/themes/templates/template-hierarchy/)" of Wordpress templates should ensure that scalexpert code is active. But we recommend strongly to test the render of these pages especially if you are using a specific or customized theme or even a [standard theme](https://wordpress.org/themes/) using "[blocks](https://developer.wordpress.org/themes/getting-started/what-is-a-theme/#block-themes)" like for instance  the "Twenty TwentyFour" theme.&#x20;
{% endhint %}

### What do I need if something is wrong!

You have encountered issued when rendering these pages, don't panic :worried: let us guide you in the diagnosis to solve your issue.

First, identify the theme you are using on your back-office "themes" menu:

<figure><img src="../../../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Wordpress Theme menu management</p></figcaption></figure>

&#x20;Second, verify your in "WooCommerce" menu "setting/advanced"  that all pages used are fill-in:

<figure><img src="../../../../.gitbook/assets/image (2).png" alt=""><figcaption><p>WooCommerce advanced pages setting</p></figcaption></figure>

And also in the "WooCommerce" status menu:

<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption><p>WooCommerce status menu</p></figcaption></figure>

Once, your theme identified you must found your "[theme type](https://developer.wordpress.org/themes/getting-started/what-is-a-theme/#theme-types)":  "classic" or "block". According that "type" the method to customize your theme will be different.

### Customize a "Block" type theme

Customization of "block" type theme can be done in the wordpress back office menu "[Appearance/editor](https://developer.wordpress.org/themes/templates/templates/#editing-templates)"&#x20;

We will demonstrate the setting with the standard "Twenty-twenty-four" theme. This theme use directly "woocommerce blocks" and therefore bypass the customization done by scalexpert plugin. We will correct this by overidden some part of the coding.

Open the editor from "appearance/editor" menu&#x20;

<figure><img src="../../../../.gitbook/assets/image (4).png" alt=""><figcaption><p>editor menu</p></figcaption></figure>

Once opened, navigate into "template" menu to open the templates that need to be customized:

* single product
* cart
* check-out
* my account

Select the template, open it then go to the "code editor" menu to access the code of the template. &#x20;

Then replace existing code by the following:

{% hint style="info" %}
Samples are to be adapted according your theme used. For instance replace "theme":"twentytwentyfour" by "theme":"YOUR\_THEME".
{% endhint %}

{% code title="single-product template" %}
```
<!-- wp:template-part {"slug":"header","theme":"twentytwentyfour"} /-->
<div class="wp-block-group woocommerce product is-layout-flow wp-block-group-
is-layout-flow">
<div class="wp-block-group has-global-padding is-layout-constrained wp-
block-group-is-layout-constrained">
<!-- wp:woocommerce/legacy-template {"template":"single-product"}
/-->
</div>
</div>
<!-- wp:template-part {"slug":"footer","theme":"twentytwentyfour"} /-->
```
{% endcode %}

<figure><img src="../../../../.gitbook/assets/1-woocommerce-edit-templates (2).gif" alt=""><figcaption><p>Replace code of a template through editor</p></figcaption></figure>

After recording, you should see appear the "financing" options in the product page: &#x20;

<figure><img src="../../../../.gitbook/assets/image (17).png" alt=""><figcaption><p>Resulting product page after editor change showing the scalexpert financing options</p></figcaption></figure>

{% hint style="info" %}
However, it works this solution is incomplete as all "HTML" balises for instance for images blocks are not inherit from the original "TwentytwentyFor" theme. This is only for demonstration purpose and we let you finishing the job :wink: &#x20;
{% endhint %}

Repeat the same operation for the other templates:

{% code title="checkout template" %}
```
[woocommerce_checkout]
```
{% endcode %}

{% code title="cart template" %}
```
[woocommerce_cart]
```
{% endcode %}

{% code title="my account template" %}
```
[woocommerce_my_account]
```
{% endcode %}

### Customize a "Classic" type theme

The WooCommerce template that have been overridden are present in the wordpress directory "[/wp-content/plugins/woo-scalexpert/woocommerce](https://github.com/scalexpert/scalexpert-woocommerce/tree/main/woo-scalexpert/woocommerce)"&#x20;

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption><p>Woocommerce templates overridden </p></figcaption></figure>

Code overridden are marked with a commentaire "SG Paiement en plusieurs fois".

{% code title="sample of code overridden " lineNumbers="true" %}
```php
	...
	<?php else : ?>
	<!--  SG Paiement en plusieurs fois -->
	<p class="woocommerce-notice woocommerce-notice--<?= $classNotice ?> woocommerce-thankyou-order-received">
		<?php
			/**  SG Paiement en plusieurs fois */
			if ( $orderData['payment_method'] == "scalexpert" ) {
				echo apply_filters(
					'woocommerce_thankyou_order_received_text',
					$API_CALL['TextStatus'],
					$order );
			} else {
				echo apply_filters(
					'woocommerce_thankyou_order_received_text',
					esc_html__( 'Thank you. Your order has been received.',
						'woocommerce' ),
					$order );
			}
			/**  SG Paiement en plusieurs fois */
		?>
	</p>
	<!--  SG Paiement en plusieurs fois -->
	...
```
{% endcode %}

{% hint style="info" %}
Don't touch it directly but copy them in your theme directory under "/wp-content/themes/yourtheme/woocommerce/..."  and keeping the same structure as found in a the source.
{% endhint %}

For more information on woocommerce templates structure directory see the [related documentation](https://woo.com/document/template-structure/#how-to-edit-files).

### Do that resolve your issue?

We hope this tutorial will help you on the resolution of issues you may encountered in the customization of your theme.&#x20;

{% hint style="info" %}
No, we are very sorry for that! Because Wordpress theme are quite complex and we can't ensure to cover all the customization cases. If you are a developer we recommend you to read the related "Handbook" from wordpress [https://developer.wordpress.org/themes/](https://developer.wordpress.org/themes/)  and also [https://woo.com/document/template-structure/](https://woo.com/document/template-structure/) . Otherwise, we strongly recommend you to look at your IT or your theme support maintenance team.
{% endhint %}
