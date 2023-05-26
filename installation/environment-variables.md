# Environment Variables

Default environment variables:

* [.env](https://github.com/Lynx-Shortener/Lynx/blob/main/.example.env)
* [docker-compose](https://github.com/Lynx-Shortener/Lynx/blob/main/docker-compose.yml)

## Database

| Variable     | Description                                                                                                            | Example   |
| ------------ | ---------------------------------------------------------------------------------------------------------------------- | --------- |
| DB\_HOST     | The address of your mongodb database.                                                                                  | 127.0.0.1 |
| DB\_PORT     | The port of your mongodb database. When using docker set this to `27017`.                                              | 27017     |
| DB\_USER     | Your mongodb database username.                                                                                        | admin     |
| DB\_PASSWORD | Your mongodb password. Generate a secure one using a tool like [1password](https://1password.com/password-generator/). |           |

## Security

| Variable   | Description                                                                                                                                                 | Example |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| JWT\_KEY   | The key used to verify and sign login-sessions. Use a site like [1password](https://1password.com/password-generator/) to generate a 32 character password. |         |
| USE\_HTTPS | If your Lynx installation will be at https://mydomain.com - this does not provide an SSL certificate, it only changes how cookies are handled.              | true    |
| CORS       | Your allowed CORS origin(s), `*` for any (default).                                                                                                         | \*      |

## Link Creation

| Variable          | Description                                                                                                                                            | Example  |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| URL\_LENGTH       | The length of your automatically generated slugs.                                                                                                      | 8        |
| URL\_SET          | The type of characters your automatically generated slug will use.                                                                                     | standard |
| URL\_ONLY\_UNIQUE | Wether each new url has to be unique, e.g. if a link already redirects to `https://example.com` new links created cannot link to the same destination. | false    |

## Umami

Lynx comes with full support for Umami, both standard tracking and events.

| Variable      | Description                           | Example                                                                      |
| ------------- | ------------------------------------- | ---------------------------------------------------------------------------- |
| UMAMI\_SITEID | Your umami site ID, blank to disable. | 224d86da-1209-4b8b-ad98-b24d300efa55                                         |
| UMAMI\_URL    | The URL to your umami instance.       | [https://analytics.umami.is/script.js](https://analytics.umami.is/script.js) |

## Backups

| Variable         | Description                                                                                        | Example       |
| ---------------- | -------------------------------------------------------------------------------------------------- | ------------- |
| BACKUP           | Wether to create backups or not. They will be in ./backups or /app/backups for Docker              | true          |
| BACKUP\_SCHEDULE | When to create backups. Use [crontab.guru](https://crontab.guru) to create                         | 0 \* \* \* \* |
| BACKUP\_COUNT    | How many backups to keep. 1 will make a backup file called backup.json, -1 will keep every backup. | 5             |

## Other

| Variable                  | Description                                                                                                                                               | Example                                  |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| NODE\_ENV                 | What node environment to use, use `production` for any production use and/or when using in docker.                                                        | production                               |
| FORCE\_FRONTEND\_REDIRECT | Use the frontend to redirect instead of express, useful for hiding embeds on discord for all your rickrolling needs                                       | false                                    |
| ENABLE\_REGISTRATION      | Whether or not to allow registration. If not accounts exist you will be allowed to register either way. This first account will also be an admin account. | false                                    |
| DOMAIN                    | Your Lynx installation domain                                                                                                                             | [http://example.com](http://example.com) |
| DEMO                      | Whether or not to enable the demo mode. In this mode features will be limited and links will be deleted after 10 minutes.                                 | false                                    |
| EXPRESS\_PORT             | The port to use internally for the backend.                                                                                                               | 3000                                     |
