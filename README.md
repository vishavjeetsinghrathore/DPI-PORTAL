# Samsung Checkout DPI Architecture – Nike Physical-Product POC

## 1. DPI Portal and Samsung Checkout

**DPI Portal** → Designed around products sold through Samsung TV apps.

The DPI portal is used by eligible Samsung TV partners to register products, configure purchase options, manage subscriptions, and view transactions.

**Samsung Checkout** → The payment system that presents the purchase flow and processes a supported purchase.

## 2. Compare Art Store and HBO Max Services

### Samsung Art Store (Samsung Service)

It is a Samsung service. The Samsung team can coordinate internally to register the app, configure Samsung Checkout, and request DPI access.

### HBO Max (Third-Party Provider)

HBO Max is provided by an external company. Its team works with Samsung to register its app, integrate Checkout, and obtain the required DPI access.

## 3. Steps to Get Access and Required Setup

1. **Partnership and App Registration**
   - Register the company/app through the applicable Seller Office process.

2. **Enable Checkout**
   - Set billing to use Samsung Checkout on TV to **Yes** in the documented registration workflow.

3. **Obtain DPI Access**
   - Access the DPI portal for the registered app, subject to the required approval and permissions.

4. **Configure and Test Purchases**
   - Register the product, integrate the Samsung Checkout API, and test the purchase flow.

## 4. Nike Advertisement POC: How Does the Purchase Flow Work?

For our POC, assume a Nike advertisement appears on the first screen of the Samsung TV. How does the purchase flow work when the user wants to buy the product?

Samsung documentation confirms that, with Dynamic Product, the partner manages actual product information and prices in its own CMS, while DPI contains a representative product and the settings needed for the approved Checkout integration.

### CMS / Commerce Backend
- Stores Nike SKU, size, price-related information, and product details.

### DPI Verification
- Samsung Checkout calls our configured Verify URI to validate the purchase details.

### Samsung Checkout
- Displays the purchase confirmation and returns the payment results.

### Order and Fulfillment
- The retailer handles the order and delivery, if physical goods are approved.

## 5. What to Register in the DPI Portal?

Assume the Samsung Checkout team approves the physical-goods use case and our application is authorized to use Dynamic Product.

### DPI Configuration

- Product name
- Product ID
- Product description
- Product type
- Verify URL
- Country and location

## 6. What to Store in Our CMS (Content Management System)?

The following are recommended commerce-backend fields for the proposed retail system, not a claim that DPI requires all of them:

- Stock
- Size
- Shipping
- Return fields

## 7. How All Components Relate to the POC

For the Nike advertisement POC on the Samsung TV, each component has a different role.

### 7.1 Samsung TV Seller Office

**Role:** Register and manage your Samsung TV application.

**Example:** Register the AdAgent TV app and configure the required billing settings to request Samsung Checkout access.

### 7.2 DPI Portal / DPI Server

**Role:** Manage the representative product configuration and support the approved Dynamic Product purchase and verification flow.

**Example:** Register a representative product such as `adagent_retail_01` and configure the verification endpoint.

### 7.3 CMS / Content Management System

**Role:** Store and manage the actual products and their current details.

**Example:** Store Nike Air Max, size US 9, price, and stock availability, and verify the product and price when a purchase is requested.

### 7.4 AdAgent Side

**Role:** Display advertisements and connect each ad to the relevant product information and purchase system.

**Example:** Show a Nike ad on the TV home screen. When the user selects **Shop Now**, open the product detail page.

### 7.5 Samsung Checkout

**Role:** Provide the supported purchase and payment interface.

**Example:** Show the purchase details and let the user complete payment through the approved Checkout flow.

- Validates purchase details and supports the payment flow.
- Handles order creation or delivery.

## 8. How It Works

1. AdAgent requests the selected shoe details from our CMS (Content Management System).
2. Our CMS returns the current price and availability.
3. The app initiates the approved Samsung Checkout flow using the DPI representative product and the actual product identifier.
4. Our verification endpoint checks whether the product and price are valid.

**DPI contains the representative product configuration; our CMS contains the actual product catalogue.**

## 9. Main Question

Can a company use Samsung’s DPI system and Samsung Checkout to sell real-world products that must be delivered to the customer, rather than digital products or subscriptions?

### Query for the Block Diagram

Create a professional block diagram for Samsung HQ explaining the Samsung Checkout DPI architecture, including each DPI component and its role. Show how AdAgent, DPI Portal/Server, Samsung Checkout, and the CMS/Commerce Backend interact in our Nike physical-product POC, including communication paths and data exchange. Clearly explain the CMS role in the Dynamic Product model, including product catalogue, pricing, stock, and product verification through the Verify URI. Use labeled directional arrows, concise component descriptions, and clearly mark physical-product support as requiring Samsung confirmation.

### Gauss-Gemini Query for the Block Diagram

Create a polished, presentation-ready architecture infographic as an actual rendered image, not Mermaid code, PlantUML, ASCII art, or a text-only diagram. Use a professional enterprise design with color-coded components, clear directional arrows, icons, concise labels, and a white background. Explain the roles of AdAgent, DPI Portal/Server, CMS/Commerce Backend, and Samsung Checkout in our Nike physical-product POC. Show how these components communicate and how the CMS supports the Dynamic Product model, including product catalogue, pricing, stock, and Verify URI. Mark physical-product support as requiring Samsung confirmation.

## 10. Standard Product vs. Dynamic Product

The main difference is who manages the product details, such as price and availability.

### 10.1 Standard Product — DPI Manages Product Configuration

**Example:** A streaming subscription costing $10/month.

- The business registers the product and its price in the DPI system.
- The app gets the registered product information through DPI.
- Samsung Checkout handles the purchase.

**Flow:**

**App** → Requests subscription details

**DPI Server** → Provides registered product and price

**Samsung Checkout** → Processes the purchase

### 10.2 Dynamic Product — CMS Manages Actual Product Details

**Example:** Nike shoes with different sizes, colors, prices, and stock levels.

- The Nike commerce backend (CMS) manages the actual product catalogue, current prices, and stock.
- DPI provides the integration and verification mechanism for the Dynamic Product.
- DPI can contact the CMS through its Verify URI to check whether the product and price are valid.
- Samsung Checkout handles the purchase if this product type is supported and approved.

**Flow:**

**AdAgent** → User selects Nike shoes

**DPI Server** → Coordinates the approved Dynamic Product flow

**Nike CMS / Commerce Backend** → Checks product ID, size, current price, and stock

**Samsung Checkout** → Processes the purchase, subject to approval

## 11. Remember This Simple Example

| Standard Product | Dynamic Product |
|---|---|
| Subscription: $10/month | Nike shoes: $100, size 9 |
| Product configuration is registered in DPI | Actual catalogue and price are managed by CMS |
| DPI provides the registered product information | CMS verifies the current product details through the configured integration |

### Why Use CMS for Dynamic Products?

Nike may have thousands of products, changing prices, and stock levels. Maintaining every live product detail in DPI would be inconvenient. The CMS already manages that information, so DPI can use it through the approved integration.

**Important:** This explains the general Dynamic Product model. Whether Samsung Checkout supports selling physical shoes through this flow must be confirmed with Samsung.