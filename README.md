<p align="center"><img src="/art/bento-javascript-sdk.png" alt="Bento Javascript SDK"></p>

[![Build Status](https://travis-ci.org/bentonow/bento-ruby-sdk.svg?branch=master)](https://travis-ci.org/bentonow/bento-ruby-sdk)

> [!TIP]
> Need help? Join our [Discord](https://discord.gg/ssXXFRmt5F) or email jesse@bentonow.com for personalized support.

The Bento JavaScript SDK makes it quick and easy to build an excellent analytics experience in your web application. We provide powerful and customizable APIs that can be used out-of-the-box to track your users' behavior, manage subscribers, and integrate chat functionality. We also expose low-level APIs so that you can build fully custom experiences.

Get started with our [📚 integration guides](https://docs.bentonow.com), or [📘 browse the SDK reference](https://docs.bentonow.com/subscribers).

Table of contents
=================

<!--ts-->
* [Features](#features)
* [Requirements](#requirements)
* [Getting started](#getting-started)
    * [Installation](#installation)
* [Modules](#modules)
* [Things to Know](#things-to-know)
* [Contributing](#contributing)
* [License](#license)
<!--te-->

## Features

* **Simple event tracking**: We make it easy for you to track user events and behavior in your application.
* **Visitor identification**: Identify your visitors to associate events with specific users.
* **Custom fields**: Track and update custom fields for your visitors to store additional data.
* **Purchase tracking**: Monitor customer purchases and calculate lifetime value (LTV) for your subscribers.
* **Chat integration**: Easily integrate and control Bento's chat functionality in your application.
* **Spam checking**: Validate email addresses to ensure data quality.
* **Subdomain tracking**: Track visitors across multiple subdomains of your website.

## Requirements

The Bento JavaScript SDK can be used in any modern web browser.

Bento Account for a valid **SITE_UUID**.

## Getting started

### Installation

Add one of the following scripts to your website's header or footer:

#### Simple Installation

```html
<script src="https://fast.bentonow.com?site_uuid={Site Key}" async defer></script>
```

#### Advanced Installation

```html
<script src="https://app.bentonow.com/{Site Key}.js" async defer></script>
<script>
window.addEventListener("bento:ready", function () {
  if (typeof(bento$) != 'undefined') {
    bento$(function() {
        bento.view();
    });
  }
})
</script>
```

Replace `{Site Key}` with your actual Bento site key.

## Modules

### Visitor Identification

Identify a visitor:

```javascript
bento.identify("user@example.com");
```

Identify a user for chat only:

```javascript
window.addEventListener('bentochat:ready', function() {
    window.$bentoChat.setUser('user123', {
        email: 'user@example.com',
        name: 'Jane Doe',
        phone_number: '1234567890'
    });
})
```

### Custom Fields

Update visitor's custom fields:

```javascript
bento.updateFields({
    "first_name": "Ash", 
    "last_name": "Ketchum"
});
```

### Event Tracking

Track a custom event:

```javascript
bento.track("optin", {"organisation_name": "Team Rocket"});
```

Track a purchase:

```javascript
bento.track("purchase", {
  unique: {
    key: "INV1234",
  },
  value: {
    currency: "USD",
    amount: 1000,
  },
  cart: {
    items: [
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

### Tagging

Add a tag to a visitor:

```javascript
bento.tag("demo_booked");
```

### Chat Integration

Show or hide chat:

```javascript
bento.showChat();
bento.hideChat();
```

Open or close chat window:

```javascript
bento.openChat();
bento.closeChat();
```

### Utility Functions

Get visitor's email:

```javascript
const email = bento.getEmail();
```

Check if an email is spam:

```javascript
const isSpam = await bento.spamCheck(email);
```

### Subdomain Tracking

Track visitors across subdomains:

```javascript
bento.trackSubdomains(['example.com', 'test.example.com']);
```

## Things to Know

1. All events are initially anonymous until a visitor is identified.
2. The `identify` method associates all previous and future events from a device with the provided email.
3. Custom fields should be updated before tracking an event or page-view.
4. The `unique.key` in purchase tracking prevents duplicate tracking of the same purchase.
5. Subdomain tracking is currently in beta and should be thoroughly tested before use in production.

## Contributing

We welcome contributions! Please see our [contributing guidelines](CONTRIBUTING.md) for details on how to submit pull requests, report issues, and suggest improvements.

## License

The Bento SDK for javascript is available as open source under the terms of the [MIT License](LICENSE).