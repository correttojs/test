
## Run this example

1. Create a new integration on the [integration console](https://vercel.com/dashboard/integrations/console)

2. Set the Redirect URL to `http://localhost:3000/callback`

3. Set the environment variables:

```
cp .env.local.example .env.local
```

Set the required environment variables values.

4. Install all dependencies

```
npm install
```

5. Start the app

```
npm run dev
```




## How this integration works

1. The user clicks "add" and selects the scope
2. The user sees the callback popup with your defined Redirect URL
3. The Redirect URL will be called with query parameters that we can use:
   - `code`: The authorization code to receive an `access_token` in order to interact with the API
   - `teamId`: The id of the team (only provided if the integration gets installed on a team)
   - `configurationId`: The id of the installation (you usually want to store this information)
   - `next`: The URL we're redirecting if the setup is done
4. Once the user sees the page `/setup` we exchange the provided `code` for an `access_token`. See the docs for [exchanging code for an access token](https://vercel.com/docs/integrations#using-the-vercel-api/getting-an-access-token/exchanging-the-code-for-an-access-token)
5. After the `code` was exchanged, we can use the `access_token` for our calls to the Vercel API. See the docs for [available endpoints](https://vercel.com/docs/api#endpoints). In this case we're querying the [Projects endpoint](https://vercel.com/docs/api#endpoints/projects/get-projects) to get a list of all projects for the user or the team
6. The user sees a list of projects. This would be the step to provide additional information and allow the user to link projects to your own resources.
7. The user clicks on "Redirect me back to Vercel" to close the popup and complete the installation on Vercel. In your real integration, this should be done automatically after you collected all information you need, to save the user some clicks.



**Important note:**

Please make sure, that you provide the `teamId` as a query parameter while interacting with the API. To determine if you have to add a `teamId` to API calls, see the response after exchanging the `code ` for an `access_token`. See the docs for [accessing resources owned by a team](https://vercel.com/docs/api#api-basics/authentication/accessing-resources-owned-by-a-team).