# SparkLite — Electric Gas Lighter Store

A responsive single-product ecommerce starter built with HTML/CSS/JS, Express and optional Razorpay Checkout. The product poster you supplied is included as `public/product-poster.jpg`.

## Included
- Responsive product landing page and feature sections
- Quantity selector and order summary
- Delivery details checkout form with validation
- Cash on Delivery (COD) order creation
- Razorpay order creation and server-side payment-signature verification
- Simple local JSON order store (`data/orders.json`)
- Policy placeholder page

## Run locally
1. Install Node.js 18 or newer.
2. Extract this folder.
3. In a terminal inside this folder run:
   ```bash
   npm install
   cp .env.example .env
   npm start
   ```
4. Open `http://localhost:3000`.

COD works without payment keys. Online payment is intentionally disabled until valid Razorpay credentials are entered.

## Configure Razorpay test payments
1. Create/verify your merchant account in the Razorpay Dashboard.
2. Create **Test Mode** API keys and put the Key ID and Key Secret in `.env`.
3. Keep `ENABLE_ONLINE_PAYMENT=true`.
4. Restart the server and test a complete payment with Razorpay's currently documented test payment methods.
5. Before going live, complete merchant verification and replace test credentials with live credentials in your hosting environment. Never put the Key Secret in frontend code or commit `.env`.

The server verifies the payment signature before marking the order paid. A payment callback or a browser success screen alone is not proof of payment.

## Important before production
This is a runnable starter, not a fully audited production commerce platform. Before taking real customer orders:
- Confirm your actual selling price, tax/GST treatment, shipping charges, stock, delivery coverage and return/refund policy.
- Replace placeholder store name, email, phone and contact details.
- Set up a persistent database (PostgreSQL/MySQL or a managed store), migrations, backups and restricted admin access. The local JSON order file is for demonstration only and is not suitable for concurrent production traffic.
- Add server-side rate limiting, CSRF/origin protections where appropriate, structured logs, monitoring, secure HTTPS hosting and error handling.
- Add a private admin/order-management dashboard, order emails/SMS, shipment tracking and refund workflows if needed.
- Configure real shipping rates and delivery rules. The current site does not calculate shipping or taxes; the total is product price × quantity.
- Review legal requirements for your jurisdiction and publish real privacy, shipping, cancellation, returns and refund policies.
- Confirm that all product safety claims, certifications and product specifications match the actual product and manufacturer documentation.

## Edit the selling price
The starter uses ₹299 per unit and shows ₹499 as a crossed-out reference price. Change `PRODUCT.pricePaise` in `server.js` and `PRICE` in `public/app.js` together. Only show a crossed-out price/discount if it is accurate and lawful. The image says “200 pcs per carton”; the website currently sells individual units, quantity up to 50 per order. Configure carton/wholesale pricing separately if that is your business model.

## Deployment
Deploy to a Node-compatible host with HTTPS, environment variables and persistent storage. Point your domain to the app, set `SITE_URL`, and configure the payment provider's production settings. Do not deploy this starter as-is for live commerce without the production hardening listed above.
