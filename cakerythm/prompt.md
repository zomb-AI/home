# The Cake Rhythm — Project README

This document captures the full build flow for **The Cake Rhythm** digital ordering and admin management system.

It covers:

- website design direction
- business information usage
- final website prompt
- WhatsApp enhancements
- Google Sheet integration
- admin panel setup
- final architecture summary

---

# 1. Project Overview

**The Cake Rhythm** is a homemade cakes and brownies business with a premium, warm, handcrafted brand identity.

The solution was built in stages:

1. Define the website design language
2. Gather business information
3. Generate a premium single-page bakery website
4. Add WhatsApp submission
5. Add Google Sheet logging with Order ID generation
6. Build an admin panel to fetch and manage orders from the same Google Sheet

The final setup includes:

- customer-facing landing page with products, cart, and order submission
- Google Sheet as central order database
- Admin Panel for fetching and updating orders

---
# Architecture Diagram
<img width="1536" height="1024" alt="8c23842a-a2bc-4cd5-93e6-0a5065951860" src="https://github.com/user-attachments/assets/dec61cc2-1374-47fb-b287-56b15802a401" />


# 2. Prompt History and Results

## [PROMPT - 1]
### Provide Design Element for a Home made Cake and Brownies website

## Result
### Visual Design Direction
A premium homemade bakery style with warmth, softness, elegance, and conversion-focused UI.

### Color Palette
- **Primary:** Warm Cream `#FFF4E6`
- **Secondary:** Cocoa Brown `#4E342E`
- **Accent:** Strawberry Pink `#F48FB1`
- **Highlight:** Butter Yellow `#FFD54F`
- **Neutral:** Soft Grey `#F5F5F5`

### Homepage Layout
- Full-width cake / brownie image
- Tagline: **“Baked with Love, Delivered Fresh 💕”**
- CTA Buttons:
  - Order Now
  - Customize Your Cake

### UI Components
#### Buttons
- Rounded edges
- Slight soft shadow

#### Cards
- Soft borders
- Hover zoom on cakes

#### Fonts
- **Headings:** Playfair Display
- **Body:** Poppins / Open Sans

---

## [PROMPT - 2]
### Fetch the information about The Cake Rhythm from the google search page.

## Result
All important business information was fetched and kept ready for later prompt usage.

This business information was used as contextual input for branding, website structure, and admin system planning.

> Keep this business information handy, because it is useful across all later prompts.

---

## [PROMPT - 3]
### Create a Claude Prompt for designing a Single page HTML mobile responsive website using the best UIX design guidelines with HERO sections, Cart, Submit (All Demo), for the business **"The Cake Rhythm" Homemade Cakes and Brownies**

## Result
A full working website prompt was prepared.

### Website Build Goal
Create a complete, production-style single-file website in HTML, CSS, and JavaScript for:

**The Cake Rhythm – Homemade Cakes and Brownies**

### Business Context Used
- **Brand Name:** The Cake Rhythm
- **Category:** Homemade Cakes and Brownies
- **Location:** DLF GARDEN CITY, Thazhambur, Chennai, Tamil Nadu 600130
- **Contact:** +91 9884620064
- **Instagram handle reference:** @ZombAI.io
- **Brand vibe:** warm, elegant, handcrafted, premium homemade bakery, feminine but classy, modern and mobile-first
- **Positioning line:** “Happiness is Homemade”

### Technical Requirements
- single self-contained HTML file
- all CSS and JavaScript inside the same file
- no frameworks
- semantic HTML5
- mobile responsive first
- smooth scrolling
- premium soft animations
- fast loading
- local demo arrays
- polished demo interactions

### Design Direction
- soft cream, cocoa brown, blush pink, rose, warm beige palette
- luxurious but cozy bakery identity
- rounded cards
- soft shadows
- generous whitespace
- premium typography pairing
- elegant handcrafted bakery feel

### Website Color Palette
- Cream: `#FFF7F1`
- Cocoa Brown: `#4A2C24`
- Deep Chocolate: `#2E1A14`
- Blush Pink: `#EFA8B8`
- Rose Pink: `#D97B93`
- Warm Beige: `#EAD8C9`
- Gold Accent: `#C89B5B`
- White: `#FFFFFF`

### Final Website Structure
1. Sticky Header / Navbar
2. Hero Section
3. About / Brand Story Strip
4. Bestsellers / Featured Products
5. Custom Cake Section
6. Brownies Section
7. Why Choose Us
8. Gallery / Sweet Moments
9. Testimonials / Customer Love
10. Cart Drawer / Cart Panel
11. Demo Checkout / Order Submit Section
12. Contact / Footer Section

### Final Result
A **full working website** was created based on this branding.

---

## [PROMPT - 4]
### Enhancements
- On order submission, send to WhatsApp at `YOUR-WHATSAPP-NUMBER`
- On custom cake request form submission, also send to WhatsApp as order summary

## Result
The site was enhanced so that:

- product order submission switches to WhatsApp
- custom cake request also switches to WhatsApp
- order data is formatted into a WhatsApp-friendly message

This created a usable ordering flow without backend complexity.

---

## [PROMPT - 5]
### Send this order to WhatsApp + append it to Google Sheet as well. Create a random OrderID using combination of Customer Name + Mobile + Date of length 6 character, and send it as OrderID in format `CR-OrderID` along with order details to both WhatsApp & Google Sheet.

**[ADD YOUR_GOOGLE_SHEET_LINK]**

## Result
The full **WhatsApp + Google Sheet Integration** was prepared.

### Files Included
1. `the_cake_rhythm_orders_whatsapp_sheet.html`
2. `google_apps_script_orders.gs`

### What this setup does
- generates a 6-character order token using Customer Name + Mobile + Date
- formats it as `CR-XXXXXX`
- sends order details to WhatsApp
- sends same order payload to Google Sheets using Google Apps Script

### Important Note
Direct posting from a static HTML page to a raw Google Sheet edit URL is not reliable.

So the correct approach used was:

- static website -> Google Apps Script Web App -> Google Sheet

### Setup Flow
1. Open your Google Sheet  
   `YOUR_GOOGLE_SHEET_LINK_WILL_APPEAR_HERE`

2. Go to **Extensions -> Apps Script**

3. Paste the content of:
   - `google_apps_script_orders.gs`

4. Deploy it as:
   - Type: **Web app**
   - Execute as: **Me**
   - Who has access: **Anyone**

5. Copy the Web App URL

6. Open the HTML file and replace:
   `PASTE_YOUR_GOOGLE_APPS_SCRIPT_WEBAPP_URL_HERE`

### After Setup
- product orders go to WhatsApp and Sheet
- custom cake requests go to WhatsApp and Sheet
- every order gets an ID like `CR-BA0406`

### Google Sheet Columns Created
- Timestamp
- Order Type
- Order ID
- Customer Name
- Customer Phone
- Address
- Occasion
- Flavor
- Weight
- Cake Type
- Cake Message
- Delivery Date
- Notes
- Items Summary
- Total
- Created At

---

## [PROMPT - 6]
### Design an admin panel for order management as a single page mobile responsive interface in the same theme so that all orders received in Google Sheet can be fetched and managed.

### Requirements
Admin should manage:

#### Order Status
- New
- Confirmed
- Preparing
- Out for Delivery
- Delivered
- Cancelled

#### Payment Status
- Paid
- Pending

#### Payment Mode
- COD
- Online
- Advance

### Dashboard Summary
- Total Orders (Today)
- Total Revenue
- Pending Orders
- Delivered Orders

### Flow
- Landing page -> **FETCH ORDERS BUTTON**
- Display order list with filters:
  - Order Status
  - All Orders
  - Today’s Orders
- Order Detail in accordion view
- Update order in popup
- On update click, write changes back into the same Google Sheet row

## Result
The admin system was created.

### Files Produced
- Admin panel HTML
- Apps Script backend for fetch + update

### Columns Used in Admin Panel
- Order ID
- Customer Name
- Customer Phone
- Address
- Occasion
- Flavor
- Weight
- Cake Type
- Cake Message
- Delivery Date
- Notes
- Items Summary
- Total
- Order Status
- Payment Status
- Payment Mode
- Assigned To
- Priority
- Admin Notes

### How it Works
- landing view includes **Fetch Orders**
- dashboard shows:
  - today’s orders
  - revenue
  - pending orders
  - delivered orders
- filters supported:
  - order status
  - all orders
  - today’s orders
  - search
- each order opens in accordion view
- update order opens popup
- saving writes back to the same row in Google Sheet
- no new row is appended during admin update

### Backend Logic
The Apps Script uses:

- spreadsheet ID
- exact sheet gid / target sheet
- row matching by `Order ID` or row number
- `doGet` for fetch
- `doPost` for update

### One Required Setup Step
1. Deploy the `.gs` file as a **Google Apps Script Web App**
2. Copy the Web App URL
3. Replace `PASTE_YOUR_GOOGLE_APPS_SCRIPT_WEBAPP_URL_HERE` inside the Admin HTML file

After this, the Admin Panel can fetch and update live sheet data.

---

# 3. Final System Summary

At the end of this flow, the static website system consists of:

## Customer-Facing Assets
- landing page with products
- cart drawer
- order submission form
- custom cake request form
- WhatsApp redirection
- Google Sheet order logging
- generated Order ID

## Admin Assets
- Google Sheet order database
- admin sheet columns
- Admin Panel
- fetch order flow
- update order flow

---

# 4. Final Architecture

## Order Flow
1. User visits website
2. User adds products to cart
3. User submits order
4. Order is marked placed
5. Website generates Order ID
6. Order is sent to WhatsApp
7. Order is saved to Google Sheet using Apps Script

## Admin Flow
1. Admin opens Admin Panel
2. Admin clicks **Fetch Orders**
3. Orders are loaded from same Google Sheet
4. Admin filters orders
5. Admin opens accordion details
6. Admin updates status / payment details
7. Changes are written back into same row in Google Sheet

---

# 5. Final Deliverables Summary

## Static Website
- Landing page with products / orders / cart

## Google Sheet
- central order database

## Admin Panel
- fetch and manage orders from same Google Sheet

---

# 6. Recommended Folder Structure

```text
TheCakeRhythm/
│
├── customer/
│   ├── the_cake_rhythm_orders_whatsapp_sheet.html
│   └── google_apps_script_orders.gs
│
├── admin/
│   ├── cake_rhythm_admin_panel.html
│   └── cake_rhythm_admin_panel_apps_script.gs
│
├── sheet/
│   └── The Cake Rhythm Orders Google Sheet
│
└── docs/
    └── README.md
```

---

# 7. Setup Checklist

## Customer Side
- [ ] Branding applied
- [ ] Website HTML created
- [ ] WhatsApp number configured
- [ ] Google Apps Script deployed
- [ ] Web App URL pasted into site
- [ ] Test order added to sheet
- [ ] WhatsApp opens correctly

## Admin Side
- [ ] Admin Panel HTML created
- [ ] Admin Apps Script deployed
- [ ] Web App URL pasted into admin panel
- [ ] Fetch Orders works
- [ ] Update popup works
- [ ] Order row updates correctly
- [ ] No duplicate append happens during update

---

# 8. Conclusion

The system now has **two different pages**:

1. **Landing Page**
   - products
   - cart
   - order submission
   - custom cake request
   - WhatsApp + Google Sheet integration

2. **Admin Panel**
   - fetch orders from Google Sheet
   - view orders
   - filter orders
   - update order status
   - update payment details
   - write updates back to same Google Sheet row

And the central source of truth is:

- **Google Sheet**

That makes the solution lightweight, manageable, low-cost, and easy to operate for a boutique homemade bakery business.

---
