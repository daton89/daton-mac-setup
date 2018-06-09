# Sentry

If you build Web Application, you probably use Sentry. We are going to setup a self-hosted instance of Sentry running Docker.

{% embed data="{\"url\":\"https://sentry.io/welcome/\",\"type\":\"link\",\"title\":\"Sentry \| Error Tracking Software — JavaScript, Python, PHP, Ruby, more\",\"description\":\"Open-source error tracking that helps developers monitor and fix crashes in real time. Iterate continuously. Boost workflow efficiency. Improve user experience.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://sentry.io/\_assets/favicon-9d9dbcc614d52b0e88787b03b400b5bf6c6467d6837a19d394f9e8b8d98bee4b.ico\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://sentry.io/\_assets/og/default-ece813046f72308a5f52e8ed4f5ff498920320ef76bbad88df5d1de0469cb185.jpg\",\"width\":1200,\"height\":630,\"aspectRatio\":0.525}}" %}

## Installation of Sentry On Premise 

Clone of fork Sentry On Premise: 

```bash
git clone https://github.com/getsentry/onpremise.git ~/Projects/SentryOnPremise
```

There may need to be modifications to the included `docker-compose.yml` file to accommodate your needs or your environment. These instructions are a guideline for what you should generally do.

1. `mkdir -p data/{sentry,postgres}` - Make our local database and sentry config directories. This directory is bind-mounted with postgres so you don't lose state!
2. `docker-compose run --rm web config generate-secret-key` - Generate a secret key. Add it to `docker-compose.yml` in `base` as `SENTRY_SECRET_KEY`.
3. `docker-compose run --rm web upgrade` - Build the database. Use the interactive prompts to create a user account.
4. `docker-compose up -d` - Lift all services \(detached/background mode\).
5. Access your instance at `localhost:9000`!

Note that as long as you have your database bind-mounted, you should be fine stopping and removing the containers without worry.

{% embed data="{\"url\":\"https://github.com/getsentry/onpremise\",\"type\":\"link\",\"title\":\"getsentry/onpremise\",\"description\":\"onpremise - Sentry On-Premise setup\",\"icon\":{\"type\":\"icon\",\"url\":\"https://github.com/fluidicon.png\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://avatars1.githubusercontent.com/u/1396951?s=400&v=4\",\"width\":96,\"height\":96,\"aspectRatio\":1}}" %}



