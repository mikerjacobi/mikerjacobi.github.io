---
layout: post
title: Shopify and Aardvark Hot Sauce
---

This post is about Shopify, Dropshipping, and selling Aardvark Hot Sauce!

Working on the design app, I needed to understand how to purchase products from a manufacturer on behalf of a client. The model we wanted to use was dropshipping - directly delivering products from a manufacturer's warehouse to the client's address. This post describes how I went about that and a proof of concept.

Dropshipping is when a customer purchases something from a merchant, which causes the merchant to place a Purchase Order (PO) with the manufacturer to be delivered directly from the manufacturer to client. This model has some pros and cons. Some pros are that the merchant doesn't have to hold inventory and can source products across many manufacturers. Some cons are that the merchant can't leverage bulk pricing because each PO is a one off, shipped directly to the customer. Buying and holding inventory is tough for a few reasons - you have to have the capital to buy the product up front, you have to physically store it somewhere, and you need the capability to receive inventory and ship it back out. The bet you're making as a dropshipper is that avoiding these costs is more advantageous than the benefits of buying in bulk. Given we had no capital to buy products up front and nowhere to store inventory even if we did, dropshipping was the only way it seemed possible to get started.

## Shopify

This proof of concept centers around Shopify. Shopify provides two things, 1) customer facing infrastructure like product pages, a shopping cart, and payment options, and 2) a merchant interface to manage a product line and handle orders. Shopify generates a product page for each product you define in the merchant interface, which allows customers to view them, add them to a cart, and purchase them from an invoice page. Alternatively, you can modify a virtual shopping cart with Shopify API calls and produce the same invoice page programmatically, more on this coming. 

## Reseller Account

I found a hot sauce wholesaler, Pepper Explosion, which sells hundreds of varieties of hot sauces and other condiments in bulk. I spoke to an account manager of theirs, who granted us a reseller account. We discussed how dropshipping would work and orders would come in. I was kind of amazed at how subjective the Pepper Explosion reseller application process was. 

I found my go to hot sauce, Aardvark, on Pepper Explosion's site and created a Shopify product listing for it in the merchant interface. I listed it for $6.00, and Pepper Explosion's cut was $4.68. Shopify has an extensive plugin system, and one I came across, called Simple Purchase Orders (SPO), let's you manage suppliers and automatically generate and send purchase orders for them when a customer purchases a product. So, I filled in Pepper Explosion's supplier information and associated Aardvark Hot Sauce with them. This makes it so whenever Aardvark is purchasd, Pepper Explosion automatically receives an order with the customers address, and they begin shipping the product. 

## Shopify's API

Shopify has support for a URL structure that has query string parameters that map product listing IDs to product quantities. This means if you could write an app that knew how to produce the correct URL, you could programmatically generate invoice pages and send them to customers. For example, you can essentially generate a URL like: merchant.shopify.com?hat=1;shirt=2, which will load an invoice page with one hat and two shirts, where those hats and shirts are listings in your Shopify profile. This would let them see the line items, taxes, and total cost, as well as an input form for their credit card. I built a prototype to generate URLs of this form. The app worked by querying Shopify for product listings, and then creating a list of them with buttons to modify the quantity of each. Then there was a Generate button that produced the invoice URL. 

The prototype was interesting because of the implications. For our purposes, we were excited about using a similar process in a virtual 3D environment. The idea was that there would be 3D models of each product listing, and when you clicked them, you'd have the ability to add a product to your cart. Then there'd be a Checkout button that let you purchase the items that you had seen 3D models of. A full, virtual 3D shopping experience, with products and delivery managed via Shopify.

## Conclusion

In the end, I bought exactly one bottle of Aardvark this way. I paid $6 for the hot sauce and another $6 for taxes and shipping. Oops. Not super viable for a single bottle of Aardvark.
