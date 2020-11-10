# heroku-lesson
Host your own website for free with heroku!

## Creating your Heroku Account
[Sign up](https://signup.heroku.com/login) for Heroku. Be sure to __verify your email__.

Once you have an account, [Login and go to your Dashboard](https://dashboard.heroku.com/apps).

## Install the Heroku CLI
Go [here](https://devcenter.heroku.com/articles/heroku-cli) to install the Heroku CLI!

If you are on linux, you can just run:
```sh
curl https://cli-assets.heroku.com/install.sh | sh
```

## Login to Heroku CLI
In your terminal, run the following.
```
heroku login
```
Press any key and it will open up your browser. Press the Log In button to link to your terminal.

## Create your new App
Go to your [dashboard](https://dashboard.heroku.com/apps) and click `Create New App`

*(if you don't see this, look in top right for `New` and the dropdown will have `Create New App`)*

## Lets do some coding

We'll be using [Express](https://expressjs.com/) and [Node.js](https://nodejs.org/en/). If you don't know what this is, we did a lesson on it a few weeks back. You can find the tutorial [here](https://github.com/hacksu/express-tutorial), and it has all the install instructions and in-depth explanations of Express and Node.js


Lets start by making a new folder.
```
mkdir my-heroku-app
cd my-heroku-app
```

Initialize our Project
```
# Create Git Repo
git init

# .gitignore
echo 'node_modules' > .gitignore

# Create empty project
npm init -y

# Install express
npm install --save express

# Create a root file for our project
echo > index.js
```

(Here is all of that but in a single command so you can copy paste)
```
git init && echo 'node_modules' > .gitignore && npm init -y && npm install --save express && echo > index.js
```

Next, we need to open `package.json` which should be inside our new folder.


We want to add `"start": "node index.js",` inside of `scripts`:
```js
{
  /* ... other stuff .. */
  "scripts": {
    "start": "node index.js", // Add this line WITH A TRAILING COMMA
    "test": "node tests"
  },
  /* ... other stuff ... */
}
```

Alright, we got everything we need. Lets make a simple express app.

index.js
```js
let express = require('express');
let app = express();

app.get('/', (req, res) => res.send('Hello there!'))

let port = process.env.PORT || 8080; // Heroku will supply a port number for us through environment variables.
app.listen(port, () => console.log(`Listening on port ${port}`));

```

## Test our Express app locally
`npm run start`

If we visit https://localhost:8080 it should say `Hello there!`

If that works, lets commit our changes.
```
git add . && git commit -m "First Commit"
```

## Deploying to Heroku

Add Heroku's remote
```
# replace "hacksu-seitz-fall2020" with whatever you named your app on your heroku daskboard.
heroku git:remote -a hacksu-seitz-fall2020
```

Deploying
```
git push heroku master
```

That will do a lot of output, and once it finishes you can go visit your app!

There is an `Open App` button on the top right of your management page for your app. Just go to your [dashboard](https://dashboard.heroku.com/apps) and click your app, then click `Open App` in the top right.

`https://{PROJECT NAME}.herokuapp.com/`

## Alright, what about a custom domain name?
The details on how to add a custom domain name to heroku are [here](https://devcenter.heroku.com/articles/custom-domains)



First, you need to have a domain name. I'd recommend buying one from [Namecheap](https://namecheap.com)


**AS A STUDENT, YOU ALSO GAIN ACCESS TO THE GITHUB STUDENT DEVELOPER PACK**
https://education.github.com/pack?sort=popularity&tag=Domains

You can get a **FREE** 1 year .me domain from Namecheap through this.


## Verify our account

In order to add a custom domain, we must verify our heroku account. You need to add a credit card to your account on your [billing page](https://dashboard.heroku.com/account/billing). I've already done this step.

Adding your domain to heroku is free, they just want to verify you are a real person.

## Adding the domain

```
heroku domains:add mydomainname.com
```

It'll spit out a **DNS Target**, ending in `.herokudns.com`. Log in to your DNS provider and add a **CNAME Record** that points to the DNS Target Heroku provides you.

I'd recommend using CloudFlare for DNS, its pretty great.

However, we won't be covering domains and DNS in this lesson.

After doing this, you should be able to visit your heroku app via your own domain name!
