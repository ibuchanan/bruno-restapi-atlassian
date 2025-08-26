# Bruno Collections for Atlassian Cloud APIs

## Getting started

1. Install [Bruno](https://www.usebruno.com/)
2. Clone this repo
3. Import each subdirectory as a [Collection](https://docs.usebruno.com/get-started/import-export-data/import-collections)
4. Configure an OAuth 2.0 client in the Atlassian developer console and in each `.env` file
5. Run `Accessible Resources` to run through the authorization flow
6. Explore!

## Atlassian Cloud APIs

* [Atlassian OAuth 2.0](https://developer.atlassian.com/cloud/oauth/)
* [Jira platform v3](https://developer.atlassian.com/cloud/jira/platform/rest/v3/intro/#version)
* [Jira Software](https://developer.atlassian.com/cloud/jira/software/rest)
(Jira Software's API covers Software-specific features of Jira
like Sprints, Epics, and developer tooling integrations.
It is built on the Jira platform,
which means consumers will usually need to interate with both APIs.)

## Bruno

[Bruno](https://www.usebruno.com/)
is a Git-friendly and offline-first open-source API client
aimed at revolutionizing the status quo
represented by tools like Postman and Insomnia.
With powerful import capabilities,
it is trivial to import Atlassian REST APIs,
by simply pointing to the appropriate OpenAPI V3 URL.
However, once imported,
those API specs still require a bit of configuration.
This repo solves the following:
* All the APIs in 1 quick Git clone.
(TODO: currently only Jira platform & Jira Software; import the rest)
* APIs have been configured to use OAuth 2.0.
(Unfortunately, that doesn't mean every path works with OAuth tokens.
Substitution for basic auth may be required.)

## [Enabling OAuth 2.0](https://developer.atlassian.com/cloud/oauth/getting-started/enabling-oauth-3lo/)

Before you can implement OAuth 2.0 for Bruno,
you need to enable OAuth in
[the developer console](https://developer.atlassian.com/console/myapps/).
Because of Atlassian's recommendation to limit clients to 50 scopes,
create 1 client (called an App in the console)
for each Bruno collection:
1. OAuth (This is required, others are optional)
2. Jira Platform
3. Jira Software

For each collection,
copy the `.env.example` to `.env`,
where you will need to provide specific values provided in the steps below:

1. From any page on developer.atlassian.com,
select your profile icon in the top-right corner,
and from the dropdown,
select **Developer console**.
You should be welcomed to the console with a subtitle that reads,
"Create and manage your Forge apps, Cloud Fortified Connect apps, and OAuth 2.0 integrations."
2. Click the **Create** and the **OAuth 2.0 integration** option.
You should be taken to a dedicated page for,
"Create a new OAuth 2.0 (3LO) integration".
3. Provide a human-readable app name for this OAuth client.
When creating a client for each collection,
use Bruno and the collection in the name.
For example, "Bruno HTTP Client for OAuth Collection".
Check the box to agree to Atlassian's developer terms.
Click the **Create** button.
You should now see an overview of the new client with the name you provided
and a subtitle that reads,
"OAuth 2.0 integration".
The App ID provided here is only for Atlassian purposes;
it is _not_ the OAuth 2.0 Client ID.
4. Select Authorization in the left menu.
You should see a list of Authorization types.
5. Next to OAuth 2.0 (3LO),
select **Add**.
You will be taken to a configuration that reads,
"OAuth 2.0 authorization code grants (3LO) for apps",
asking for a Callback URL.
6. Enter the Callback URL.
In OAuth terms,
Bruno is known as a [public client](https://oauth.net/2/client-types/).
The common convention for public clients is to register the Callback URL as `http://localhost`.
If you use a different URL,
make sure to update the `.env` file to match.
Click **Save changes**.
A message should appear that explains,
"Your app doesn't have any APIs."
7. Click the hyperlink for **Add APIs**
(or the Permissons menu item on the left,
which navigates to the same place as the URL).
You should see a "Permissions" page
with a list of APIs
and 0 scopes used.
8. Click **Add* for the API corresponding to each Bruno collection.
For example, start with the "User identity API".
When the Add button becomes **Configure**,
click it.
You should see a list of Scopes.
9. Click **Edit scopes**.
You should see a modal for editing the selected scopes.
10. Select all the scopes
and click **Save**.
You should see confirmation that the scopes have changed.
Scopes should now be checked
and the count of scopes should be more than zero.
Check these scopes match what is provided by default
in the `.env` file.
11. Select the **Settings** menu item on the left.
You should see the "General settings" for your client.
12. Copy Client ID & Secret to the `.env` file.
13. Set the target site name in the `.env` file.
For example, if your site's URL is `https://one-atlas-example.atlassian.net/`
then use `one-atlas-example` in the `.env` file.
14. Repeat for each Bruno collection.
