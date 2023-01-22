---
name: Edge Redirects with Upstash
slug: edge-redirects-upstash
description: Redirect from a list of redirects both hardcoded and coming from Upstash (Redis), that get evaluated at the edge.
framework: Next.js
useCase: Edge Functions
css: Tailwind
deployUrl: https://vercel.com/new/clone?repository-url=https://github.com/vercel/examples/tree/main/edge-functions/redirects-upstash&env=UPSTASH_REST_API_DOMAIN,UPSTASH_REST_API_TOKEN,UPSTASH_EDGE_API_DOMAIN,UPSTASH_EDGE_API_TOKEN&project-name=redirects-upstash&repository-name=redirects-upstash
demoUrl: https://edge-functions-redirects-upstash.vercel.app
---

# Edge Redirects with Upstash

This demo features a list of redirects, both hardcoded and coming from Redis ([Upstash](https://upstash.com/)), that get evaluated at the edge.

The demo has a total of 10,000 redirects, 1,000 of which are hardcoded on a JSON file, and 9,000 added to Redis.

Redirects in a JSON file are faster to evaluate, but they can only be edited at build time, with Redis we can have editable redirects with a low latency cost.

## Demo

https://edge-functions-redirects-upstash.vercel.app

### One-Click Deploy

Deploy the example using [Vercel](https://vercel.com?utm_source=github&utm_medium=readme):

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/vercel/examples/tree/main/edge-functions/redirects-upstash&env=UPSTASH_REST_API_DOMAIN,UPSTASH_REST_API_TOKEN,UPSTASH_EDGE_API_DOMAIN,UPSTASH_EDGE_API_TOKEN&project-name=redirects-upstash&repository-name=redirects-upstash)

## Getting Started

Execute [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app) with [npm](https://docs.npmjs.com/cli/init) or [Yarn](https://yarnpkg.com/lang/en/docs/cli/create/) to bootstrap the example:

```bash
npx create-next-app --example https://github.com/vercel/examples/tree/main/edge-functions/redirects-upstash redirects-upstash
# or
yarn create next-app --example https://github.com/vercel/examples/tree/main/edge-functions/redirects-upstash redirects-upstash
```

You'll need to have an account with [Upstash](https://upstash.com/). Once that's done, copy the `.env.example` file in this directory to `.env.local` (which will be ignored by Git):

```bash
cp .env.example .env.local
```

Then open `.env.local` and set the environment variables to match the REST API and Edge API of your database. It should look like this:

```bash
# Upstash REST API
UPSTASH_REST_API_DOMAIN = "us1-shiny-firefly-12345.upstash.io"
UPSTASH_REST_API_TOKEN = "your-api-token"

# Upstash Edge API
UPSTASH_EDGE_API_DOMAIN = "us1-shiny-firefly-12345.edge-a.upstash.io"
UPSTASH_EDGE_API_TOKEN = "your-edge-token"
```

We populate the redirects in Upstash in [scripts/upstash.js](scripts/upstash.js) using their REST API, if you prefer not to do that then set `POPULATE_REDIS` to `false` in `.env`. JSON redirects are also created there.

We use the Edge API to have the lowest latency possible when fetching a redirect, it's also possible to only use the REST API by replacing `upstashEdge` with `upstashRest` in [lib/redirects.ts](lib/redirects.ts).

Next, run Next.js in development mode:

```bash
npm install
npm run dev

# or

yarn
yarn dev
```

Deploy it to the cloud with [Vercel](https://vercel.com/new?utm_source=github&utm_medium=readme&utm_campaign=edge-middleware-eap) ([Documentation](https://nextjs.org/docs/deployment)).
