# Salesforce Commerce Cloud plugin for New Relic Browser

## To Do
- Move `beacon` params into some simple per-application configuration setup that is inject as JSON in the page

[![Experimental Project header](https://github.com/newrelic/opensource-website/raw/master/src/images/categories/Experimental.png)](https://opensource.newrelic.com/oss-category/#experimental)

# New Relic Browser for SalesForce Commerce Cloud

A plugin to SalesForce Commerce Cloud (aka SFCC aka Demandware) that adds the New Relic Browser Javascript snippet to the header of every SFCC Site page.

## Local Installation

1. Clone this repository
2. Install the project's dependencies by running `npm install` in the repository root folder.

## Configuration
1. Edit `package.json`, modify `paths.base` property to point to your local `app_storefront_base` cartridge.
  - You can find the [Store Front Reference Architecture](https://github.com/SalesforceCommerceCloud/storefront-reference-architecture) here if you don't have it.
2. Open the [New Relic Browser UI](https://one.newrelic.com/launcher/browser-nr1.browser-home) and click the `(+) Add More` button in the top-right corner.
    **Note:** if you have access to multiple acccounts, be sure to choose the account you want to deploy to from the pull-down menu.
3. In the "Get started with New Relic Browser" page, choose the following:
  - Deployment Method: `Copy/Paste Javascript code` method.
  - Instrumentation: 'Pro' (recommended) or 'Lite' Instrumentation.
    **Note:** 'Pro + SPA' will work, but SFCC sites are not Single-Page Apps (as of the writing of this README), so those postions of the UI will be empty. Using 'Pro' or 'Lite' will hide those pages and the Summary page will populate properly.
  - Name your app: choose "No. (Name your standalone app)" and name it however you like.
    **Note:** Do not associate it with an existing APM application, as this will have unintended consequences in the UI!
3. Replace the contents of `cartridges/plugin_newrelic_browser/cartridge/client/default/js/nr-agent.js` with your Copy/Paste snippet.
   **Note:** You MUST comment-out or delete the `<script type="text/javascript">` and `</script>` HTML tags from your snippet. The portion you *do* want to preserve starts with: `window.NREUM||(NREUM={})...`
4. Run `npm run compile:js` in the repository root folder to create client-side assets. These are found in `cartridges/plugin_newrelic_browser/cartridge/state`
5. Configure `dw.json` with your Business Manager or API client credentials and your Site version. (There are examples of `dw.json` packaged with this plugin for both authentication types).

## Deployment & Verification
1. Upload the plugin by running `npm run uploadCartridge` in the repository root folder.
2. In SFCC Business Manager, add `plugin_newrelic_browser` to your site's cartridge path (Administration -> Sites -> Manage Sites -> <Your_site> -> Settings)
3. Once deployed, you can use New Relic Browser as usual, your application will appear like any other.

### Notes
- Make sure your site is receiving browser traffic before checking for data.
- `uBlock Origin` or similar filters can break the page load once the Browser JS snippet has been added.

## Support
New Relic has open-sourced this project. This project is provided AS-IS WITHOUT WARRANTY OR DEDICATED SUPPORT. Issues and contributions should be reported to the project here on GitHub. We encourage you to bring your experiences and questions to the [Explorers Hub](https://discuss.newrelic.com) where our community members collaborate on solutions and new ideas.

## Contributing

We encourage your contributions to improve Salesforce Commerce Cloud for New Relic Browser! Keep in mind when you submit your pull request, you'll need to sign the CLA via the click-through using CLA-Assistant. You only have to sign the CLA one time per project.

If you have any questions, or to execute our corporate CLA, required if your contribution is on behalf of a company, please drop us an email at opensource@newrelic.com.

## License

Salesforce Commerce Cloud for New Relic Browser is licensed under the [Apache 2.0](http://apache.org/licenses/LICENSE-2.0.txt) License.

Salesforce Commerce Cloud for New Relic Browser also uses source code from third-party libraries. You can find full details on which libraries are used and the terms under which they are licensed in the [third-party notices](./THIRD_PARTY_NOTICES.md) document.