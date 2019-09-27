<!-- Heads up! This is a generated file, do not edit directly. You can find the source at https://github.com/ember-learn/super-rentals-tutorial/blob/master/src/chapters/01-orientation.md -->

You can install the latest version of _Ember CLI_ by running the following command. If you've already done this by following the [Quick Start](../../getting-started/quick-start/) guide, feel free to skip ahead!

```shell
$ npm install -g ember-cli
```

To verify that your installation was successful, run:

```shell
$ ember --version
ember-cli: 3.12.0
node: 12.8.1
os: darwin x64
```

If a version number is shown, you're ready to go.

We can create a new project using Ember CLI's `new` command. It follows the pattern `ember new <project-name>`. In our case, the project name would be `super-rentals`:

```shell
$ ember new super-rentals --yarn -b @ember/octane-app-blueprint
installing octane-app-blueprint
  create .editorconfig
  create .ember-cli.js
  create .eslintignore
  create .eslintrc.js
  create .template-lintrc.js
  create .travis.yml
  create .watchmanconfig
  create README.md
  create app/app.js
  create app/index.html
  create app/resolver.js
  create app/router.js
  create app/styles/app.css
  create app/templates/application.hbs
  create config/environment.js
  create config/optional-features.json
  create config/targets.js
  create ember-cli-build.js
  create .gitignore
  create jsconfig.json
  create package.json
  create public/robots.txt
  create testem.js
  create tests/index.html
  create tests/test-helper.js
Yarn: Installed dependencies
Successfully initialized git.
```

This should have created a new folder for us called `super-rentals`. We can navigate into it using the `cd` command.

```shell
$ cd super-rentals
```

Let's bring the pods!!!

```js { data-filename="config/environment.js" data-diff="+6" }
'use strict';

module.exports = function(environment) {
  let ENV = {
    modulePrefix: 'super-rentals',
    podModulePrefix: 'super-rentals/pods',
    environment,
    rootURL: '/',
    locationType: 'auto',
    EmberENV: {
      FEATURES: {
        // Here you can enable experimental features on an ember canary build
        // e.g. EMBER_MODULE_UNIFICATION: true
        EMBER_METAL_TRACKED_PROPERTIES: true
      },
      EXTEND_PROTOTYPES: {
        // Prevent Ember Data from overriding Date.parse.
        Date: false
      }
    },

    APP: {
      // Here you can pass flags/options to your application instance
      // when it is created
    }
  };

  if (environment === 'development') {
    // ENV.APP.LOG_RESOLVER = true;
    // ENV.APP.LOG_ACTIVE_GENERATION = true;
    // ENV.APP.LOG_TRANSITIONS = true;
    // ENV.APP.LOG_TRANSITIONS_INTERNAL = true;
    // ENV.APP.LOG_VIEW_LOOKUPS = true;
  }

  if (environment === 'test') {
    // Testem prefers this...
    ENV.locationType = 'none';

    // keep test console output quieter
    ENV.APP.LOG_ACTIVE_GENERATION = false;
    ENV.APP.LOG_VIEW_LOOKUPS = false;

    ENV.APP.rootElement = '#ember-testing';
    ENV.APP.autoboot = false;
  }

  if (environment === 'production') {
    // here you can enable a production-specific feature
  }

  return ENV;
};
```

```shell
$ mkdir -p app/pods/application

$ mv app/templates/application.hbs app/pods/application/template.hbs

$ yarn test
$ ember test
Environment: test
cleaning up...
Built project successfully. Stored in "/var/folders/_7/8wwzqn8j1wlc91y9kgm_mq580000gp/T/tests-dist-2019827-31400-1d5umqn.jy6ml".
ok 1 Chrome 77.0 - [3 ms] - ember-qunit: Ember.onerror validation: Ember.onerror is functioning properly

1..1
# tests 1
# pass  1
# skip  0
# fail  0

# ok

$ git add .ember-cli.js

$ git add config/environment.js

$ git add app/templates/application.hbs

$ git add app/pods/application/template.hbs

$ git commit -m "Use pods"
[master 8ef8169] Use pods
 2 files changed, 1 insertion(+)
 rename app/{templates/application.hbs => pods/application/template.hbs} (100%)
```

For the rest of the tutorial, all commands should be run within the `super-rentals` folder. This folder has the following structure:

```plain
super-rentals
├── app
│   ├── pods
│   │   └── application
│   │       └── template.hbs
│   ├── styles
│   │   └── app.css
│   ├── templates
│   ├── app.js
│   ├── index.html
│   ├── resolver.js
│   └── router.js
├── config
│   ├── environment.js
│   ├── optional-features.json
│   └── targets.js
├── public
│   └── robots.txt
├── tests
│   ├── index.html
│   └── test-helper.js
├── .editorconfig
├── .ember-cli.js
├── .eslintignore
├── .eslintrc.js
├── .gitignore
├── .template-lintrc.js
├── .travis.yml
├── .watchmanconfig
├── README.md
├── ember-cli-build.js
├── jsconfig.json
├── package.json
├── package-lock.json
└── testem.js

8 directories, 25 files
```

We will get to know the purposes of these files and folders as we go. For now, just know we will spend most of the time working within the `app` folder.

Ember CLI comes with a lot of different commands for a variety of development tasks, such as the `ember new` command that we saw earlier. It also comes with a _development server_, which we can launch with the `ember server` command:

```shell
$ ember server

Build successful (3663ms) – Serving on http://localhost:4200/
```

The development server is responsible for compiling our app and serving it to the browsers. It may take a while to boot up. Once it's up and running, open your favorite browser and head to <http://localhost:4200>. You should see the following welcome page:

![Welcome to Ember!](/screenshots/01-orientation/welcome@2x.png)

<div class="cta">
  <div class="cta-note">
    <div class="cta-note-body">
      <div class="cta-note-heading">Zoey says...</div>
      <div class="cta-note-message">
        <p>The <code>localhost</code> address in URL means that you can only access the development server from your local machine. If you would like to share your work to the world, you will have to <em>deploy</em> your app to the public Internet. Don't worry, we will cover that in Part 2 of the tutorial.</p>
      </div>
    </div>
    <img src="/images/mascots/zoey.png" role="presentation" alt="Ember Mascot">
  </div>
</div>

You can exit out of the development server at any time by typing `Ctrl + C` into the terminal window where `ember server` is running. That is, typing the "C" key on your keyboard _while_ holding down the "Ctrl" key at the same time. Once it has stopped, you can start it back up again with the same `ember server` command. We recommend having two terminal windows open: one to run the server in background, another to type other Ember CLI commands.

The development server has a feature called _live reload_, which monitors your app for file changes, automatically re-compiles everything, and refreshes any open browser pages. This comes in really handy during development, so let's give that a try!

As text on the welcome page pointed out, the source code for the page is located in `app/pods/application/template.hbs`. Let's try to edit that file and replace it with our own content:

```handlebars { data-filename="app/pods/application/template.hbs" data-diff="-1,-2,-3,-4,-5,-6,+7" }
{{!-- The following component displays Ember's default welcome message. --}}
<WelcomePage />
{{!-- Feel free to remove this! --}}

{{outlet}}

Hello World!!!
```

Soon after saving the file, your browser should automatically refresh and render our greetings to the world. Neat!

![Hello World!!!](/screenshots/01-orientation/hello-world@2x.png)

When you are done experimenting, go ahead and delete the `app/pods/application/template.hbs` file. We won't be needing this for a while, so let's start afresh. We can add it back later when we have a need for it.

Again, if you still have your browser tab open, your tab will automatically re-render a blank page as soon as you delete the file. This reflects the fact that we no longer have an application template in our app.

Create a `app/pods/index/template.hbs` file and paste the following markup.

```handlebars { data-filename="app/pods/index/template.hbs" }
<div class="jumbo">
  <div class="right tomster"></div>
  <h2>Welcome to Super Rentals!</h2>
  <p>We hope you find exactly what you're looking for in a place to stay.</p>
</div>
```

If you are thinking, "Hey, that looks like HTML!", then you would be right! In their simplest form, Ember templates are really just HTML. If you are already familiar with them, you should feel right at home here.

Of course, unlike HTML, Ember templates can do a lot more than just displaying static content. We will see that in action soon.

After saving the file, your browser tab should automatically refresh, showing us the welcome message we just worked on.

![Welcome to Super Rentals! (unstyled)](/screenshots/01-orientation/unstyled@2x.png)

Before we do anything else, let's add some styling to our app. We spend enough time staring at the computer screen as it is, we must protect our eyesight against unstyled markup!

Fortunately, our designer sent us some CSS for us to use, so we can just go ahead <a href="/downloads/style.css" download="app.css">download the stylesheet file</a> and copy it into `app/styles/app.css`. This file has all the styles we need for building the rest of the app.

```css { data-filename="app/styles/app.css" }
@import url(https://fonts.googleapis.com/css?family=Lato:300,300italic,400,700,700italic);

/**
 * Base Elements
 */

* {
  margin: 0;
  padding: 0;
}

body,
h1,
h2,
h3,
h4,
h5,
h6,
p,
div,
span,
a,
button {
  font-family: 'Lato', 'Open Sans', 'Helvetica Neue', 'Segoe UI', Helvetica, Arial, sans-serif;
  line-height: 1.5;
}

body {
  background: #f3f3f3;
}

/* ...snip... */
```

If you are familiar with CSS, feel free to customize them to your liking! Just keep in mind that you may see some visual differences going forward, if you choose to do so.

When you are ready, save the CSS file; our trusty development server should pick it up and refresh our page right away. No more unstyled content!

![Welcome to Super Rentals! (styled)](/screenshots/01-orientation/styled@2x.png)

To match mockup from our designer, we will also need to download the `teaching-tomster.png` image, which was referenced from our CSS file:

```css { data-filename=app/styles/app.css }
.tomster {
  background: url(../assets/images/teaching-tomster.png);
  /* ...snip... */
}
```

As we learned earlier, the Ember convention is to place your source code in the `app` folder. For other assets like images and fonts, the convention is to put them in the `public` folder. We will follow this convention by <a href="/downloads/teaching-tomster.png" download="teaching-tomster.png">downloading the image file</a> and saving it into `public/assets/images/teaching-tomster.png`.

Both Ember CLI and the development server understand these folder conventions and will automatically make these files available to the browser.

You can confirm this by navigating to
`http://localhost:4200/assets/images/teaching-tomster.png`. The image should also show up in the welcome page we have been working on. You may need to do a manual refresh for the browser to pick up the new file.

![Welcome to Super Rentals! (with Tomster)](/screenshots/01-orientation/styled-with-tomster@2x.png)
