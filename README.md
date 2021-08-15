# Tacoma Consignment Project Overview

Tacoma Consignment is a "brick-and-mortar" retail consignment business specializing in furniture and art. It is transitioning from a in-person based Quickbooks POS system to a joint online/in-person commerce system based on the following technologies:

* Shopify (eCommerce and POS)
* Stripe for consignor payout
* Cloudinary for image storage and CDN
* Azure SQL Server as master database and "source of truth" (open to discussion, but relational db preferred)
* Auth0 for identity management of:
  * consignors
  * customers
  * store staff
  * store admins
* Vuetify as a web front-end
* Segment for referral tracking and customer insights
* Axios for API management
* Mailchimp for email management and marketing campaigns

## MVP Feature Overview

The core system needs to enable the following roles and activities:

* Vuetify front-end based Store management single-page application including product onboarding with proper commission attribution and financial treatment of vendors and consignors
  * Product creation page and product-image upload via Vuetify web front-end, published to Shopify
  * Wishlist management via customer signup (Vuetify front-end) and product tagging on Shopify website
  * Print QR-code based product tag with product description, price, sku on Zebra, Epson, or other wireless label printer
  * Open-ended wishlist form analogous to product creation flow
* Customer signup flow that uses [Auth0](https://auth0.com/docs/quickstart/spa/vuejs) Shopify and other social connectors (Google, Facebook, Amazon, and [magic email links](https://auth0.com/docs/connections/passwordless/guides/email-magic-link)) to authorize customer, create an account in Azure and publish the results to appropriate Shopify and Mailchimp campaigns
  * New accounts trigger appropriate discount assignments and Mailchimp campaigncustomer discount via mailchimp email signup
  * Customer management including authentication via Auth0, referral tracking via Segment, and appropriate updating of relevant Mailchimp campaigns
* New consignor onboarding system, including invite system to transition existing merchants to new portal and payout alternatives
  * commission structures
  * active and sold products
  * billing address
  * PDF versions of contracts
* Vendor and consignor payout via automated payout on Stripe or manual checks generated from a PDF template and printed; Azure system must enforce proper accounting
* Synching transactions within and across systems:
  * Products, consignors, and staff store management functionality within Azure
  * Automated synchronization with Shopify via Webhooks
  * Communicate with web front-end via Vuetify/Axios/Azure/Auth0
  * Job execution of automatic discounting functionality
  * Publishing and synching data to Shopify via Shopify REST (or Graph) API

The Tacoma Consignment SQL Server database is the source of truth for all data. To do so it has to also capture all the external transactions that occur in the Shopify and Stripe systems, as well as integrate into the Vuetify front-end to enable the management of the store.

