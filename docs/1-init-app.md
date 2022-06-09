# App setup

# Pre-requisites
If not already done, you should follow the below links to have your environment set up before starting the codelab:

- [How to Get Access to App Builder](https://developer.adobe.com/app-builder/docs/overview/getting_access/)
 - [Setting up Your Environment
Creating](https://developer.adobe.com/app-builder/docs/getting_started)
- [Set up your First App Builder App](https://developer.adobe.com/app-builder/docs/getting_started/first_app/)
  

## TL;DR
1. Install [nodeJS](https://nodejs.org/en/blog/release/v14.17.0/) (use the lates LTS version)
2. Install Adobe aio CLi `npm install -g @adobe/aio-cli`
3. Install Docker Desktop (required for local development setup)
4. Create new project and development workspace from [Adobe Developer Console](https://developer.adobe.com/console)


# Init project
- [Aio app plugin](https://github.com/adobe/aio-cli-plugin-app)
  
1. Log in to the aio cli `aio login`
2. Run `aio app init type-script-actions --no-extensions` and select your organization, project and workspace
   1. Features to select: `Adobe Actions`
   2. Type of actions to generate: `Generic`
   3. UI:  react spectrum
   4. Action names: helloworld-ts, publish-events