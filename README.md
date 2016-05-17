# recurringinvoices-paynow
A retrofit for the popular open source invoice software Bamboo Invoice that adds a recurring invoice feature. 

When the set recurring interval is reached a duplicate invoice is created. With the PayNow feature you can enter in your Google Merchant ID or PayPal e-mail into the Bamboo Invoice settings page to allow your customers to pay you via these services (a button will be added the PDFs generated).

This post aims to help users setup and use my Recurring Invoices + PayNow Bamboo Invoice mod.

## Requirements
- BambooInvoice v0.8.9
- MySQL v5.x.x+
- PHP v5.x.x+

## Installation
Extract the contents of the zip to the BambooInvoice root directory (overwriting files when prompted).

Execute the following MySQL query on your server (replacing table names with your table names):

ALTER TABLE bamboo_invoices ADD COLUMN recur_interval INT(11);
ALTER TABLE bamboo_settings ADD google_merchant_id VARCHAR(255),
ADD paypal_email VARCHAR(255);

Using crontab (or a similar program) setup the recur function to be executed every day. Here is an example crontab file:
# m h  dom mon dow   command
30 3 * * * wget http://www.mywebsite.com/bamboodir/index.php/recur
31 3 * * * rm -rf recur
