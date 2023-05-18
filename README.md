[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fvercel%2Fcommerce&project-name=saleor-nextjs-commerce&repo-name=saleor-nextjs-commerce&demo-title=Saleor%20Next.js%20Commerce&demo-url=https%3A%2F%2Fnextjs-commerce-git-v2-saleorcommerce.vercel.app&demo-image=https%3A%2F%2Fbigcommerce-demo-asset-ksvtgfvnd.vercel.app%2Fbigcommerce.png&env=SALEOR_INSTANCE_URL,SITE_NAME,TWITTER_CREATOR,TWITTER_SITE)

# Next.js Commerce

> Note: Looking for Next.js Commerce v1? View the [code](https://github.com/saleor/nextjs-commerce/tree/v1), [demo](https://commerce-v1.vercel.store), and [release notes](https://github.com/vercel/commerce/releases/tag/v1)

A Next.js 13 and App Router-ready e-commerce template, built with Saleor, featuring:

- Next.js App Router
- Optimized for SEO using Next.js's Metadata
- React Server Components (RSCs) and Suspense
- Route Handlers for mutations
- Edge runtime
- New fetching and caching paradigms
- Dynamic OG images
- Styling with Tailwind CSS
- Checkout and payments with Saleor
- Automatic light/dark mode based on system settings

## Running locally

You will need to use the environment variables [defined in `.env.example`](.env.example) to run Next.js Commerce. It's recommended you use [Vercel Environment Variables](https://vercel.com/docs/concepts/projects/environment-variables) for this, but a `.env` file is all that is necessary.

> Note: You should not commit your `.env` file or it will expose secrets that will allow others to control your Saleor store.

1. Install Vercel CLI: `npm i -g vercel`
2. Link local instance with Vercel and GitHub accounts (creates `.vercel` directory): `vercel link`
3. Download your environment variables: `vercel env pull`

```bash
pnpm install
pnpm dev
```

Your app should now be running on [localhost:3000](http://localhost:3000/).

## How to configure your Saleor store for Next.js Commerce

Next.js Commerce requires a [Saleor account](https://saleor.io/).

### Add the Saleor URL to an environment variable

Create a `SALEOR_INSTANCE_URL` environment variable and use your Saleor GraphQL API URL as the value (ie. `https://yourinstance.saleor.cloud/graphql/`).

### Accessing the Saleor Storefront API

Next.js Commerce utilizes [Saleor's Storefront API](https://docs.saleor.io/docs/3.x/api-storefront/api-reference) to create unique customer experiences. The API offers a full range of commerce options making it possible for customers to control products, collections, menus, pages, cart, checkout, and more.

### Configure webhooks for on-demand incremental static regeneration (ISR)

Coming soon.

### Using Saleor as a CMS

Next.js Commerce is fully powered by Saleor in a truly headless and data-driven way.

#### Products

`https://yourinstance.saleor.cloud/dashboard/products/`

Only `Active` products are shown. `Draft` products will not be shown until they are marked as `Active`.

Product options and option combinations are driven by Saleor options and variants. When selecting options on the product detail page, other options and variant combinations will be visually validated and verified for availability, as Amazon does.

Products that are active and "out of stock" are still shown on the site, but the ability to add the product to the cart is disabled.

#### Collections

`https://yourinstance.saleor.cloud/dashboard/collections/`

Create whatever collections you want and configure them however you want. All available collections will show on the search page as filters on the left, with one exception...

Any collection names that start with the word "hidden" will not show up on the headless front end. The Next.js Commerce theme comes pre-configured to look for two hidden collections. Collections were chosen for this over tags so that order of products could be controlled (collections allow for manual ordering).

Create the following collections:

- `Featured` -- Products in this collection are displayed in the three featured blocks on the homepage.
- `All Products` -- Products in this collection are displayed in the auto-scrolling carousel section on the homepage.

#### Pages

`https://yourinstance.saleor.cloud/dashboard/pages/`

Next.js Commerce contains a dynamic `[page]` route. It will use the value to look for a corresponding page in Saleor. If a page is found, it will display its rich content using Tailwind's prose. If a page is not found, a 404 page is displayed.

#### Navigation menus

`https://yourinstance.saleor.cloud/dashboard/navigation/`

Next.js Commerce's header and footer navigation is pre-configured to be controlled by Saleor navigation menus. This means you have full control over what links go here. They can be to collections, pages, external links, and more.

Create the following navigation menus:

- `navbar` -- Menu items to be shown in the headless frontend header.
- `footer` -- Menu items to be shown in the headless frontend footer.

#### SEO

Saleor's products, collections, pages, etc. allow you to create custom SEO titles and descriptions. Next.js Commerce is pre-configured to display these custom values but also comes with sensible default fallbacks if they are not provided.
