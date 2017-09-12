# Moleculer from Scratch
Nanobox builds an isolated Node.js environment for you inside of a local, virtual development environment. Installing Moleculer and generating a new project is simple. Your current working directory is mounted into the virtual environment, so anything written or changed in the `/app` directory in the VM will propagate down to your local filesystem.

## Create a Moleculer project
Create the project folder and change into it:

```bash
mkdir nanobox-moleculer && cd $_
```

**HEADS UP**: All `nanobox` commands *must* be run from within your project folder.

#### Add a boxfile.yml
Nanobox uses the <a href="https://docs.nanobox.io/boxfile/" target="\_blank">boxfile.yml</a> to configure your app's environment.

At the root of your project create a `boxfile.yml` telling Nanobox you want to use the Nodejs <a href="https://docs.nanobox.io/engines/" target="\_blank">engine</a> and include a [Redis component](/redis):

```yaml
run.config:
  engine: nodejs

data.redis:
  image: nanobox/redis:3.2
```

## Start the Dev Environment
Add a convenient way to access your app from the browser, then start the dev environment.

```bash
# add a local dns for easy browser access
nanobox dns add local moleculer.dev

# start the dev environment and drop into a console
nanobox run
```

## Generate a Moleculer App

```bash
# install the moleculer cli so you can use it to generate your application
yarn add moleculer-cli

# cd into the /tmp dir to create an app
cd /tmp

# generate the moleculer app
moleculer init project-simple app

# Walk through the project generation checklist
# Don't load dependencies yet

# cd back into the /app dir
cd -

# enable the hidden files shell option
# copy the generated app into the project
shopt -s dotglob
cp -a /tmp/app/* .

# Install dependencies
yarn install
```

## Configure Moleculer

### Update the Redis Connection
Update the Redis connection information in `moleculer.config.js` to use environment variables automatically generated by Nanobox. You'll need to update the existing `cacher` config and add the `transporter` config.

```javascript
cacher: `redis://${process.env.DATA_REDIS_HOST}:6379`,
transporter: `redis://${process.env.DATA_REDIS_HOST}:6379`,
```

## Run the App

```bash
yarn run dev
```

Visit your app at <a href="http://moleculer.dev:3000/greeter/hello" target="\_blank">moleculer.dev:3000/greeter/hello</a>

## Explore
With Nanobox, you have everything you need develop and run your Moleculer app:

```bash
# drop into a Nanobox console
nanobox run

# where node is installed
node -v

# npm/yarn are installed
npm -v; yarn --version

# and your code is mounted
ls

# exit the console
exit
```

## Now what?
Whats next? Think about what else your app might need and hopefully the topics below will help you get started with the next steps of your development!

* [Add a Database](/nodejs/moleculer/add-a-database)
* [Frontend Javascript](/nodejs/moleculer/frontend-javascript)
* [Local Environment Variables](/nodejs/moleculer/local-evars)
* [Back to Moleculer Overview](/nodejs/moleculer)