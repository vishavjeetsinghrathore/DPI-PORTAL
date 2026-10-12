

dpi portal designed around product sold through samsung tv apps


dpi portal -> used by eligible samsung tv partners to register products, configure purchase option, manage subscription, view transaction,

samsung checkout -> the payment that presents the purchase flow and processes a supported purchase

compare art-app and hbo-max service -> 

samsung art store (samsung service ) ->

it is a samsung service, samsung team can coordinate internally to register, the app, configure samsung checkout , request dpi access

hbo max -> third party prodiver

hbo max is provided by an external company, its team works with samsung to register its app, integrate checkout , and obtain required dpi
access

steps for get access thr required things ->

1. partnership and app registration -> ( register the company/app through the applicable seller office process)
2. enable checkout -> set billing to use and samsung checkout on tv to yes in the documented registration workflow
3. obtain the dpi access -> access the dpi portal for the registration app , subject to the required approval and permission
4. consfigure and test purchases -> register product, integrate the samsung checkout api, and test the purchase flow


for our poc like nike ad on the first screen how it flow happening for buy the product by the user -> 

samsung documentation confirm that , with dynamic product, the partner manages actual product information and prices in its own cms, 
while dpi contains a representative product and the settings needed for the approved checkout integration

cms/commerce backend -> store nike, sku, size, or price related information and the product details

dpi verification -> samsung checkout calls our configured verify uri to validate the purchase details

samsung checkout -> displays the purchase confirmation and return the payment results

order and fullfillment -> retailer handles the order and delivery, if physical-goods are approved


what to register in the dpi portal -> 

assume the samsung checkout team approves the physical-goods use case and our application is authorized to use the dynamic product

dpi configuration ->

product name, product id,product description, product type, verify the url, country and location


what to store in our cms (content management system) ->

the stock, size, shipping and return fields, above are recommended commerce-backend fields for your proposed retail system, not a claim
that dpi requires all of them


how it related all the things in the poc -> for the nike advertisement poc on the samsung tv , each component has different role ->

1. samsung tv seller office -> 

role -> register and manage your samsung tv application
example -> register the adagent tv app and configure the required billing settings to request samsung checkout access

2. dpi portal/dpi server ->

role -> manage the representative product configuration and support the approved dynamic product purchase and verification flow
example -> register a repesentative product such as adagent_retail_01 and configure the verification endpoint

3. cms/content management system

role -> store and manage the actual products and their current details
example -> store nike air max size us 9, price, and stock availability, verify the product and price when a purchase is requested

4. adagent side -> 

role -> display advertisement and connect each ad to the relevant product information purchase system
example -> show a nike ad on the tv home screen, when the user selects shop now, open the product detail page 

5. samsung checkout ->

role -> provide the supported purchase and payment interface
example -> show the purchase details and let the user complete payment through the approved checkout flow.

validate purchase details and supoprt the payment flow supported

handles order creation or delivery , 


how it works ->

adagent request the selected shoe details from your cms (content management system)
our cms returns the current price and availability
the app initates the approved samsung checkout flow using the dpi representative product the the actual product identifier
your verification endpoint checks that the product and price are valid or not
-> dpi contains the representaive product configuration: our cms contains the actual product catalogue


question -> 

dynamic product integration supports physical-goodds

use samsung checkout to sell physical-goods 

query for the block diagram -<

Create a professional block diagram for Samsung HQ explaining the Samsung Checkout DPI architecture, including each DPI component and its role. Show how AdAgent, DPI Portal/Server, Samsung Checkout, and the CMS/Commerce Backend interact in our Nike physical-product POC, including communication paths and data exchange. Clearly explain the CMS role in the Dynamic Product model, including product catalogue, pricing, stock, and product verification through the Verify URI. Use labeled directional arrows, concise component descriptions, and clearly mark physical-product support as requiring Samsung confirmation.


gauss-gemini query for the block diagram ->

Create a polished, presentation-ready architecture infographic as an actual rendered image, not Mermaid code, PlantUML, ASCII art, or a text-only diagram. Use a professional enterprise design with color-coded components, clear directional arrows, icons, concise labels, and a white background. Explain the roles of AdAgent, DPI Portal/Server, CMS/Commerce Backend, and Samsung Checkout in our Nike physical-product POC. Show how these components communicate and how the CMS supports the Dynamic Product model, including product catalogue, pricing, stock, and Verify URI. Mark physical-product support as requiring Samsung confirmation.


The main difference is who manages the product details, such as price and availability.
1. Standard Product — DPI manages product configuration
Example: A streaming subscription costing $10/month.
- The business registers the product and its price in the DPI system.
- The app gets the registered product information through DPI.
- Samsung Checkout handles the purchase.
App
Requests subscription details

DPI Server
Provides registered product and price

Samsung Checkout
Processes the purchase


2. Dynamic Product — CMS manages actual product details
Example: Nike shoes with different sizes, colors, prices, and stock levels.
- The Nike commerce backend (CMS) manages the actual product catalogue, current prices, and stock.
- DPI provides the integration and verification mechanism for the dynamic product.
- DPI can contact the CMS through its Verify URI to check whether the product and price are valid.
- Samsung Checkout handles the purchase if this product type is supported and approved.
AdAgent
User selects Nike shoes

DPI Server
Coordinates the approved dynamic-product flow

Nike CMS / Commerce Backend
Checks product ID, size, current price, and stock

Samsung Checkout
Processes the purchase, subject to approval


Remember this simple example
Standard product	Dynamic product
Subscription: $10/month	Nike shoes: $100, size 9
Product configuration is registered in DPI	Actual catalogue and price are managed by CMS
DPI provides the registered product information	CMS verifies the current product details through the configured integration
Why use CMS for Dynamic Products? Nike may have thousands of products, changing prices, and stock levels. Maintaining every live product detail in DPI would be inconvenient. The CMS already manages that information, so DPI can use it through the approved integration.
Important: This explains the general Dynamic Product model. Whether Samsung Checkout supports selling physical shoes through this flow must be confirmed with Samsung.


