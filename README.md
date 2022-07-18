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
        bento.showChat();
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

## Update Fields

If you'd like to update a visitors custom field (first_name, last_name, status, etc) run the following command _before_ you track an event or pageview.

```js
bento.updateFields({"first_name": "Ash", "last_name": "Ketchum"});
```

This will send their fields inside the event and update the visitor.

## Track

The following will build an event with a custom type/name and a details payload that you can filter by in Workflows. 

```js
bento.track("optin", {"source": "test"});
bento.track("demo");
bento.track("download");
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

## Autofill

This fetches the visitors details (email and whitelisted fields) and automatically fills out all forms on the page.

## [BETA] Track Subdomains

If you have traffic going to multiple subdomains and wish to track people throughout that journey simply run the following at least once per pageview. We will attempt to add the visitors identifier to each link. Please test this thoroughly before going live.

```js
bento.trackSubdomains(['example.com', 'test.example.com'])
```
