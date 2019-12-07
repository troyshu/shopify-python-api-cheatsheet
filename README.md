# Shopify Python API Cheatsheet

# Introduction

After a lot of frustration with the [lack of documentation](https://github.com/Shopify/shopify_python_api/issues/132), I compiled this cheatsheet that should help when developing with the Shopify API Python wrapper.

The methods are derived from the [Github repository](https://github.com/Shopify/shopify_python_api) for the wrapper. I’ve included the most common JSON responses, but more detailed examples are [available here](https://github.com/Shopify/shopify_python_api/tree/master/test/fixtures).

Use the pop-out menu on the left to quick-nav to the different sections.

If you think anything’s missing, leave a comment.

[Mathew](https://www.linkedin.com/in/mathewkeegan) @ [Kano](http://www.kano.me)


----------
# Article
## Methods

Create Article

    shopify.Article({'blog_id':1008414260})
    article.save()

Get Article

    shopify.Article.find(6242736)

Update Article

    shopify.Article.find(6242736)
    article.save()

Get Articles

    shopify.Article.find()

Get Articles Namespaced

    shopify.Article.find(6242736, blog_id=1008414260)

Get Authors

    shopify.Article.authors()

Get Authors for Blog ID

    shopify.Article.authors(blog_id=1008414260)

Get Tags

    shopify.Article.tags()

Get Tags for Blog ID

    shopify.Article.tags(blog_id=1008414260)

Get Popular Tags

    shopify.Article.tags(popular=1, limit=1)


## JSON

Article

    {
      "article": {
      "author": "Shopify",
      "blog_id": 1008414260,
      "body_html": null,
      "created_at": "2012-07-06T13:57:28-04:00",
      "id": 6242736,
      "published_at": "2012-07-06T13:57:28-04:00",
      "summary_html": null,
      "title": "First Post",
      "updated_at": "2012-07-06T13:57:51-04:00",
      "user_id": null,
      "tags": "consequuntur, cupiditate, repellendus"
      }
    }
# Asset
## Methods

Get Assets

    shopify.Asset.find()

Get Asset

    shopify.Asset.find('templates/index.liquid')

Update Asset

    v = shopify.Asset.find('templates/index.liquid')
    v.save()

Get Assets Namespaced

    shopify.Asset.find(theme_id = 1)

Get Asset Namespaced

    shopify.Asset.find('templates/index.liquid', theme_id=1)

Update Asset Namespaced

    v = shopify.Asset.find('templates/index.liquid', theme_id=1)
    v.save()

Delete Asset Namespaced

    v = shopify.Asset.find('templates/index.liquid', theme_id=1)
    v.destroy()


## JSON

Asset

    {
      "asset": {
      "created_at": "2010-07-12T15:31:50-04:00",
      "updated_at": "2010-07-12T15:31:50-04:00",
      "public_url": null,
      "value": "<!-- LIST 3 PER ROW -->\n<h2>Featured Products</h2>\n<table id=\"products\" cellspacing=\"0\" cellpadding=\"0\">\n{% tablerow product in collections.frontpage.products cols:3  %}\n   <a href=\"{{product.url}}\">{{ product.featured_image | product_img_url: 'small' | img_tag }}</a>\n   <h3><a href=\"{{product.url}}\">{{product.title}}</a></h3>\n   <ul class=\"attributes\">\n     <li><span class=\"money\">{{product.price_min | money}}</span></li>\n   </ul>\n{% endtablerow %}\n</table>\n<!-- /LIST 3 PER ROW  -->\n\n  <div id=\"articles\">\n  \t{% assign article = pages.frontpage %}\n\n    <div class=\"article\">\n    {% if article.content != \"\" %}\n\t\t  <h3>{{ article.title }}</h3>\n      <div class=\"article-body textile\">\n  \t\t  {{ article.content }}\n  \t\t</div>\n  \t{% else %}\n      <div class=\"article-body textile\">\n  \t  In <em>Admin &gt; Blogs &amp; Pages</em>, create a page with the handle <strong><code>frontpage</code></strong> and it will show up here.<br />\n  \t  {{ \"Learn more about handles\" | link_to \"http://wiki.shopify.com/Handle\" }}\n      </div>\n  \t{% endif %}\n    </div>\n\n  </div>\n\n",
      "key": "templates/index.liquid"
      }
    }
# Blog
## Methods

Create Blog

    shopify.Blog.create({'title': "Test Blog"})


## JSON
    {
      "blog": {
      "handle": "test-blog",
      "created_at": "2012-01-10T17:45:19-05:00",
      "title": "Test Blog",
      "template_suffix": null,
      "updated_at": "2012-01-10T17:45:19-05:00",
      "feedburner_location": null,
      "id": 1008414260,
      "feedburner": null,
      "commentable": "no"
      }
    }
# Carrier Service
## Methods

Create Carrier Service

    shopify.CarrierService.create({'name': "Some Postal Service"})

Get Carrier Service

    shopify.CarrierService.find(123456)

Set Format Attribute

    shopify.CarrierService()
    carrier_service.format = "json"


## JSON
    {
      "carrier_service": {
        "name": "Some Postal Service",
        "id": 123456,
        "callback_url": "http://google.com",
        "format": "json",
        "service_discovery": true
      }
    }
# Cart
## Methods

Return All Carts

    shopify.Cart.find()


## JSON
    {
      "carts": [
        {
          "id": 2,
          "note": null,
          "token": "3eed8183d4281db6ea82ee2b8f23e9cc",
          "updated_at": "2012-02-13T14:39:37-05:00",
          "line_items": 
          [
            {
              "id": 1,
              "title": "test",
              "price": "1.00",
              "line_price": "1.00",
              "quantity": 1,
              "sku": "",
              "grams": 1000,
              "vendor": "test",
              "variant_id": 1
            }
          ]
        },
        {
          "id": 1,
          "note": "",
          "token": "49801807939c296be1e9a4bf6783a705",
          "updated_at": "2012-02-13T14:39:12-05:00",
          "line_items":[
            {
              "id": 1,
              "title": "test",
              "price": "1.00",
              "line_price": "1.00",
              "quantity": 1,
              "sku": "",
              "grams": 1000,
              "vendor": "test",
              "variant_id": 1
            }
          ]
        }
      ]
    }
# Checkout
## Methods

Return All Checkouts

    shopify.Checkout.find()


## JSON
    {
      "checkouts": [
        {
          "buyer_accepts_marketing": false,
          "cart_token": "68778783ad298f1c80c3bafcddeea02f",
          "closed_at": null,
          "completed_at": null,
          "created_at": "2012-10-12T07:05:27-04:00",
          "currency": "USD",
          "email": "bob.norman@hostmail.com",
          "gateway": null,
          "id": 450789469,
          "landing_site": null,
          "note": null,
          "referring_site": null,
          "shipping_lines": [
            {
              "title": "Free Shipping",
              "price": "0.00",
              "code": "Free Shipping",
              "source": "shopify"
            }
          ],
          "source": null,
          "source_identifier": null,
          "source_name": "web",
          "source_url": null,
          "subtotal_price": "398.00",
          "taxes_included": false,
          "token": "2a1ace52255252df566af0faaedfbfa7",
          "total_discounts": "0.00",
          "total_line_items_price": "398.00",
          "total_price": "409.94",
          "total_tax": "11.94",
          "total_weight": 400,
          "updated_at": "2012-10-12T07:05:27-04:00",
          "line_items": [
            {
              "applied_discounts": [
    
              ],
              "compare_at_price": null,
              "fulfillment_service": "manual",
              "gift_card": false,
              "grams": 200,
              "id": 49148385,
              "line_price": "199.00",
              "price": "199.00",
              "product_id": 632910392,
              "properties": null,
              "quantity": 1,
              "requires_shipping": true,
              "sku": "IPOD2008RED",
              "tax_lines": [
    
              ],
              "taxable": true,
              "title": "IPod Nano - 8GB",
              "variant_id": 49148385,
              "variant_title": "Red",
              "vendor": "Apple"
            },
            {
              "applied_discounts": [
    
              ],
              "compare_at_price": null,
              "fulfillment_service": "manual",
              "gift_card": false,
              "grams": 200,
              "id": 808950810,
              "line_price": "199.00",
              "price": "199.00",
              "product_id": 632910392,
              "properties": null,
              "quantity": 1,
              "requires_shipping": true,
              "sku": "IPOD2008PINK",
              "tax_lines": [
    
              ],
              "taxable": true,
              "title": "IPod Nano - 8GB",
              "variant_id": 808950810,
              "variant_title": "Pink",
              "vendor": "Apple"
            }
          ],
          "name": "#450789469",
          "note_attributes": [
            {
              "name": "custom engraving",
              "value": "Happy Birthday"
            },
            {
              "name": "colour",
              "value": "green"
            }
          ],
          "discount_codes": [
            {
              "code": "TENOFF",
              "amount": "10.00"
            }
          ],
          "abandoned_checkout_url": "https://checkout.local/orders/690933842/2a1ace52255252df566af0faaedfbfa7?recovered=1",
          "tax_lines": [
            {
              "price": "11.94",
              "rate": 0.06,
              "title": "State Tax"
            }
          ],
          "billing_address": {
            "address1": "Chestnut Street 92",
            "address2": "",
            "city": "Louisville",
            "company": null,
            "country": "United States",
            "first_name": "Bob",
            "last_name": "Norman",
            "latitude": "45.41634",
            "longitude": "-75.6868",
            "phone": "555-625-1199",
            "province": "Kentucky",
            "zip": "40202",
            "name": "Bob Norman",
            "country_code": "US",
            "province_code": "KY"
          },
          "shipping_address": {
            "address1": "Chestnut Street 92",
            "address2": "",
            "city": "Louisville",
            "company": null,
            "country": "United States",
            "first_name": "Bob",
            "last_name": "Norman",
            "latitude": "45.41634",
            "longitude": "-75.6868",
            "phone": "555-625-1199",
            "province": "Kentucky",
            "zip": "40202",
            "name": "Bob Norman",
            "country_code": "US",
            "province_code": "KY"
          },
          "customer": {
            "accepts_marketing": false,
            "created_at": "2014-03-07T16:12:37-05:00",
            "email": "bob.norman@hostmail.com",
            "first_name": "Bob",
            "id": 207119551,
            "last_name": "Norman",
            "last_order_id": null,
            "multipass_identifier": null,
            "note": null,
            "orders_count": 0,
            "state": "disabled",
            "total_spent": "0.00",
            "updated_at": "2014-03-07T16:12:37-05:00",
            "verified_email": true,
            "tags": "",
            "last_order_name": null,
            "default_address": {
              "address1": "Chestnut Street 92",
              "address2": "",
              "city": "Louisville",
              "company": null,
              "country": "United States",
              "first_name": null,
              "id": 207119551,
              "last_name": null,
              "phone": "555-625-1199",
              "province": "Kentucky",
              "zip": "40202",
              "name": null,
              "province_code": "KY",
              "country_code": "US",
              "country_name": "United States",
              "default": true
            }
          }
        }
      ]
    }
# Customer Saved Search
## Methods

Load Customer Saved Search

    shopify.CustomerSavedSearch.find(8899730)
## JSON
    {
      "customer_saved_search": {
        "created_at": "2013-01-21T13:26:12-05:00",
        "id": 8899730,
        "name": "Accepts Marketing",
        "updated_at": "2013-01-21T13:26:12-05:00",
        "query": "accepts_marketing:1"
      }
    }
# Customer
## Methods

Create Customer

    customer = shopify.Customer()
    customer.save()

Get Customer

    customer = shopify.Customer.find(207119551)

Search

    shopify.Customer.search(query='Bob country:United States')


## JSON
    {
      "customer": {
        "accepts_marketing": false,
        "created_at": "2015-05-27T18:11:24-04:00",
        "email": "bob.norman@hostmail.com",
        "first_name": "Bob",
        "id": 207119551,
        "last_name": "Norman",
        "last_order_id": 450789469,
        "multipass_identifier": null,
        "note": null,
        "orders_count": 1,
        "state": "disabled",
        "tax_exempt": false,
        "total_spent": "41.94",
        "updated_at": "2015-05-27T18:11:24-04:00",
        "verified_email": true,
        "tags": "",
        "last_order_name": "#1001",
        "default_address": {
          "address1": "Chestnut Street 92",
          "address2": "",
          "city": "Louisville",
          "company": null,
          "country": "United States",
          "first_name": null,
          "id": 207119551,
          "last_name": null,
          "phone": "555-625-1199",
          "province": "Kentucky",
          "zip": "40202",
          "name": "",
          "province_code": "KY",
          "country_code": "US",
          "country_name": "United States",
          "default": true
        },
        "addresses": [
          {
            "address1": "Chestnut Street 92",
            "address2": "",
            "city": "Louisville",
            "company": null,
            "country": "United States",
            "first_name": null,
            "id": 207119551,
            "last_name": null,
            "phone": "555-625-1199",
            "province": "Kentucky",
            "zip": "40202",
            "name": "",
            "province_code": "KY",
            "country_code": "US",
            "country_name": "United States",
            "default": true
          }
        ]
      }
    }
# Discount
## Methods

Create Discount

     shopify.Discount.create({
                "discount_type": "shipping",
                "code": "quidagis?",
                "starts_at": "2015-08-23T00:00:00-04:00",
                "ends_at": "2015-08-27T23:59:59-04:00",
                "usage_limit": 20
            })

Fetch Discounts

    shopify.Discount.find()

Disable Discount

    discount = shopify.Discount.find(992807812)
    discount.disable()


## JSON
    {
      "discount": {
        "id": 992807812,
        "code": "quidagis?",
        "value": "9999999.00",
        "ends_at": "2015-08-27T23:59:59-04:00",
        "starts_at": "2015-08-23T00:00:00-04:00",
        "status": "enabled",
        "usage_limit": 20,
        "minimum_order_amount": "0.00",
        "applies_to_id": null,
        "applies_once": false,
        "discount_type": "shipping",
        "applies_to_resource": null,
        "times_used": 0
      }
    }
# Fulfillment Service
## Methods

Create Fulfillment Service

    shopify.FulfillmentService.create({'name': "SomeService"})

Get Fulfillment Service

    shopify.FulfillmentService.find(123456)

Get All Fulfillment Services

    shopify.FulfillmentService.find(scope="all")

Set Format Attribute

    fulfillment_service = shopify.FulfillmentService()
    fulfillment_service.format = "json"


## JSON
    {
      "fulfillment_service": {
        "name": "SomeService",
        "id": 123456,
        "inventory_management": false,
        "tracking_support": true,
        "requires_shipping_method": false,
        "format": "json"
      }
    }
# Gift Card
## Methods

Create Gift Card

    shopify.GiftCard.create({'code': 'd7a2bcggda89c293', 'note': "Gift card note."})

Get Gift Cards

    shopify.GiftCard.find()

Disable Gift Card

    gift_card = shopify.GiftCard.find(4208208)
    gift_card.disable()


## JSON
    {
      "gift_card": {
        "api_client_id": null,
        "balance": "25.00",
        "created_at": "2015-05-11T10:16:40+10:00",
        "currency": "AUD",
        "customer_id": null,
        "disabled_at": null,
        "expires_on": null,
        "id": 4208208,
        "initial_value": "25.00",
        "line_item_id": null,
        "note": "Gift card note.",
        "template_suffix": null,
        "updated_at": "2015-05-11T15:13:15+10:00",
        "user_id": 123456,
        "last_characters":"c293",
        "order_id":null
      }
    }
# Image
## Methods

Create Image

    image = shopify.Image({'product_id':632910392})
    image.position = 1
    image.attachment = "R0lGODlhbgCMAPf/APbr48VySrxTO7IgKt2qmKQdJeK8lsFjROG5p/nz7Zg3MNmnd7Q1MLNVS9GId71hSJMZIuzTu4UtKbeEeakhKMl8U8WYjfr18YQaIbAf=="
    image.save()

Create Image then Add Parent ID

    image = shopify.Image()
    image.position = 1
    image.product_id = 632910392
    image.attachment = "R0lGODlhbgCMAPf/APbr48VySrxTO7IgKt2qmKQdJeK8lsFjROG5p/nz7Zg3MNmnd7Q1MLNVS9GId71hSJMZIuzTu4UtKbeEeakhKMl8U8WYjfr18YQaIbAf=="
    image.save()

Get Images

    shopify.Image.find(product_id=632910392)

Get Image

    shopify.Image.find(850703190, product_id=632910392)

Get Metafields for Image

    image = shopify.Image(attributes = { 'id': 850703190, 'product_id': 632910392 })
    metafields = image.metafields()


## JSON
    {
      "image": {
        "created_at": "2014-01-10T16:15:40-05:00",
        "id": 850703190,
        "position": 1,
        "product_id": 632910392,
        "updated_at": "2014-01-10T16:15:40-05:00",
        "src": "http://cdn.shopify.com/s/files/1/0006/9093/3842/products/ipod-nano.png?v=1389388540"
      }
    }
# Locations
## Methods

Get Locations

    shopify.Location.find()

Get Location

    shopify.Location.find(487838322)


## JSON
    {
      "location": {
        "id": 487838322,
        "name": "Fifth Avenue AppleStore",
        "deleted_at": null,
        "address1": null,
        "address2": null,
        "city": null,
        "zip": null,
        "province": null,
        "country": "US",
        "phone": null,
        "created_at": "2015-12-08T11:44:58-05:00",
        "updated_at": "2015-12-08T11:44:58-05:00",
        "country_code": "US",
        "country_name": "United States",
        "province_code": null
      }
    }
# Order Risk
## Methods

Create Order Risk

    v = shopify.OrderRisk({'order_id':450789469})
    v.save()

Get Order Risks

    shopify.OrderRisk.find(order_id=450789469)

Get Order Risk

    shopify.OrderRisk.find(284138680, order_id=450789469)

Delete Order Risk

    v = shopify.OrderRisk.find(284138680, order_id=450789469)
    v.destroy()

Delete Order Risk

    v = shopify.OrderRisk.find(284138680, order_id=450789469)
    v.position = 3
    v.save()


## JSON
    {
      "risk": {
        "cause_cancel": true,
        "checkout_id": null,
        "display": true,
        "id": 284138680,
        "message": "This order was placed from a proxy IP",
        "order_id": 450789469,
        "recommendation": "cancel",
        "score": "1.0",
        "source": "External",
        "merchant_message": "This order was placed from a proxy IP"
      }
    }
# Order
## Methods

Load Correctly from Order XML

    order_xml = """<?xml version="1.0" encoding="UTF-8"?>
              <order>
                <note-attributes type="array">
                  <note-attribute>
                    <name>size</name>
                    <value>large</value>
                  </note-attribute>
                </note-attributes>
              </order>"""
    order = shopify.Order(xml_to_dict(order_xml)["order"])

Add Note Attributes to Order

    order = shopify.Order()
    order.note_attributes = []
    order.note_attributes.append(shopify.NoteAttribute({'name': "color", 'value': "blue"}))

Get Order

    shopify.Order.find(450789469)


    shopify.Order.find(fulfillment_status="partial", fields="id,fulfillment_status,line_items")

Get Order Transaction

    order = shopify.Order.find(450789469)
    order.transactions()


## JSON
    {
      "order": {
        "buyer_accepts_marketing": false,
        "cancel_reason": null,
        "cancelled_at": null,
        "cart_token": "68778783ad298f1c80c3bafcddeea02f",
        "checkout_token": null,
        "closed_at": null,
        "confirmed": false,
        "created_at": "2008-01-10T11:00:00-05:00",
        "currency": "USD",
        "email": "bob.norman@hostmail.com",
        "financial_status": "authorized",
        "fulfillment_status": null,
        "gateway": "authorize_net",
        "id": 450789469,
        "landing_site": "http://www.example.com?source=abc",
        "location_id": null,
        "name": "#1001",
        "note": null,
        "number": 1,
        "reference": "fhwdgads",
        "referring_site": "http://www.otherexample.com",
        "source": null,
        "subtotal_price": "398.00",
        "taxes_included": false,
        "test": false,
        "token": "b1946ac92492d2347c6235b4d2611184",
        "total_discounts": "0.00",
        "total_line_items_price": "398.00",
        "total_price": "409.94",
        "total_price_usd": "409.94",
        "total_tax": "11.94",
        "total_weight": 0,
        "updated_at": "2008-01-10T11:00:00-05:00",
        "user_id": null,
        "browser_ip": null,
        "landing_site_ref": "abc",
        "order_number": 1001,
        "discount_codes": [
          {
            "code": "TENOFF",
            "amount": "10.00"
          }
        ],
        "note_attributes": [
          {
            "name": "custom engraving",
            "value": "Happy Birthday"
          },
          {
            "name": "colour",
            "value": "green"
          }
        ],
        "processing_method": "direct",
        "checkout_id": 450789469,
        "source_name": "web",
        "tax_lines": [
          {
            "price": "11.94",
            "rate": 0.06,
            "title": "State Tax"
          }
        ],
        "line_items": [
          {
            "fulfillment_service": "manual",
            "fulfillment_status": null,
            "grams": 200,
            "id": 466157049,
            "price": "199.00",
            "product_id": 632910392,
            "quantity": 1,
            "requires_shipping": true,
            "sku": "IPOD2008GREEN",
            "title": "IPod Nano - 8gb",
            "variant_id": 39072856,
            "variant_title": "green",
            "vendor": null,
            "name": "IPod Nano - 8gb - green",
            "variant_inventory_management": "shopify",
            "properties": [
              {
                "name": "Custom Engraving",
                "value": "Happy Birthday"
              }
            ],
            "product_exists": true
          },
          {
            "fulfillment_service": "manual",
            "fulfillment_status": null,
            "grams": 200,
            "id": 518995019,
            "price": "199.00",
            "product_id": 632910392,
            "quantity": 1,
            "requires_shipping": true,
            "sku": "IPOD2008RED",
            "title": "IPod Nano - 8gb",
            "variant_id": 49148385,
            "variant_title": "red",
            "vendor": null,
            "name": "IPod Nano - 8gb - red",
            "variant_inventory_management": "shopify",
            "properties": [
    
            ],
            "product_exists": true
          },
          {
            "fulfillment_service": "manual",
            "fulfillment_status": null,
            "grams": 200,
            "id": 703073504,
            "price": "199.00",
            "product_id": 632910392,
            "quantity": 1,
            "requires_shipping": true,
            "sku": "IPOD2008BLACK",
            "title": "IPod Nano - 8gb",
            "variant_id": 457924702,
            "variant_title": "black",
            "vendor": null,
            "name": "IPod Nano - 8gb - black",
            "variant_inventory_management": "shopify",
            "properties": [
    
            ],
            "product_exists": true
          }
        ],
        "shipping_lines": [
          {
            "code": "Free Shipping",
            "price": "0.00",
            "source": "shopify",
            "title": "Free Shipping"
          }
        ],
        "payment_details": {
          "avs_result_code": null,
          "credit_card_bin": null,
          "cvv_result_code": null,
          "credit_card_number": "XXXX-XXXX-XXXX-4242",
          "credit_card_company": "Visa"
        },
        "billing_address": {
          "address1": "Chestnut Street 92",
          "address2": "",
          "city": "Louisville",
          "company": null,
          "country": "United States",
          "first_name": "Bob",
          "last_name": "Norman",
          "latitude": "45.41634",
          "longitude": "-75.6868",
          "phone": "555-625-1199",
          "province": "Kentucky",
          "zip": "40202",
          "name": "Bob Norman",
          "country_code": "US",
          "province_code": "KY"
        },
        "shipping_address": {
          "address1": "Chestnut Street 92",
          "address2": "",
          "city": "Louisville",
          "company": null,
          "country": "United States",
          "first_name": "Bob",
          "last_name": "Norman",
          "latitude": "45.41634",
          "longitude": "-75.6868",
          "phone": "555-625-1199",
          "province": "Kentucky",
          "zip": "40202",
          "name": "Bob Norman",
          "country_code": "US",
          "province_code": "KY"
        },
        "fulfillments": [
          {
            "created_at": "2014-01-22T15:58:27-05:00",
            "id": 255858046,
            "order_id": 450789469,
            "service": "manual",
            "status": "failure",
            "tracking_company": null,
            "updated_at": "2014-01-22T15:58:27-05:00",
            "tracking_number": "1Z2345",
            "tracking_numbers": [
              "1Z2345"
            ],
            "tracking_url": "http://wwwapps.ups.com/etracking/tracking.cgi?InquiryNumber1=1Z2345&TypeOfInquiryNumber=T&AcceptUPSLicenseAgreement=yes&submit=Track",
            "tracking_urls": [
              "http://wwwapps.ups.com/etracking/tracking.cgi?InquiryNumber1=1Z2345&TypeOfInquiryNumber=T&AcceptUPSLicenseAgreement=yes&submit=Track"
            ],
            "receipt": {
              "testcase": true,
              "authorization": "123456"
            },
            "line_items": [
              {
                "fulfillment_service": "manual",
                "fulfillment_status": null,
                "grams": 200,
                "id": 466157049,
                "price": "199.00",
                "product_id": 632910392,
                "quantity": 1,
                "requires_shipping": true,
                "sku": "IPOD2008GREEN",
                "title": "IPod Nano - 8gb",
                "variant_id": 39072856,
                "variant_title": "green",
                "vendor": null,
                "name": "IPod Nano - 8gb - green",
                "variant_inventory_management": "shopify",
                "properties": [
                  {
                    "name": "Custom Engraving",
                    "value": "Happy Birthday"
                  }
                ],
                "product_exists": true
              }
            ]
          }
        ],
        "client_details": {
          "accept_language": null,
          "browser_ip": "0.0.0.0",
          "session_hash": null,
          "user_agent": null
        },
        "customer": {
          "accepts_marketing": false,
          "created_at": "2014-01-22T15:58:27-05:00",
          "email": "bob.norman@hostmail.com",
          "first_name": "Bob",
          "id": 207119551,
          "last_name": "Norman",
          "last_order_id": null,
          "multipass_identifier": null,
          "note": null,
          "orders_count": 0,
          "state": "disabled",
          "total_spent": "0.00",
          "updated_at": "2014-01-22T15:58:27-05:00",
          "verified_email": true,
          "tags": "",
          "last_order_name": null,
          "default_address": {
            "address1": "Chestnut Street 92",
            "address2": "",
            "city": "Louisville",
            "company": null,
            "country": "United States",
            "first_name": null,
            "id": 207119551,
            "last_name": null,
            "phone": "555-625-1199",
            "province": "Kentucky",
            "zip": "40202",
            "name": null,
            "province_code": "KY",
            "country_code": "US",
            "country_name": "United States",
            "default": true
          }
        }
      }
    }
# Product
## Methods

Add Metafields to Product

    product = shopify.Product.find(632910392)
    product.add_metafield(shopify.Metafield({'namespace': "contact", 'key': "email", 'value': "123@example.com", 'value_type': "string"}))

Get Metafields for Product

    product = shopify.Product.find(632910392)
    product.metafields()

Get Metafields for Product with Params

    product = shopify.Product.find(632910392)
    product.metafields(limit=2)

Get Metafields for Product Count

    product = shopify.Product.find(632910392)
    product.metafields_count()

Get Metafields for Product with Params

    product = shopify.Product.find(632910392)
    product.metafields_count(value_type="string")

Update Loaded Variant

    product = shopify.Product.find(632910392)
    variant = self.product.variants[0]
    variant.price = "0.50"
    variant.save

Add Variant to Product

    product = shopify.Product.find(632910392)
    v = shopify.Variant()
    product.add_variant(v)


## JSON
    {
      "product": {
        "product_type": "Cult Products",
        "handle": "ipod-nano",
        "created_at": "2011-10-20T14:05:13-04:00",
        "body_html": "<p>It's the small iPod with one very big idea: Video. Now the world's most popular music player, available in 4GB and 8GB models, lets you enjoy TV shows, movies, video podcasts, and more. The larger, brighter display means amazing picture quality. In six eye-catching colors, iPod nano is stunning all around. And with models starting at just $149, little speaks volumes.</p>",
        "title": "IPod Nano - 8GB",
        "template_suffix": null,
        "updated_at": "2011-10-20T14:05:13-04:00",
        "id": 632910392,
        "tags": "Emotive, Flash Memory, MP3, Music",
        "images": [
          {
            "position": 1,
            "created_at": "2011-10-20T14:05:13-04:00",
            "product_id": 632910392,
            "updated_at": "2011-10-20T14:05:13-04:00",
            "src": "http://static.shopify.com/s/files/1/6909/3384/products/ipod-nano.png?0",
            "id": 850703190
          }
        ],
        "variants": [
          {
            "position": 1,
            "price": "199.00",
            "product_id": 632910392,
            "created_at": "2011-10-20T14:05:13-04:00",
            "requires_shipping": true,
            "title": "Pink",
            "inventory_quantity": 10,
            "compare_at_price": null,
            "inventory_policy": "continue",
            "updated_at": "2011-10-20T14:05:13-04:00",
            "inventory_management": "shopify",
            "id": 808950810,
            "taxable": true,
            "grams": 200,
            "sku": "IPOD2008PINK",
            "option1": "Pink",
            "fulfillment_service": "manual",
            "option2": null,
            "option3": null
          },
          {
            "position": 2,
            "price": "199.00",
            "product_id": 632910392,
            "created_at": "2011-10-20T14:05:13-04:00",
            "requires_shipping": true,
            "title": "Red",
            "inventory_quantity": 20,
            "compare_at_price": null,
            "inventory_policy": "continue",
            "updated_at": "2011-10-20T14:05:13-04:00",
            "inventory_management": "shopify",
            "id": 49148385,
            "taxable": true,
            "grams": 200,
            "sku": "IPOD2008RED",
            "option1": "Red",
            "fulfillment_service": "manual",
            "option2": null,
            "option3": null
          },
          {
            "position": 3,
            "price": "199.00",
            "product_id": 632910392,
            "created_at": "2011-10-20T14:05:13-04:00",
            "requires_shipping": true,
            "title": "Green",
            "inventory_quantity": 30,
            "compare_at_price": null,
            "inventory_policy": "continue",
            "updated_at": "2011-10-20T14:05:13-04:00",
            "inventory_management": "shopify",
            "id": 39072856,
            "taxable": true,
            "grams": 200,
            "sku": "IPOD2008GREEN",
            "option1": "Green",
            "fulfillment_service": "manual",
            "option2": null,
            "option3": null
          },
          {
            "position": 4,
            "price": "199.00",
            "product_id": 632910392,
            "created_at": "2011-10-20T14:05:13-04:00",
            "requires_shipping": true,
            "title": "Black",
            "inventory_quantity": 40,
            "compare_at_price": null,
            "inventory_policy": "continue",
            "updated_at": "2011-10-20T14:05:13-04:00",
            "inventory_management": "shopify",
            "id": 457924702,
            "taxable": true,
            "grams": 200,
            "sku": "IPOD2008BLACK",
            "option1": "Black",
            "fulfillment_service": "manual",
            "option2": null,
            "option3": null
          }
        ],
        "vendor": "Apple",
        "published_at": "2007-12-31T19:00:00-05:00",
        "options": [
          {
            "name": "Title"
          }
        ]
      }
    }
# Recurring Charge
## Methods

Activate Charge

    charge = shopify.RecurringApplicationCharge({'id': 35463})
    charge.activate()

Get Current Active Charge

    shopify.RecurringApplicationCharge.current()

Get Associated Usage Charges

    charge = shopify.RecurringApplicationCharge.current()
    charge.usage_charges()

Customize Capped Amount

    charge = shopify.RecurringApplicationCharge.current()
    charge.customize(capped_amount= 200)


## JSON
    {
      "recurring_application_charges": [
        {
          "activated_on": null,
          "api_client_id": 755357713,
          "billing_on": "2015-01-15T00:00:00+00:00",
          "cancelled_on": null,
          "created_at": "2015-01-16T11:45:44-05:00",
          "id": 455696195,
          "name": "Super Mega Plan",
          "price": "15.00",
          "return_url": "http://yourapp.com",
          "status": "accepted",
          "test": null,
          "trial_days": 0,
          "trial_ends_on": null,
          "updated_at": "2015-01-16T11:46:56-05:00",
          "decorated_return_url": "http://yourapp.com?charge_id=455696195"
        },
        {
          "activated_on": "2015-01-15T00:00:00+00:00",
          "api_client_id": 755357713,
          "billing_on": "2015-01-15T00:00:00+00:00",
          "cancelled_on": null,
          "created_at": "2015-01-16T11:45:44-05:00",
          "id": 455696195,
          "name": "Super Mega Plan 2",
          "price": "15.00",
          "return_url": "http://yourapp.com",
          "status": "active",
          "test": null,
          "trial_days": 0,
          "trial_ends_on": null,
          "updated_at": "2015-01-16T11:46:56-05:00",
          "decorated_return_url": "http://yourapp.com?charge_id=455696195",
          "capped_amount": 100,
          "terms": "$1 for 1000 emails"
        }
      ]
    }
# Refund
## Methods

Find Specific Refund

    shopify.Refund.find(509562969, order_id=450789469)


## JSON
    {
      "refund": {
          "id": 509562969,
          "order_id": 450789469,
          "created_at": "2016-06-20T13:35:06-04:00",
          "note": "it broke during shipping",
          "restock": true,
          "user_id": 799407056,
          "refund_line_items": [
            {
              "id": 104689539,
              "quantity": 1,
              "line_item_id": 703073504,
              "line_item": {
                "id": 703073504,
                "variant_id": 457924702,
                "title": "IPod Nano - 8gb",
                "quantity": 1,
                "price": "199.00",
                "grams": 200,
                "sku": "IPOD2008BLACK",
                "variant_title": "black",
                "vendor": null,
                "fulfillment_service": "manual",
                "product_id": 632910392,
                "requires_shipping": true,
                "taxable": true,
                "gift_card": false,
                "name": "IPod Nano - 8gb - black",
                "variant_inventory_management": "shopify",
                "properties": [
                ],
                "product_exists": true,
                "fulfillable_quantity": 1,
                "total_discount": "0.00",
                "fulfillment_status": null,
                "tax_lines": [
                  {
                    "title": "State Tax",
                    "price": "3.98",
                    "rate": 0.06
                  }
                ]
              }
            },
            {
              "id": 709875399,
              "quantity": 1,
              "line_item_id": 466157049,
              "line_item": {
                "id": 466157049,
                "variant_id": 39072856,
                "title": "IPod Nano - 8gb",
                "quantity": 1,
                "price": "199.00",
                "grams": 200,
                "sku": "IPOD2008GREEN",
                "variant_title": "green",
                "vendor": null,
                "fulfillment_service": "manual",
                "product_id": 632910392,
                "requires_shipping": true,
                "taxable": true,
                "gift_card": false,
                "name": "IPod Nano - 8gb - green",
                "variant_inventory_management": "shopify",
                "properties": [
                  {
                    "name": "Custom Engraving Front",
                    "value": "Happy Birthday"
                  },
                  {
                    "name": "Custom Engraving Back",
                    "value": "Merry Christmas"
                  }
                ],
                "product_exists": true,
                "fulfillable_quantity": 1,
                "total_discount": "0.00",
                "fulfillment_status": null,
                "tax_lines": [
                  {
                    "title": "State Tax",
                    "price": "3.98",
                    "rate": 0.06
                  }
                ]
              }
            }
          ],
          "transactions": [
            {
              "id": 179259969,
              "order_id": 450789469,
              "amount": "209.00",
              "kind": "refund",
              "gateway": "bogus",
              "status": "success",
              "message": null,
              "created_at": "2005-08-05T12:59:12-04:00",
              "test": false,
              "authorization": "authorization-key",
              "currency": "USD",
              "location_id": null,
              "user_id": null,
              "parent_id": null,
              "device_id": null,
              "receipt": {},
              "error_code": null,
              "source_name": "web"
            }
          ],
          "order_adjustments": [
          ]
        }
    }
# Session
## Methods

Create Session

    shopify.Session("testshop.myshopify.com", "any-token")

Setup Session

    shopify.Session.setup(api_key="My test key", secret="My test secret")

Create Temp Session

    shopify.Session.temp("testshop.myshopify.com", "any-token")

Calculate HMAC

    shopify.Session.calculate_hmac(params)

Validate HMAC

    hopify.Session.validate_hmac(params)

Request Token

    session = shopify.Session("testshop.myshopify.com")
    token = session.request_token({'code':'any_code', 'foo': 'bar', 'timestamp':'1234'})

Create Permission URL

    shopify.Session.setup(api_key="My_test_key", secret="My test secret")
    session = shopify.Session('http://localhost.myshopify.com')
    scope = ["write_products"]
    session.create_permission_url(scope)
# Shipping Zone
## Methods

Get Shipping Zones

    shopify.ShippingZone.find()


## JSON
    {
      "shipping_zones": [
        {
          "id": 1,
          "name": "Some zone",
          "countries": [
            {
              "id": 817138619,
              "name": "United States",
              "tax": 0.0,
              "code": "US",
              "tax_name": "Federal Tax",
              "provinces": [
                {
                  "id": 1013111685,
                  "country_id": 817138619,
                  "name": "New York",
                  "code": "NY",
                  "tax": 0.04,
                  "tax_name": "Tax",
                  "tax_type": null,
                  "shipping_zone_id": 1,
                  "tax_percentage": 4.0
                },
                {
                  "id": 1069646654,
                  "country_id": 817138619,
                  "name": "Ohio",
                  "code": "OH",
                  "tax": 0.0,
                  "tax_name": "State Tax",
                  "tax_type": null,
                  "shipping_zone_id": 1,
                  "tax_percentage": 0.0
                }
              ]
            },
            {
              "id": 879921427,
              "name": "Canada",
              "tax": 0.05,
              "code": "CA",
              "tax_name": "GST",
              "provinces": [
                {
                  "id": 702530425,
                  "country_id": 879921427,
                  "name": "Ontario",
                  "code": "ON",
                  "tax": 0.08,
                  "tax_name": "Tax",
                  "tax_type": null,
                  "shipping_zone_id": 1,
                  "tax_percentage": 8.0
                },
                {
                  "id": 224293623,
                  "country_id": 879921427,
                  "name": "Quebec",
                  "code": "QC",
                  "tax": 0.09,
                  "tax_name": "HST",
                  "tax_type": "compounded",
                  "shipping_zone_id": 1,
                  "tax_percentage": 9.0
                }
              ]
            },
            {
              "id": 988409122,
              "name": "Yemen",
              "tax": 0.0,
              "code": "YE",
              "tax_name": "GST",
              "provinces": [
              ]
            }
          ],
          "weight_based_shipping_rates": [
            {
              "id": 760465697,
              "weight_low": 1.2,
              "weight_high": 10.0,
              "name": "Austria Express Heavy Shipping",
              "price": "40.00",
              "shipping_zone_id": 1
            }
          ],
          "price_based_shipping_rates": [
            {
              "id": 583276424,
              "name": "Standard Shipping",
              "min_order_subtotal": "0.00",
              "price": "10.99",
              "max_order_subtotal": "2000.00",
              "shipping_zone_id": 1
            }
          ],
          "carrier_shipping_rate_providers": [
            {
              "id": 972083812,
              "country_id": null,
              "carrier_service_id": 61629186,
              "flat_modifier": "0.00",
              "percent_modifier": 0,
              "service_filter": {
                "*": "+"
              },
              "shipping_zone_id": 1
            }
          ]
        }
      ]
    }
# Shop
## Methods

Get Current Shop

    shopify.Shop.current()

Get Metafields

    shop = shopify.Shop.current()
    shop.metafields()

Add Metafield

    shop = shopify.Shop.current()
    shop.add_metafield( shopify.Metafield({'namespace': "contact", 'key': "email", 'value': "123@example.com", 'value_type': "string"}))

Get Events

    shop = shopify.Shop.current()
    shop.events()


## JSON
    {
      "shop": {
        "name": "Apple Computers",
        "city": "Cupertino",
        "address1": "1 Infinite Loop",
        "zip": "95014",
        "created_at": "2007-12-31T19:00:00-05:00",
        "shop_owner": "Steve Jobs",
        "plan_name": "enterprise",
        "public": false,
        "country": "US",
        "money_with_currency_format": "$ {{amount}} USD",
        "money_format": "$ {{amount}}",
        "domain": "shop.apple.com",
        "taxes_included": null,
        "id": 690933842,
        "timezone": "(GMT-05:00) Eastern Time (US & Canada)",
        "tax_shipping": null,
        "phone": null,
        "currency": "USD",
        "myshopify_domain": "apple.myshopify.com",
        "source": null,
        "province": "CA",
        "email": "steve@apple.com"
      }
    }


# ShopifyResource
## Methods

Activate Session

    session1 = shopify.Session('shop1.myshopify.com', 'token1')
    ShopifyResource.activate_session(session1)

Set Headers

    shopify.ShopifyResource.set_headers({'X-Custom': 'abc'})

Clear Session

    shopify.ShopifyResource.clear_session()
# Transaction
## Methods

Get Transaction

    shopify.Transaction.find(389404469, order_id=450789469)


## JSON
    {
      "transaction": {
        "amount": "409.94",
        "authorization": "authorization-key",
        "created_at": "2005-08-01T11:57:11-04:00",
        "gateway": "bogus",
        "id": 389404469,
        "kind": "authorization",
        "location_id": null,
        "message": null,
        "order_id": 450789469,
        "parent_id": null,
        "status": "success",
        "test": false,
        "user_id": null,
        "device_id": null,
        "receipt": {
          "testcase": true,
          "authorization": "123456"
        },
        "payment_details": {
          "avs_result_code": null,
          "credit_card_bin": null,
          "cvv_result_code": null,
          "credit_card_number": "XXXX-XXXX-XXXX-4242",
          "credit_card_company": "Visa"
        }
      }
    }
# Usage Charge
## Methods

Create Usage Charge

    charge = shopify.UsageCharge({'price': 9.0, 'description': '1000 emails', 'recurring_application_charge_id': 654381177})
    charge.save()

Get Usage Charge

    shopify.UsageCharge.find(359376002, recurring_application_charge_id= 654381177)


## JSON
    {
      "usage_charge": {
        "id": 359376002,
        "description": "1000 emails",
        "price": "9.00",
        "recurring_application_charge_id": 654381177,
        "billing_on": "2015-07-08",
        "balance_remaining": "91.00",
        "balance_used": "9.00"
      }
    }
# Variant
## Methods

Get Variants

    shopify.Variant.find(product_id = 632910392)

Get Variant Namespaced

    shopify.Variant.find(product_id = 632910392)

Update Variant Namespaced

    v = shopify.Variant.find(808950810, product_id = 632910392)
    v.save()

Create Variant

    v = shopify.Variant({'product_id':632910392})
    v.save()

Create Variant then Add Parent ID

    v = shopify.Variant()
    v.product_id = 632910392
    v.save()

Get Variant

    shopify.Variant.find(808950810)


## JSON
    {
      "variant": {
        "price": "199.00",
        "position": 1,
        "created_at": "2011-10-20T14:05:13-04:00",
        "title": "Pink",
        "requires_shipping": true,
        "updated_at": "2011-10-20T14:05:13-04:00",
        "inventory_policy": "continue",
        "compare_at_price": null,
        "inventory_quantity": 10,
        "inventory_management": "shopify",
        "taxable": true,
        "id": 808950810,
        "grams": 200,
        "sku": "IPOD2008PINK",
        "option1": "Pink",
        "option2": null,
        "fulfillment_service": "manual",
        "option3": null
      }
    }

