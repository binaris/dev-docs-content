---
title: Reshuffle Custom Domains
route: custom-domains
description: ‘How to add a custom domain to your Reshuffle site’
category: 'Main Concepts'
priority: 16
---

# Reshuffle Custom Domains

All Reshuffle apps are available via their automatically provisioned “app domain”, ie:

`https://focused-weasel-32.reshuffle.app`

Reshuffle custom domains enables you to use a domain you own for any Reshuffle app, ie:

`www.revered-weasel.com`

Follow the steps below to get your Reshuffle app connected to a custom domain.

## Table of contents

* [Key terms](#key-terms)
* [Adding a custom domain](#adding-a-custom-domain-to-reshuffle)
     * [Adding a subdomain](#adding-a-subdomain-wwwrevered-weaselcom)
          * [Adding a CNAME to namecheap](#adding-a-cname-to-namecheap)
          * [Adding a CNAME to GoDaddy](#adding-a-cname-to-godaddy)
          * [Additional resources](#additional-resources)
     * [Adding an apex domain](#adding-an-apex-domain-revered-weaselcom)
          * [Adding an ALIAS to namecheap](#adding-an-alias-to-namecheap)
          * [Adding an ALIAS to GoDaddy](#adding-an-alias-to-godaddy)
     * [Waiting for verification](#waiting-for-verification)
* [Removing a custom domain](#removing-a-custom-domain-from-reshuffle)

## Key terms

**Subdomain**: the portion of a URL that comes before the domain. `www` is the most common subdomain ie: `www.placeholder.com`, but there are many other popular subdomains (`api`, `dev`, `blog`, etc…). Subdomains are configured with a `CNAME` record. 

**Apex (root) domain**: domain that does not contain a subdomain, ie: `placeholder.com`. Apex domains are configured with an `ALIAS` record.

**Reshuffle app domain**: domain that is automatically provisioned for each Reshuffle app, ie: `fancy-cat-2359.reshuffle.app`.

**CNAME**: DNS record which allows one domain to point to another domain, ie: `www.placeholder.com` -> `www.holderplace.com`. A `CNAME` record can only point to another domain, never an IP address.

**ALIAS**: Virtual DNS record that provides CNAME-like behavior but for *Apex* domains.

**DNS provider**: maintains the DNS servers that translate a custom domain name to a destination (Reshuffle in this case). The DNS provider is where any and all records (`CNAME` and `ALIAS`) must be configured.

**Domain registrar (registrar)**: service that allows you to buy and register an available domain of your choosing.

## Adding a custom domain to Reshuffle

The first step of setting up a custom domain for your Reshuffle app is to purchase/acquire a domain. At this time, Reshuffle is not a domain registrar and therefore does not offer the ability to purchase a domain directly. Instead, we recommend you purchase a domain from a trusted third-party registrar such as:


* [Namecheap](https://www.namecheap.com/)
* [Google domains](https://domains.google/)
* [Cloudflare](https://www.cloudflare.com/products/registrar/)

Once you have the custom domain you wish to use for your Reshuffle app, proceed to the ‘application’ page for your app, ie: 

`https://reshuffle.com/application/focused-weasel-32`

Next, click the “ADD CUSTOM DOMAIN” button located in the domains section of the UI:

![add-custom-domain-showcase -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/add-custom-domain-showcase.png)




Clicking this button will open a dialog where you’ll be asked to provide the custom domain you want to add to your Reshuffle app. Once you’ve provided your domain, use the continue button to move on to the next step of the process.

![add-custom-domain-dialog-continue -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/add-custom-domain-dialog-continue.png)




The next step will differ slightly based on the type of domain you entered.

### Adding a subdomain (www.revered-weasel.com)

To add a subdomain such as `www.revered-weasel.com`, Reshuffle requires you to add a `CNAME` record to your domain registrar:

![add-cname-record-dialog -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/add-cname-record-dialog.png) 





This process will change based on your registrar of choice. Examples for some of the most popular registrars are shown below.

#### Adding a CNAME to namecheap

If you’re planning to add the `www` subdomain, you should first remove the default `www`, `CNAME` namecheap provides:

![delete-default-cname-namecheap -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/delete-default-cname-namecheap.png)





Next, add your Reshuffle app’s default domain as a `CNAME` record. Remember to replace “Host” if you’re attempting to setup a non `www` subdomain.

![add-cname-namecheap -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/add-cname-namecheap.png)





#### Adding a CNAME to GoDaddy

If you’re planning to add the `www` subdomain, you should first remove the default `www` `CNAME` GoDaddy provides:

![delete-default-cname-godaddy -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/delete-default-cname-godaddy.png)





Next, add your Reshuffle app’s default domain as a `CNAME` record. Remember to replace “Host” if you’re attempting to setup a non `www` subdomain.

![add-cname-godaddy -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/add-cname-godaddy.png)





#### Additional resources

* [Changing a domains DNS on namecheap](https://www.namecheap.com/support/knowledgebase/article.aspx/767/10/how-to-change-dns-for-a-domain)
* [Adding a CNAME record with GoDaddy](https://www.godaddy.com/help/add-a-cname-record-19236)
* [Adding a CNAME record with Google domains](https://support.google.com/domains/answer/9211383?hl=en) 

### Adding an apex domain (revered-weasel.com)

To add an apex domain such as `revered-weasel.com`, Reshuffle requires you to add an `ALIAS` record to your domain registrar:

![add-alias-record-dialog -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/add-alias-record-dialog.png)





Depending on your specific registrar, this process will differ slightly. Unfortunately, not all registrars support `ALIAS` records at this time. Examples for some popular registrars that do support `ALIAS` records are shown below.

#### Adding an ALIAS to namecheap

Before you add an `ALIAS` record, remove the URL redirect record that namecheap automatically adds to all your sites:

![remove-url-redirect-record-namecheap -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/remove-url-redirect-record-namecheap.png)




Next, in the namecheap domains UI, add your Reshuffle app’s default domain as an `ALIAS` record. 

![add-alias-namecheap -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/add-alias-namecheap.png)






[Here is a detailed article which describes the process of adding an `ALIAS` record to namecheap.](https://www.namecheap.com/support/knowledgebase/article.aspx/10128/2237/how-to-create-an-alias-record)


#### Adding an ALIAS to GoDaddy
GoDaddy does not natively support the `ALIAS` record type, instead you’ll need to configure a 301 redirect. A 301 redirects traffic from the apex domain to another valid subdomain or apex domain. To add a redirect with GoDaddy, start by visiting the DNS management for your domain:

![manage-domains-godaddy -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/manage-domains-godaddy.png)



Once you’re on the DNS management page for your domain, scroll down to the “Forwarding” section located near the bottom of the page and click “ADD”  for the “DOMAIN” entry:

![forwarding-section-godaddy -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/forwarding-section-godaddy.png)


Finally, configure the forward to use your Reshuffle app URL or a previously configured subdomain:

![add-forward-godaddy -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/add-forward-godaddy.png)



[Read more about redirecting with GoDaddy here](https://help.instapage.com/hc/en-us/articles/206028427-How-do-I-create-a-301-redirect-for-a-root-naked-domain-in-my-GoDaddy-account-)


### Waiting for verification

After adding the record to your registrar, you should be able to verify your domain in the Reshuffle UI:

![continue-with-verified-domain -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/continue-with-verified-domain.png)




Keep in mind that propagation of the added record can take some time. Once the DNS has finished propagating, the Reshuffle verification process will finish and you’ll be greeted with a screen similar to this:


![live-cname -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/live-cname.png)





## Removing a custom domain from Reshuffle

To remove a domain, navigate to the page for your reshuffle app, ie:

`https://reshuffle.com/application/<YOUR_APP_NAME_HERE>`

For example, for `focused-weasel-32` the URL would be:

`https://reshuffle.com/application/focused-weasel-32`

On the application page, click the delete button (shown below) for the specific domain you wish to remove:

![remove-a-domain -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/remove-a-domain.png)




Before removal, you’ll be asked to confirm by manually typing the custom domain:

![remove-a-domain-confirmation -maxwidth](https://raw.githubusercontent.com/binaris/dev-docs-content/master/assets/custom-domains/remove-a-domain-confirmation.png)


<br />
<br />

