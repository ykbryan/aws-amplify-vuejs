# Getting started to build VueJS app and AWS Amplify

The raising trends and love for VueJS is no surprise for many developers. With over [160k stars on Github](https://github.com/vuejs/vue), many developers and companies, including big and small, have been adopting it since the very beginning. With the ease of developing a responsive and impressive frontend application using VueJS, it is no wonder that developers are looking for the _same_ development experience and turning their attentions to cloud services and libraries to automatically spin up and connect the cloud capabilities together.

![AWS Amplify](docs/amplify-introduction.png 'What is AWS Amplify')

AWS Amplify is [an open-source library](https://github.com/aws-amplify/amplify-js) that supports many modern javascript frameworks and native mobile platforms i.e. [iOS](https://github.com/aws-amplify/aws-sdk-ios) and [Android](https://github.com/aws-amplify/aws-sdk-android). The [Amplify CLI](https://github.com/aws-amplify/amplify-cli) also provides the developer the ability to create a whole set of serverless, feature-rich features such as Auth, API, Analytics, Storage and Hosting in the AWS environment in their own comfortable console terminal. Since it is open-source and community-driven, any developers who is interested in contributing to AWS Amplify development or its [communities](https://github.com/aws-amplify/community), can easily vote and create tickets in its respective github, and see each project's roadmap (e.g. [Amplify JS Roadmap & Projects](https://github.com/aws-amplify/amplify-js/projects)) as well.

## Project setup

In this project, we will setup a brand new VueJS app, [your own AWS account](https://portal.aws.amazon.com/billing/signup?redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start), and add Vue CLI and AWS Amplify CLI via your favourite terminal. If you are new to VueJS or AWS, it is ok to take a step back to understand the concept and art of building modern apps with cloud services. I will add notes and explanations to each step for your understanding. You can also refer to [this Github](https://github.com/ykbryan/aws-amplify-vuejs) as we go along.

### NodeJS version

To make sure that your terminal is compatible with the latest [AWS Amplify CLI](https://docs.amplify.aws/cli/start/install) (minimum 10.0 and above) and [Vue CLI](https://cli.vuejs.org/guide/installation.html) (minimum 8.9 and above, 8.11.0+ recommended), you need to be running with at least node v10 and above in your terminal. Enter the following command to make sure that you are runnign the latest node version:

```
node -v
```

If you realise that you are not using the latest node/npm, you can use the [Node Version Manager (NVM)](http://nvm.sh) to install and select the node version you need. After you have install [nvm](http://nvm.sh), you can enter the following command to install and use node version 13.

```
nvm install 13 && nvm use 13
```

### Install @vue/cli

This is optional for you to actually start development with VueJS but in this project, I am going to use the @vue/cli to quickly create vue project with additional features such as Babel or TypeScript transpilation, ESLint integration and end-to-end testing.

```
yarn global add @vue/cli
# OR
npm install -g @vue/cli
```

### Install @aws-amplify/cli

The Amplify Command Line Interface (CLI) is a unified toolchain to create AWS cloud services for your app. Let’s go ahead and install the Amplify CLI.

```
yarn global add @aws-amplify/cli
# OR
npm install -g @aws-amplify/cli
```

## A new Vue app

Let's start with a new Vue app by running the following command:

```
vue create aws-amplify-vuejs
```

I am also going to select the **default preset** given by the @vue/cli and add babel and eslint to the vue project.

![VueJS default preset](docs/vuejs-default-preset.png 'VueJS default preset')

Once you have let the cli to finish its job, you should be able to go inside the project folder to begin the next step.

```
cd aws-amplify-vuejs
```

You can use your favourite IDE to open up the project and take a look at the new project. In this example, i am going to use VSCode for development.

![VueJS New App](docs/vuejs-new-app.png 'VueJS New App')

Now you can start your VueJS development and see your changes in your local browser

```
yarn serve
```

### It is Amplify time

Within the new VueJS app, I am going to configure my cloud services using Amplify CLI by entering the following command:

```
amplify init
```

You can now step-through and key in the respective values for your project name to be seen in the AWS console and environment you are in. In additional, if you do not have an AWS profile in your terminal, you will be also entering the AWS credentials for your AWS profile in your terminal.

![amplify init](docs/aws-amplify-init.png 'amplify init')

After the amplify configuration, you should be able to see the new folder named `amplify` and there is a new `aws-export.js` in your VueJS app. These are auto-generated by AWS Amplify CLI and it will add new identifiers and credentials needed for every new component you added via the CLI.

![New files and folders generated by AWS Amplify CLI](docs/amplify-new-files-folder.png 'New files and folders generated by AWS Amplify CLI')

### Adding AWS Amplify to your VueJS app

Once you all the files and AWS environment setup, you now need to add aws amplify and its UI components to your VueJS app.

```
yarn add aws-amplify @aws-amplify/ui-vue
# OR
npm install -S aws-amplify @aws-amplify/ui-vue
```

After that, you can add the following javascript codes to your `main.js` to initialise the AWS Amplify libraries.

```
import '@aws-amplify/ui-vue';
import Amplify from 'aws-amplify';
import awsconfig from './aws-exports';

Amplify.configure(awsconfig);
```

![Add AWS Amplify to VueJS](docs/vuejs-amplify-main.png 'Add AWS Amplify to VueJS')

## Add Auth to your VueJS app

Now that you have configured and ready to add features to your new VueJS app, we are going to add Auth to your app. Let's go back to the terminal and run this command in your project folder to add `auth` via AWS Amplify CLI.

```
amplify add auth
```

![amplify add auth](docs/amplify-add-auth.png 'Add Auth to your Amplify project')

In this example, we are probably not going to configure and complicate the whole process. You can easily re-configure this in the future with the following command.

```
amplify update auth
```

After you have added `auth` to your amplify, you can now see if what kind of resources will be added in your AWS environment by entering the following command:

```
amplify status
```

![amplify status](docs/amplify-status.png 'Amplify status to see the resources')

After you have confirmed the resources to be added to your AWS environment, you can now enter the following command to push your changes to the AWS cloud.

```
amplify push
```

This should take some time as in your AWS environment, new `auth` resources will be added with best practices such as new IAM roles with minimum permissions required and all of these event changes and resources can be seen in your AWS CloudFormation. Back to the VueJS app,
you can now open up your App.vue to edit the codes and include the auth features you need.

![VueJS New App.vue](docs/vuejs-new-appvue.png 'VueJS App.vue')

Firstly, let's refer to the [aws amplify documentations](https://docs.amplify.aws/ui/auth/authenticator/q/framework/vue#usage) and take a look at what is needed to be added.

```
<template>
  <amplify-authenticator>
    <div>
      My App
      <amplify-sign-out></amplify-sign-out>
    </div>
  </amplify-authenticator>
</template>
```

In this code example, you can see that my app is wrapped around `<amplify-authenticator>` and I also can add a dedicated sign out button with `<amplify-sign-out>`. If you copy-paste the codes given in the example, your app will look like this.

![auth code for VueJS](docs/aws-amplify-auth-code.png 'auth code for VueJS')

Instead, I am going to use the VueJS's HelloWorld component as my main screen and add the amplify `auth` component around it.

![auth code for VueJS](docs/vuejs-amplify-auth.png 'auth code for VueJS')

Next, I want to customise a little bit to the default Amplify Auth screen by adding extra HTML header texts and also, I do not want the mega-large sign out button so I attached a new `id` to the component to better style it.

![Custom attributes for Amplify Auth](docs/amplify-auth-custom-attributes.png 'Custom attributes for Amplify Auth')

Now that we have added the `auth` features, given some customisations and styles, I can now test the app via http://localhost:8080/. If you previously close/cancel the process in your terminal, enter the following command again to start.

```
yarn serve
```

![Amplify Auth Screen](docs/amplify-auth-screen.png 'Amplify Auth Screen')

Now, you can go ahead and create a new account. Have you noticed that you literally did not code any of these auth functionalities and all we did is to add the respective auth components from the Amplify UI libraries?

After you have successfully logged in, you should be able to see your main component with a sign out button below it.

![Amplify Logged In](docs/amplify-logged-in.png 'User Logged In')

Your final javascript code should look like this:

```
<template>
  <div id="app">
    <amplify-authenticator>
      <amplify-sign-in header-text="My Custom Sign In Text" slot="sign-in"></amplify-sign-in>
      <div>
        <img alt="Vue logo" src="./assets/logo.png" />
        <HelloWorld msg="Welcome to Your Vue.js App" />
        <div id="amplify-signout">
          <amplify-sign-out></amplify-sign-out>
        </div>
      </div>
    </amplify-authenticator>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#amplify-signout {
  width: 100px;
  margin: 0 auto;
}
</style>
```

## Add Hosting to your Vue App

After you have built the beautiful UX app, you want to host it. AWS Amplify Console got you covered and fortunately, you can add that via the following command and choose git-based deployment under `Hosting with Amplify Console`.

```
amplify add hosting
```

![amplify add hosting](docs/amplify-hosting.png 'AWS Amplify and Hosting')

Your browser should now open and lead you to the AWS Amplify Console. Firstly, you can link the app to your code repository and in this case, I am using my personal Github account to version all codes.

![Amplify Console Step 1](docs/console-connect-github.png 'AWS Amplify and Console Hosting')

Under step 2, you now need to select the repository and its `branch` for Amplify Console to know what and which branch to deploy to.

![Amplify Console Step 2](docs/console-step-two.png 'Amplify Console, select repo and branch')

Lastly, under step 3, you can review your configuration one more time before `Save and Deploy`.

![Amplify Console Step 3](docs/console-step-three.png 'Amplify Console, Save & Deploy')

You should now see your changes being deployed via the AWS Amplify Console and note that every changes you push to your repository under that selected branch, the Amplify Console also automatically deploy your changes to your portal.

![Amplify Console Deployment](docs/amplify-console-deployment.png 'Amplify Console Deployment')

Going back to your terminal, you can proceed by pressing `ENTER` and you should be able to see your portal URL too.

![Amplify Console, Hosting URL](docs/aws-amplify-console-cli.png 'Amplify Console, Hosting URL')

I also went back to the Amplify Console to update my DNS and point vuejs.bryanchua.io to the portal.

![Amplify Console DNS](docs/amplify-custom-dns.png 'Amplify Console DNS')

## What's next

In this project, I have only covered the basic functionalities of both VueJS and AWS Amplify, and showed how easy it is to add server-side functionalities within your frontend codes and beautify them. The beauty of using these advanced libraries is that there is literally no/less codes to write. You can now focus more time on user experience (UX) and delivering values via your app.
