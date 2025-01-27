## How to deploy the Upstash Rate Limit template through Azion

The Upstash Rate Limiting template helps you to implement rate limiting in a serverless environment, without requiring extensive manual setup. This template includes configurations for limiting requests and window limit.

It works in conjunction with Azion Edge Functions, being possible to adjust the initial setup based on the args. Additionally, this template creates a new GitHub repository that allows a continuous deployment workflow. This way, you're able to further configure and customize further the setup to attend to your needs, obtaining easy management and delivery of your personalized content.

## Requirements

To start using this template, you need to: 

1. Create an Upstash account.
2. Create a Global Database for the best available edge latency in the Upstash Console.
3. Generate your GitHub personal token.

While generating your GitHub personal token, grant that your scope has the permissions to authorize an OAuth app or a personal token to access to public and private repositories, including read and write access to code.You must also enable the workflow option to allow adding and updating GitHub Actions workflow files. Note that permissions can be scoped either to a user or an organization or to a repository. Read the Creating a personal access token documentation for more information.

—

## Getting the template

To start using the **Upstash Rate Limit** template, proceed as follows:

1. Access [Real-Time Manager (RTM)](https://manager.azion.com/).
- If you don’t have an account yet, create a new one [by visiting the sign-up page](https://manager.azion.com/signup/).
2. On the homepage, select the **Start with a template** option.
3. Find the **Upstash Rate Limit** card and select it.
4. Click the **Settings** tab to open the configuration section. 

—

## Setting up the template

In the configuration form, you must provide the information to configure your Azion application. Fill in the presented fields. 

Fields identified with an asterisk are mandatory.

- **Application Name** *: the name of your edge application. It's used to identify and manage your application within Azion's platform.
    - Use a unique and easy-to-remember name. If the name has already been used, the platform returns an error message.
- **Upstash Redis Rest URL** *: the URL to access your Upstash database using REST.
    - Go to your Upstash Console and copy the UPSTASH_REDIS_REST_URL in your database page.
- **Upstash Redis Rest Token** *: the token to authorize access to your Upstash database using REST. 
    - Go to your Upstash Console and copy the UPSTASH_REDIS_REST_TOKEN in your database page.
- **Limit Request**: the maximum number of requests. Example: 6.
- **Window Limit**: the time window for new requests. Example: 10 s ("ms" | "s" | "m" | "h" | "d").
- **GitHub Personal Token** *: your GitHub Personal Token.

After completing all the information, click the **Next** button, located in the bottom-right corner. This will start the deployment process.
Deploying the template

During the deployment, you'll be able to follow the process through a window showing off the logs. When it's complete, the *deployment* page appears, confirming the edge application for your project has been successfully created.

This page shows you the following sections:

   - **Access your Edge Application** section includes the link to visit and explore your edge application.
   - **Build Summary** contains the application's name and function.
   - The **Deployment details** tab can be opened to access the logs related to the deployment. 
   - **What do you want to do next?** provides recommendations regarding advanced options to enhance your edge application: **Customize Domain**, **Manage Edge Application**, **View Edge Application Metrics**, **View Edge Application Logs**, and the **Back to Home** button.

The link to the edge application allows you to see how it looks on the browser. However, ​​it takes a certain time to propagate and configure the application in Azion’s edge locations. It may be necessary to wait a few minutes for the URL to be activated and for the application page to be effectively displayed in the browser.

## Key configurations

The Upstash Rate Limiting template creates a new Azion edge application and its domain. It also creates an edge function to provide the arguments for the rate limiting, and a new repository in your GitHub account based on a [public template](https://github.com/aziontech/).

In this function, the upstash/redis and upstash/ratelimit libraries are integrated, connecting to your Upstash Global Database and checking in the /login route if it's within the configured Window and Limit. The key for limits is metadata ["remote_addr"].

Additionally, to guarantee the optimal performance of this template, it's necessary to activate the following Azion product:

To guarantee the optimal performance of this template, the following Azion products must be activated in your account:

[Edge Functions](https://www.azion.com/en/documentation/products/edge-application/edge-functions/)


You must activate this product separately via RTM. To do so:

1. [Access RTM](https://manager.azion.com/).
2. On the upper-left corner, select the three horizontal lines to open the **Products menu**.
3. In the **BUILD** section, select **Edge Application**.
4. You'll be redirected to the **Edge Application** page.
- It lists all the edge applications you've created. 
5. Find the edge application related to your template and select it. 
6. In the **Main Settings** tab, find the **Edge Application Modules** section and active the switch for the product you want to enable.

If this product is activated, the execution of this template could generate usage-related costs. Check the [pricing page](https://www.azion.com/en/pricing/) for more information.

## Managing your project

Considering the initial setup may not be optimal for your specific web application, all settings can be customized any time you need using Azion Real-Time Manager (RTM). Once the template is deployed, you also have full control over customizing your Upstash account and database.

To manage and edit your edge application's settings on Azion, follow these steps:

## Access RTM.

On the upper-left corner, select the three horizontal lines to open the **Products menu**.
In the **BUILD** section, select **Edge Application**.
You'll be redirected to the **Edge Application** page.
It lists all the edge applications you've created. 
Find the edge application relate to the Qstash Scheduler template and select it. 
  The list is organized alphabetically. You can also use the **search bar** located in the upper-left corner of the list; currently, it filters only by **Application Name**.

After selecting the edge application you’ll work on, you’ll be directed to a page containing all the settings you can configure.

Read the documentation about managing edge applications for more details. For specific Upstash or QStash-related questions, check the Upstash documentation.

## Continuous deployment

Once the template is deployed, you can edit and update your args and code, as well as implement a continuous deployment workflow. However, you'll need first to *declare secrets on your project's GitHub repository* to complete the second build with the changes. When the second build is completed, you'll be able to manage your project with a continuous deployment workflow and edit the args as desired.

To do so, open your repository in GitHub. Then, go to **Settings** > **Secrets and variables** > **Action** to [add your variables](https://docs.github.com/en/actions/security-guides/encrypted-secrets), following these instructions:

1. Add the Azion Personal Token to the *secrets*:
- Read [how to generate an Azion Personal Token](/en/documentation/products/accounts/personal-tokens/) in the documentation.

```bash
    AZION_PERSONAL_TOKEN=<value>
```

Environments for use in the action workflow:

```yml
  - name: edge-...
    id: azion_edge
    ...
    with:
        ....
        azionPersonalToken: ${{ secrets.AZION_PERSONAL_TOKEN }}
        ....

```

2. Add the Redis Database access credentials to the *secrets*, being:

- **UPSTASH_REDIS_REST_URL**: the URL to access your Upstash database using REST.
- Go to your Upstash Console and copy the UPSTASH_REDIS_REST_URL in your database page.
- **UPSTASH_REDIS_REST_TOKEN**: the token to authorize access to your Upstash database using REST.
- Go to your Upstash Console and copy the UPSTASH_REDIS_REST_TOKEN in your database page.
- *UPSTASH_LIMIT*: the maximum number of requests. Example: 6.
- *UPSTASH_LIMIT_WINDOW*: the time window for new requests. Example: 10 s. ("ms" | "s" | "m" | "h" | "d").


```bash
    UPSTASH_REDIS_REST_URL=<value>
    UPSTASH_REDIS_REST_TOKEN=<value>
    UPSTASH_LIMIT=6
    UPSTASH_LIMIT_WINDOW=10 s // "ms" | "s" | "m" | "h" | "d";
```

Environments for use in the action workflow:

```yml
 - name: Create args file
    run: |
        ...
        "UPSTASH_REDIS_REST_URL": "${{ secrets.UPSTASH_REDIS_REST_URL }}",
        "UPSTASH_REDIS_REST_TOKEN": "${{ secrets.UPSTASH_REDIS_REST_TOKEN }}",
        "UPSTASH_LIMIT": "${{ secrets.UPSTASH_LIMIT }}",
        "UPSTASH_LIMIT_WINDOW": "${{ secrets.UPSTASH_LIMIT_WINDOW }}"
        ...
```

3. Open a pull request to merge the changes to the main branch and start the automatic deployment.

Now your project is ready to work with a continuous deployment workflow, updating instantly any changes in the application or the repository. 

### Adding a custom domain

The edge application created during the deployment has an assigned Azion domain to make it accessible through the browser. The domain has the following format: `xxxxxxxxxx.map.azionedge.net`. However, you can add a custom domain for users to access your edge application through it.
