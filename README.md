# Midway

Named for the sake of being the middle component missing from your business. Think of this repo as a middlewear to anything and everything custom, ecom, DTC and headless.

### Starter kit for [Gatsby](https://www.gatsbyjs.org/), [Sanity.io](https://www.sanity.io), & Shopify

This repo was forked from the work that [Lucas](https://github.com/lucasvocos/gatsby-sanity-shopify) did on an initial Sanity/Gatsby/Shopify repo. I've extended it to include various patterns that I use in my builds, more functions for handling accounts, typescript, and functional CSS to name a few. I also incldue some common components in my Sanity & Gatsby instance that I don't believe we should rebuild over and over, things like a press module, general ctas etc. Use whatever you'd like or just use it as a baseplate.

Clone this repository to bootstrap a fresh Gatsby site, powered by Sanity CMS and dynamically import Shopify products to Sanity with the help of a WebHook

## Basic Instructions

### Initial Setup
1. Remove remote repo by entering `rm -rf .git`
2. Either create a new repo in this folder and version control both Sanity & Gatsby, or set up new repos for both folders

### Studio/
1. In the `studio` folder run `sanity init` and create a new project.
2. Update `studio/sanity.json` and update the Project ID.
3. Update the studio name in `studio/package.json`.
3. Edit schemas, add different content types, find out more here: [Sanity Docs](https://www.sanity.io/docs/sanity-studio)
4. Include these schemas in the `deskStructure.js` export (include a fun icon!)

### Web/
1. Rename `env.example` to `.env` by typing `mv env.example .env` in your terminal.
2. Enter your Sanity API keys in the `.env` file.
3. Modify `gatsby-config.js` and add your site title, etc.
3. Develop your front end, etc. (purposely left this ultra stripped-down)
4. Create a repo specifically for your Gatsby build, host with Netlify or anywhere you can have a Lambda function.

### Shopify 

1. In your Netlify environment, go to your project and create a new Function.
2. Set the functions directory to be the `functions/` folder in your project.
3. In Shopify, go to `Settings -> Notifications -> Webhooks` and create webhooks for Product Creation, Updates, & Deletions (⚠️ Be careful with how you implement this, see more [here](https://github.com/lucasvocos/gatsby-sanity-shopify/blob/d69ed053dfa3e21b17a1c10e1b5697044774f70d/web/functions/shopify.js#L171)). Set the webhook's Callback URL to `[https://YOUR_URL.DOMAIN/.netlify/functions/shopify]` (if using Netlify, otherwise point to your provider's Lambda location)

<details>
<summary>Local Development of Functions</summary>
You can alternatively run your webhook locally, you can do this with ngrok
1. npm install ngrok -g
2. ngrok [:PORT] http
3. Point Shopify webhook to the above url +  /.netlify/functions/shopify
</details>

## Features

**A blank slate Gatsby site w custom webhook to create new Shopify products**
  * 📡 Real-time content preview in development
  * ⏱ Fast & frugal builds
  * 🗃 No accidental missing fields/types
  * 🧰 Full Render Control with Portable Text
  * 📸 gatsby-image support
  * 🔧 Minimal configuration
  * 💻 Custom lambda function that will create/update products from Shopify, as well as flag deleted items

**Sanity Studio with a schema for**
  * 🏢 Site settings
    * Menu configuration pattern
    * Basic Footer configuration pattner
  * 📃 Pages
    * Meta Card support for SEO with Tabs
    * Common modularity patterns
  * 📰 Posts
  * 🛍 Products & Variants
    * Products have default settings for `title`, `slug`, `defaultPrice`, `id`, `productId`.
    * Variants have default settings for `id`, `productId`, `variantId`, `title`, `variantTitle`, `sku`, and `price`.
    * The `web/functions/shopify` file will generate new Sanity documents with these default fields.


## Orginal Credits from Lucas

This entire repo is really just merged together from a stripped-down version of Sanity's [Sample company website built with Gatsby & Sanity.io](https://github.com/sanity-io/example-company-website-gatsby-sanity-combo) repo and a modified version of [Kevin Green](https://github.com/iamkevingreen)'s lambda function as discussed in the [Sanity + Shopify Roundtable: Headless ecommerce with Kevin Green & Joseph Thomas](https://www.youtube.com/watch?v=4mgI333aGvo) video.

## License

MIT
