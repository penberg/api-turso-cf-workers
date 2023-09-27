# Turso-Cloudflare Workers REST API

This is a distributed REST API built using [Cloudflare workers] and [Turso] with [Drizzle] used as the ORM.

## Database Setup

[Install the Turso CLI].

Create a new turso database.

```sh
turso db create the-mugs-store-api
```

> **Note**
>
> We use `the-mugs-store-api` as the database name in this command, but you can give
> it any name.

To access the data stored inside your database, you need the Turso database url and an authentication token.

To obtain the database url, run the following command:

```sh
export TURSO_DB_URL=$(turso db show the-mugs-store-api --url)
```

And, to create an authentication token for your database, run:

```sh
export TURSO_DB_AUTH_TOKEN=$(turso db tokens create the-mugs-store-api)
```

## For local development

Add a `.env` file at the root of the project and inside it add the database url and authentication token for your Turso database obtained in the previous step, these variables will be used to assist in database migration with Drizzle.

```
echo "TURSO_DB_URL = $TURSO_DB_URL" > .env
echo "TURSO_DB_AUTH_TOKEN = $TURSO_DB_AUTH_TOKEN" >> .env
```

Also make the configuration visible to Wrangler:

```
cp .env .dev.vars
```

Then install all the dependencies with:

```
npm i
```

## Generate database schema, run migrations, and seed data

To generate the schema for the API database, run:

```
npm run generate
```

The command will create a new `migrations` directory under the `drizzle` directory.

Next, run the following command to apply the migrations on the created Turso database:

```
npm run migrate
```

And lastly, seed the database with some data by running:

```
npm run seed
```

and run the following command to start the development server:

```
npm run start
```

## For the production environment

Configure the Cloudflare project by running the following commands and copy-pasting the URL and the authentication token when prompted for them:

```
wrangler secret put TURSO_DB_URL
wrangler secret put TURSO_DB_AUTH_TOKEN
```

## Deployment

If you don't have an account, then [create a Cloudflare account here]. After verifying your email address, run the following command on your project's workspace to authenticate it with Cloudflare workers:

```
npx wrangler login
```

Lastly, deploy your Cloudflare workers project by running:

```
npm run deploy
```

## More information

For more information, visit the following links:
- [Cloudflare workers Docs]
- [Turso Docs]
- [Drizzle Docs]

[Cloudflare workers Docs]: https://developers.cloudflare.com/workers/
[Cloudflare workers]: https://developers.cloudflare.com/workers/
[Turso Docs]: https://docs.turso.tech/
[Drizzle Docs]: https://orm.drizzle.team/
[Install the Turso CLI]: https://docs.turso.tech/reference/turso-cli#installation
[Turso]: https://turso.tech/
[Drizzle]: https://github.com/drizzle-team/drizzle-orm
[create a cloudflare account here]: https://dash.cloudflare.com/sign-up
