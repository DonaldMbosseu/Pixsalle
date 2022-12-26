# :book: Summary
This project was developped with PHP language, applying the SOLID principle.
Templates used was twig.
API testings done using postman.

In this project, Docker is used to create containers to help me develop my project
My project contains
* `docker-compose.yaml` file with a
    * php-fpm image
    * mysql-image
    * nginx image
    * adminer image
* `docker-entrypoint-initdb.d/schema.sql` so when you run `docker compose up` a database is created following such
  schema
* The PHP code to start my application with
    * `composer.json` file
    * `templates` folder
    * `src` folder
    * `config` folder
    * `public` folder
* `.env` file
* `cypress` folder

# :computer: How to create and destroy my services

I Use `docker compose up` to create the services. And use `docker compose down` to destroy them.

To run tests, you can run:

```
docker run --env CYPRESS_baseUrl=http://nginx:80 -v "${PWD}:/cypress" -w /cypress --network="pixsalle-template_default" -it --rm vcaballerosalle/cypress-mysql:1.0 /cypress --browser chrome --spec "cypress/integration/sign-in.spec.js"
```

# :notebook: Important notes:

* First, you have to specify the spec at the end of the command. `cypress/integration/sign-in.spec.js` is the spec run
  by the previous command. If you remove the `--spec` flag and the corresponding argument, cypress will run all specs
  found inside the `integration` folder.
* Second, the services specified by the `docker-compose.yaml` file must be running. If you read the command again, you
  will see the flag `--network`. The right hand of the equals sign is the name of the network `docker compose up`
  created for us, therefore, what we are doing is connecting the standalone cypress container to the network with all
  the services. Notice that the first part of the network name is the name of the folder where `docker-compose.yaml` is
  located, so if you change the name of the folder, you will need to change the name of the network you want to connect
  to.

Finally, if you run the command and you signal to cancel the execution (Ctrl+C), your `.env` file may be left in an
unstable state. You can find the original file in `cypress/tmp/env.prod`.
