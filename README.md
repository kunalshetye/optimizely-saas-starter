# Optimizely CMS Frontend Starter

This is a [Next.js](https://nextjs.org/) project for [Optimizely CMS](https://www.optimizely.com/cms) bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app). It contains the minimum required code to start building your own frontend on top of Optimizely CMS.

## Install the starter
To install this example/starter, use the command: `yarn create next-app -e https://github.com/remkoj/optimizely-saas-starter my-great-project`. This will install this starter into the `my-great-project` folder within the current directory.

[`create-next-app` CLI Reference](https://nextjs.org/docs/pages/api-reference/create-next-app)

## Getting Started

### 1. Create the connection between your frontend and CMS
Within the root folder of this project create a `.env.local`, which will hold the keys to your CMS instance. The default `.gitignore` file will make sure that the keys in this file will not be commited into the repository.

First, start by adding the URL at which the CMS has been installed. This is typically something like https://[your instance].cms.optimizely.com/
```bash
OPTIMIZELY_CMS_URL=https://example.cms.optimizely.com/
```

Second, within your CMS, go to the dashboard and define the connection to Optimizely Graph using the variables shown below.
```bash
OPTIMIZELY_GRAPH_GATEWAY=
OPTIMIZELY_GRAPH_SINGLE_KEY=
OPTIMIZELY_GRAPH_APP_KEY=
OPTIMIZELY_GRAPH_SECRET=
```

Third, within your CMS, go to "Settings" > "API Clients" and create a new API Client. Define the credentials with the variables below.
```bash
OPTIMIZELY_CMS_CLIENT_ID=
OPTIMIZELY_CMS_CLIENT_SECRET=
```

You can find the default configuration, and more configuration options within the `.env` file

### 2. Reflect the CMS structure in the frontend
Now, with the connection defined, create the default components to reflect the structure.

```bash
# Export all type definitions into the frontend codebase, for reference
# and easy type updates 
yarn opti-cms types:pull

# Export all style definitions into the frontend codebase, for reference
# and easy type updates 
yarn opti-cms styles:pull

# Create placeholders for all components registered within the CMS
yarn opti-cms nextjs:create
```

### 3. Test/build the frontend
```bash
# Generate the types and functions from GraphQL, based on the components
# inside your frontend. This needs to run successfully once before the
# dev-server can be started.
yarn compile

# Start the dev-server
yarn dev
```

### 4. Customize the components
By default all components are created in `src/components/cms`, you can now start modifying these components to build your site. The commands from step 2 are non-destructive, so you can re-run them as you define more content types within the CMS.

## Debugging starter points
- The compilation of GraphQL queries should complete with errors, if not, running `yarn compile --verbose` typically yields more detailed information on the cause of the error.
- Content does not update after publishing in the CMS. In a deployed scenario, Optimizely Graph sends a webhook to notify the frontend of the change. Locally this does not work, so you need to publish manually by navigating to: `http://localhost:3000/api/content/publish?token=$OPTIMIZELY_PUBLISH_TOKEN` (replace `$OPTIMIZELY_PUBLISH_TOKEN` with the value from your .env / .env.local file). Run `yarn webhook:list` to see recipients of content updates.