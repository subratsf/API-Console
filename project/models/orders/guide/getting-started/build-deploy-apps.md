---
description: ""
date: "2020 - May - 26"
draft: false
author: sejal.parikh
---

# Build and Deploy the Sample App

If you're already a B2C Commerce customer and part of the Beta program, you can build and deploy our sample app using these steps. The sections below have more details about each step.

- **Prepare the platform**: Prepare a B2C Commerce sandbox.
- **Configure access**: Create a client ID.
- **Create the app**: Use the create-commerce-app tool to build the app.

## Prerequisites

Before you begin, you'll need a few tools and accounts configured.

- **Node.js environment**: Make sure you have [Node.js 12](https://nodejs.org/en/) installed, with at least npm (Node Package Manager) 5.2+. You also need the npx tool, which is a package runner that installs with npm 5.2+. For best results, use a node version manager such as NVM to manage Node.js versions.
- **Yarn**: You'll need the [yarn package manager](https://yarnpkg.com/).
- **Git**: To complete some of the steps in this procedure, you'll need to have the Git version control system installed.
- **A B2C Commerce account**: To access the platform, you'll need an Account Manager account. Check with your administrator if you don't have an account.
- **A B2C Commerce sandbox**: [On Demand Developer Sandboxes](https://documentation.b2c.commercecloud.salesforce.com/DOC1/topic/com.demandware.dochelp/Sandboxes/DeveloperSandboxes.html) are a perfect fit since you can manage them with CI/CD tools similar to what you use to manage your headless apps. Your sandbox must be enabled for the Beta program.

## Prepare the Platform

Make sure there's data in your storefront so that you can see the features of the sample app once you've got it running. If you're starting with a blank sandbox, you can install sample data. See [Use Site Import/Export to Import Reference Application Demo Sites](https://documentation.b2c.commercecloud.salesforce.com/DOC1/topic/com.demandware.dochelp/ImportExport/UsingSiteImportForReferenceApplicationDemos.html) for details.

## Configure Access

- **Create a client ID**. Log into Account Manager and create a client ID. The sample app uses the client ID to authenticate itself.
- **Authorize access to APIs**. The client requires permission to access the Commerce APIs. We've provided text in JSON format that you can copy into Business Manager to give the client all the right access. In Business Manager, go to **Administration > Site Development > Open Commerce API Settings**. For type, select Shop and for context, select your site, or Global to cover all sites. Paste the JSON CLOB here into the Business Manager screen, replacing the client ID in the JSON with your new client ID.

## Create App

1. **Download the git repo**: npx create-commerce-app yourappname
2. **Change into your app folder**: cd yourappname
3. Copy the packages/storefront-lwc/app/api.example.js file, save it as packages/storefront-lwc/app/api.js, and make sure api.js is added to your .gitignore file.
4. In api.js, provide values for the following variables (you can obtain these values from your Account Executive (AE) or Customer Support Manager (CSM)):

   - `COMMERCE_CLIENT_API_SITE_ID`: Unique site ID (for example, `RefArch` or `SiteGenesis`).
   - `COMMERCE_CLIENT_CLIENT_ID`: Unique ID used exclusively for API access. See Add a Client API for more information.
   - `COMMERCE_CLIENT_REALM_ID`: Unique four-character ID (for example, `bblx`).
   - `COMMERCE_CLIENT_INSTANCE_ID` : Unique instance ID within a realm (for example, `015` for an on-demand sandbox).
   - `COMMERCE_CLIENT_SHORT_CODE`: Unique region-specific merchant identifier (for example, `staging-001`).
   - `COMMERCE_SESSION_SECRET`: Unique ID for session management (for example, `thisisasecretkey`).
   - `COMMERCE_CORS`: Optionally enable CORS for GraphQL on the defined domains (for example, enable all domains with `\*`).

   > If the COMMERCE_SESSION_SECRET key is not unique per customer application, session information can be unintentionally shared between ecommerce sites.

5. **Install dependencies**: `yarn`
6. **Build the sample application**: `yarn build`
7. **Start the sample application**: `yarn start:dev` (development mode) or yarn start (production mode)
8. **Access the sample application**: open your browser to <http://localhost:3000.>
9. (Optional) Test the sample app: `yarn test`.
