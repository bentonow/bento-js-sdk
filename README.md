# Bento Javascript SDK
[![Build Status](https://travis-ci.org/bentonow/bento-ruby-sdk.svg?branch=master)](https://travis-ci.org/bentonow/bento-ruby-sdk)

🍱 Simple, powerful analytics for web projects!

Track events, update data, record LTV and more in Javascript. Data is stored in your Bento account so you can easily research and investigate what's going on.

👋 To get personalized support, please tweet @bento or email jesse@bentonow.com!

🐶 Battle-tested on Bento Production!

## Installation

When you sign up to Bento, you'll be able to copy and paste an `Embed Script`. There are two versions, please pick just one and add it to the header or footer of your site. Both scripts are async and deferred so will load after everything else has loaded.

### Simple
Initiates Bento and triggers `bento.view()`. Good for most websites that don't need much customization.
```js
<script src="https://fast.bentonow.com?site_uuid={Site Key}" async defer></script>
```

### Advanced
Loads Bento.js and fires off an event (`bento:ready`) that you can listen for. 
```js
<script src="https://app.bentonow.com/{Site Key}.js" async defer></script>
<script>
window.addEventListener("bento:ready", function () {
  if (typeof(bento$) != 'undefined') {
    bento$(function() {
        // bento.showChat();
        bento.view();
    });
  }
})
</script>
```
_Note: {Site Key} will automatically be replaced on the script page. Do not copy and paste the above verbatim_. 

## Identify

In Bento, all new visitors are anonymous. If you'd like to identify a visitor, simply run the following command _before_ you track an event or pageview.

```js
bento.identify("example@example.com");
```

After you do so, all future events sent from this users device will be correctly identified as that person. Worth mentioning that all previous events sent from that visitors device will also be associated to that user. Magic, right?

# Identify (Chat Only)

In Bento, if you wish to identify a user in chat (not requiring self-identification) then you can use the following method. It requires both an email AND an identifier (like a user_id or account_id in your database).

```js
window.addEventListener('bentochat:ready', function() {
    window.$bentoChat.setUser('<identifier>', {
        email: '<email>',
        name: 'Jane Doe',
        phone_number: ''
    });
    console.log('running this')
})
```

## Update Fields

If you'd like to update a visitors custom field (first_name, last_name, status, etc) run the following command _before_ you track an event or pageview.

```js
bento.updateFields({"first_name": "Ash", "last_name": "Ketchum"});
```

This will send their fields inside the event and update the visitor.

## Track (Create Event)

The following will build an event with a custom type/name and a details payload that you can filter by in Workflows. 

```js
bento.track("optin", {"organisation_name": "Team Rocket"});
bento.track("demo");
bento.track("download");
```

## Track Purchase (Create Unique Events)

The following will track a purchase and increase/decrease the LTV of a customer. Note that the `key` stops duplicate values being tracked, this is important if you're loading this script on a thank you page and it loads multiple times. Cool, huh?

```js
bento.track("purchase", {
  unique: {
    key: "INV1234", // a unique key — this stops duplicate unique events
  },
  value: {
    currency: "USD",
    amount: 1000, // in cents
  },
  cart: {
    items: [ // an array of items, can be any format
      {
        product_name: "Product 1",
        product_id: "1234",
        quantity: 1,
        price: 1000,
      },
    ],
  },
});
```

## Tag

Fires an event with a tag inside. This can trigger automations.

```js
bento.tag("demo_booked");
```

## Chat

```js
// Renders or hides chat bubble.
bento.showChat();
bento.hideChat();

// Opens or closes the chat window.
bento.openChat();
bento.closeChat();

```

## Get Email

If you have identified the device _at least once_ during the session you can fetch that information for your own use. This will usually be available if someone has logged in, opted in via Bento Capture, or used a form on your site.

```js
bento.getEmail()
```

## Spam Check

Got an important piece of content behind an opt-in and don't want your users putting fake emails in to get it? Leverage Bento's Spam API to ensure their email is correct before proceeding. NOTE: This _does not_ check MX records as that _can_ be super slow. 

```js
await bento.spamCheck(email)
```

## [DEPRECATED] Autofill

This fetches the visitors details (email and whitelisted fields) and automatically fills out all forms on the page.

```js
bento.autofill();
```

## [BETA] Track Subdomains

If you have traffic going to multiple subdomains and wish to track people throughout that journey simply run the following at least once per pageview. We will attempt to add the visitors identifier to each link. Please test this thoroughly before going live.

```js
bento.trackSubdomains(['example.com', 'test.example.com'])
```
