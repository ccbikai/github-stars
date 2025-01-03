---
project: gitignore.io
stars: 8339
description: Create useful .gitignore files for your project
url: https://github.com/toptal/gitignore.io
---

  
**Create useful .gitignore files for your project**

About
-----

.gitignore.io is a web service designed to help you create .gitignore files for your Git repositories. The site has a graphical and command line method of creating a .gitignore for your operating system, programming language, or IDE.

`.gitignore` Template Source
----------------------------

Source templates for gitignore.io: https://github.com/toptal/gitignore

License of the generated files
------------------------------

All files generated by https://www.toptal.com/developers/gitignore are under CC0.

Documentation
-------------

Complete gitignore.io documentation: https://docs.gitignore.io/

Docker Container
----------------

### Prerequisites

-   Docker

### Build

#### Production

```
docker-compose up --build
```

#### Development

```
docker-compose -f ./docker-compose-dev.yml build
```

```
docker-compose -f ./docker-compose-dev.yml up
```

It will start the web server running on http://localhost:8080

Development mode mounts the following directories to docker volumes:

-   `/Public`
-   `/Resources`

LESS and CSS
------------

The app uses LESS as its CSS preprocessor for the files in `Public/css`.

To process the less file you need to:

-   Install all dependencies with `yarn install`
-   Process the assets with `yarn build`

Environment Variables
---------------------

Please set your environment variables to docker configurations. All are optional.

...
services:
  app:
    ...
    environment:
      HOST\_ORIGIN: http://www.example.com
      BASE\_PREFIX: /foo/bar
      GOOGLE\_ANALYTICS\_UID:
    ...
...

### HOST\_ORIGIN

Origin of your web server, falls back to https://www.toptal.com

```
HOST_ORIGIN: http://www.example.com
```

### BASE\_PREFIX

If you want to host this web server under a subdirectory (http://www.example.com/foo/bar for example), please set this variable.

```
BASE_PREFIX: /foo/bar
```

### GOOGLE\_ANALYTICS\_UID

User ID for Google Tag Manager snippet

```
GOOGLE_ANALYTICS_UID: UA-XXXXXXXX-X
```

E2E Tests
---------

Tests are located in `e2e-tests` folder with:

-   API tests in `api` folder - implemented using Superagent
-   E2E tests in `pages` folder - implemented with Puppeteer

Prerequisites:

-   Node.js 12.9 or above.
-   Yarn 1.15.2 or 1.17.3

Running:

-   Set the BASE\_URL env variable (only if you have changed the default URL or port)
-   docker-compose up --build --detach
-   yarn gitupdate
-   yarn install
-   yarn build
-   yarn test
-   docker-compose stop
