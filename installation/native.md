# Native

For running directly on your machine, please follow this guide.

Lynx has 3 parts:

* The backend - Node.JS
* The frontend - Vue + Vite, but builds to static HTML.
  * The backend will serve these files for you is the environment NODE\_ENV is set to `production`.Lynx should now be accessible at [localhost:3000](http://localhost:3000)
* The database - MongoDB

## MongoDB

Set up a Database for MongoDB to use, here are some guides for each platform by Mongo:

* [Windows](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-windows/)
* [Linux](https://www.mongodb.com/docs/manual/administration/install-on-linux/)
* [macOS](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/)

Make sure it is protected with a username and password.

Your database does not need to be openly accessible (only from the backend), for best security practices make sure it is only accessible locally on your server.



## Lynx

You need [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git), [node ](https://nodejs.org/en/download)and [yarn ](https://yarnpkg.com/getting-started/install#nodejs-1610-1)(via NPM) to build and run Lynx.

Clone Lynx:

```bash
git clone https://github.com/Lynx-Shortener/Lynx
```

Enter the Lynx directory:

```bash
cd Lynx
```

Rename `.example.env` to `.env` and set the [environment variables ](environment-variables.md)to match your setup and requirements.

### Build the frontend

Change to its directory, and then the frontend:

```bash
cd Lynx/frontend
```

Install the required dependencies:

```bash
yarn
```

Build the frontend: (It will create a dist folder in ./Lynx)

```bash
yarn build
```

Then go back to the main Lynx directory

```bash
cd ..
```

### Run the backend

Install the required dependencies:

```bash
yarn
```

Run the backend

```bash
node .
```

Lynx should now be accessible at [localhost:3000](http://localhost:3000)

Now go to Post Installation&#x20;

{% content-ref url="post-installation.md" %}
[post-installation.md](post-installation.md)
{% endcontent-ref %}

###



