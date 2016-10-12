# Existing Flask App
Part of what makes nanobox so useful is you don't have to have python or flask installed on your local machine.

This guide will help you get an existing Flask app up-and-running with nanobox.

## Build a Ruby Dev Environment
Nanobox will create an isolated virtual environment and mount your local codebase inside of. From within this environment you can run the app, a flask console, or even rake tasks as you would normally.

#### Add a boxfile.yml
The boxfile.yml tells nanobox how to build and configure these environments. Create a `boxfile.yml` at the root of your project that contains the following:

```yaml
# tell nanobox to build a python runtime
code.build:
  engine: python
```

#### Build the Environment

```bash
# build a python runtime
nanobox build

# deploy the python runtime into the dev environment
nanobox dev deploy

# add a convenient way to access your app from a browser
nanobox dev dns add flask.nanobox.dev
```

## Configure your Flask App
We need to allow connections from the host into the app's container. To do this we need modify the app to tell flask to listen on all available IP's at port 8080:

```python
app.run(host='0.0.0.0', port=8080)
```

## Flask up-and-running
With the app configured the last thing to do is run it:

```bash
# run the app from the nanobox dev console
python hello.py
```

Visit the app from your favorite browser at: `flask.nanobox.dev:8080`

## Now what?
With an app running in a dev environment with nanobox, whats next? Think about what else your app might need and hopefully the topics below will help you get started with the next steps of your development!

* [Connect a database](connect-a-database.html)
* [Javascript Runtime](javascript-runtime.html)
* [Local Environment Variables](local-evars.html)
* [Back to flask overview](flask.html)