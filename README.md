Driver Booking — Billing System

A single-file, mobile-first billing & invoice system for driver bookings.
Generates professional invoices with UPI QR (contains amount), lets you save bookings locally (localStorage), download a print-ready single-page PDF, share via WhatsApp, and manage bookings in an admin panel — all offline, no backend required.

Features

Mobile-first, responsive UI (Bootstrap 5)

Select plans, overtime calculation, extras, editable total

Order ID generator (ORD-YYYYMMDD-XXXX)

UPI QR generator with amount (UPI ID: bhanupratapbiswas@ptyes)

Preview invoice (company details, billing address, QR, signature placeholder)

Download single-page A4 PDF that matches the on-screen preview (QR included)

Share invoice via WhatsApp (prefilled message)

Local admin panel (localStorage) with:

Search, pagination, page-size selector

Actions: Mark Paid (confirmation modal with optional Transaction ID), Export, Delete

Clear all bookings, export all to CSV

CSV includes paymentTxId and paymentTimestamp when payment is marked

All data stored locally (no servers), offline-capable

Simple configuration points for UPI ID, logo, admin password, storage key

Files

driver_billing_final.html — single-file app (HTML, CSS, JavaScript).
(Everything lives in this one file — copy to your device and open in a browser.)

Quick Start

Save the provided HTML into a file named, e.g., driver_billing_final.html.

Open the file in a modern browser (Chrome, Edge, Firefox) on desktop or mobile.

Use the form to:

Generate Order ID → select a plan → set overtime/extras → click Preview & Generate QR.

Click Download PDF to get a single-page A4 invoice PDF.

Click Save to store the booking locally (visible in Admin).

Click Share WhatsApp to open WhatsApp with a prefilled message.

Admin Panel

Open: Click Admin Panel (top-right).

Default password: admin123 (change it in the HTML for production).

Admin features:

Clear All: removes all bookings from localStorage.

Export CSV: downloads a CSV with the complete bookings list and payment metadata.

Search: search by order id, customer name, contact, or plan.

Pagination: choose page size (5/10/25) and navigate pages.

Actions per booking:

Mark Paid — opens a confirmation modal asking for an optional Transaction ID. On confirm, the booking is updated with paymentVerified = true, paymentTxId, and paymentTimestamp.

Export — exports a single booking CSV.

Delete — removes the booking.

Configuration (in the HTML)

Open the HTML and edit the top script config values as needed:

const STORAGE_KEY = 'apna_driver_bookings_final_v1'; // localStorage key
const ADMIN_PASSWORD = 'admin123';                    // change this
const UPI_ID = 'bhanupratapbiswas@ptyes';             // change to your UPI id


To change the company logo or details, replace the logo URL and text inside the HTML (header & invoice preview).

To add/remove plans, edit the <select id="planDropdown"> options (format: Label|Price|Info).

PDF Notes / How it Works

The app clones the visible invoice .invoice-box element and feeds it to html2pdf so the PDF matches the preview.

It waits for the QR image to load before starting PDF generation.

The PDF is constrained to A4 and uses compact CSS and tight margins to keep the invoice on one page.

If you find the PDF still breaks to 2 pages, try:

Using Chrome/Edge (most predictable).

Reducing the page size (page-size selector in admin) or reducing extra text in the invoice.

If necessary, tweak the html2canvas options or adjust CSS padding in the HTML.

CSV Export Columns

When you export bookings to CSV (all or single), the file includes these columns:

id, customerName, customerContact, customerAddress, plan, base, overtime, otRate, extras, total, upi, createdAt, paymentVerified, paymentTxId, paymentTimestamp


paymentTxId and paymentTimestamp are set when you use Mark Paid in Admin.

Security & Limitations

Local storage only — bookings are stored in the browser on the device where the app was used. If you need central persistence, integrate a backend (Node/PHP) and change the save/export functions to use an API.

Admin password is stored in the HTML (client-side). This is convenient for offline setups but not secure for multi-user or public deployments. For production, implement server-side authentication.

UPI payment verification is manual. Marking a booking paid does not contact any payment gateway.

QR generation uses api.qrserver.com to create QR images (no API key). That requires an internet connection for QR generation. If offline QR generation is required, integrate a local JS QR library.

Browser Recommendations

Best: Chrome or Edge (desktop/mobile) — consistent PDF generation with html2pdf.

Firefox: works, but PDF layout may vary in rare cases.

Mobile: modern Android Chrome / Safari on iOS should work fine; test PDF download behavior on your device (some mobile browsers use their own PDF viewers).

Troubleshooting

PDF splits to 2 pages

Make sure QR finished loading before clicking Download PDF.

Try Chrome/Edge.

Reduce extras/overtime text lengths, reduce padding, or edit CSS in the HTML to shrink fonts/paddings.

Saved bookings not appearing

Ensure you saved the booking using the Save button before opening Admin.

Check localStorage in browser dev tools (Application → Local Storage) and confirm the STORAGE_KEY value matches.

QR not showing

The app uses api.qrserver.com — check network connectivity.

Alternatively replace QR generation with a client-side QR library.

Extending the App

Ideas for future improvements:

Add on-screen digital signature canvas and embed the signature into PDFs.

Backend integration (Node/PHP) to persist bookings and protect admin access.

Integrate a payment gateway webhook to automatically confirm payments.

Multi-user admin with roles & authentication.

Add GST/tax calculations and invoice numbering per financial year.

License & Attribution

This project is provided as-is for your use and modification. You may reuse/modify it for personal or business purposes. No warranty is provided.

Third-party libraries used:

Bootstrap 5 (CSS/JS) — MIT-like license

html2pdf.js / html2canvas / jsPDF — respective open-source licenses (check upstream for full license text)

QR generation uses https://api.qrserver.com (public QR image API).

Contact / Help

If you want me to:

Add an on-screen signature drawer and include it in PDF

Convert LocalStorage to a simple backend (Node/PHP) with secure admin

Add GST calculation and more invoice fields

Reply with which feature and I’ll update the single-file app accordingly.
