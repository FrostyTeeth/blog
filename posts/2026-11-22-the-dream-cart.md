# Build Your Dream Cart Now

*2026-11-22 — marketing, advertising, strategy, opinion*

I love this advertisement for Vegain, a Canadian plant-based supplement store, and I have to tell you about it. Here's the pitch: for Black Friday they're giving away your dream (shopping) cart. Go to Vegain.ca, put the products you want in the cart, go to the checkout, and create a profile. On Friday they'll pick carts and give them away.

I like it because it gets the customer imagining what it's like to get these products, and it removes the shell of budget/pricing from the customer's mental state. But did you pick up on what they didn't say? I'll come back to that later.

Every step of entering is a step of buying: open the store, browse, pick a flavour, add it to the cart, add something else, go to the checkout. The only part you skip is the credit card. By the time you've built a dream cart you've spent a few minutes rehearsing what it's like to own all of it, and you did that to yourself, voluntarily, because you wanted to win.

This builds a sense of ownership called the endowment effect, where things feel more valuable because you own them.

So to recap, customers: A) learn how to navigate the website, B) select the products they want, C) build an emotional connection to those products, and D) create a profile on the website. The advertisement is a quadruple-whammy of brand building and purchase escalation.

## Why the Ad Works
### The right production
The casting is right. She's young, fit, and attractive, in a bright café-looking space with plants hanging behind her, which suits a supplement brand's idea of its own customer.

And what's super amazing is how she delivers it. She's enthusiastic and authentic, which is a hard thing to get out of someone reading an offer. She smiles (which builds trust with the audience), and her eyebrows and eyelids do the work of joy and surprise, so the excitement is in her face without being in her volume — she isn't yelling. She is calm and clear. The offer lands as good news, not pressure.

To walk you through how easy it is to enter, an overlay shows a phone screen with the store on it, and you watch products get added to a cart and the page scroll along.

The speaking part is present with on-screen captions, since some people scroll reels with the sound off sometimes/all the time, this easy accessibility step goes a long way to communicating the offer.

### The right targeting

What the ad didn't say, as I teased earlier, is anything about the product or the brand. I've purchased a product from them before (I think it was through an Instagram advertisement). Having the right data tools allows for an ad like this to be so short, because the store already knows who it's talking to. It also lets them follow up with the same people later, for the next campaign.

There are several marketing tracking tools on Vegain.ca (listed below) and one is Meta's Conversions API (CAPI), which can match the web actions to the Instagram ad.

### How Meta's Conversions API Works

1. Someone taps the ad in Instagram. Meta adds a click ID (fbclid) to the link, and the store opens in Instagram's in-app browser.
2. The Meta Pixel in the page records that click ID in a cookie (_fbc), along with a browser ID (_fbp).
3. As the visitor adds to the cart, checks out, and buys, Shopify's server sends those same events to Meta through CAPI, along with the click ID, the browser ID, and, if the store has chosen to share it, a hashed email once they've created a profile.
4. Meta removes the duplicate copies from the Pixel and CAPI and matches the events to the Instagram ad click, so the cart and the sale are credited to the ad.

## I Want

**Which brings me to it. I'm going to go add a bunch of stuff to my cart right now. Why not? It can't hurt. If I don't win, I'll probably remove a few things after Black Friday and buy one or two items that I'd value anyway.**

![I love this advertisement](images/i-love-this-advertisement.png)

## What Marketing Tracking Tools Are Installed on Vegain.ca?

| Tracking | What it does |
|---|---|
| Meta Pixel | Records site visits and purchases and ties them back to the Instagram ad that brought the visitor. |
| Meta Conversions API | Sends the same events from the server, so they still count when iOS privacy settings or ad blockers block the Pixel. |
| Google Analytics (GA4) | Shows where visitors came from and what they did, Instagram included. |
| Google Ads tag | Tracks conversions for Google ads only. |
| TikTok Pixel | Tracks conversions for TikTok ads only. |
| Klaviyo | Links a visitor to an email address and what they put in the cart, so Vegain can follow up. |
| Microsoft Clarity | Records sessions and heatmaps of how visitors move around the site. |
| Shopify analytics | Reports sales and traffic sources in the store's own dashboard. |

## Advertisement Transcript

> As a part of our Black Friday deal,
> we are doing something crazy.

> We are giving away your Vegain dream cart.
> All you have to do is go to Vegain.ca, build your dream cart,
> go to the checkout and create a profile.

> And then on Friday, 
> we'll randomly be picking a bunch of carts
> and giving them away.
>
> Winners get picked this Friday, so start building your carts now.

Source: [Vegain's Instagram ad](https://www.instagram.com/p/Df8eTlcMoVf/)
