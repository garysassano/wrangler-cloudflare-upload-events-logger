# wrangler-cloudflare-upload-events-logger

Wrangler app that generates a log upon uploading a file to an R2 bucket.

### Related Apps

- [cdktf-cloudflare-upload-events-logger](https://github.com/garysassano/cdktf-cloudflare-upload-events-logger) - Built with CDKTF instead of Wrangler.

## Prerequisites

- **_Cloudflare:_**
  - Must have set the `CLOUDFLARE_API_TOKEN` variable in your local environment.
- **_pnpm:_**
  - Must be [installed](https://pnpm.io/installation) in your system.
- **_Wrangler:_**
  - Must be [installed](https://developers.cloudflare.com/workers/wrangler/install-and-update/) in your system.

## Deployment

Create R2 buckets:

```sh
npx wrangler r2 bucket create upload-bucket
npx wrangler r2 bucket create log-bucket
```

Create queue:

```sh
npx wrangler queues create event-notification-queue
```

Create worker:

```sh
npx wrangler deploy
```

Enable R2 event notifications:

```sh
npx wrangler r2 bucket notification create upload-bucket --event-type object-create --queue event-notification-queue
```

## Usage

1. Upload a file to `upload-bucket` from the Cloudflare dashboard.

2. After the upload is complete, logs will appear in `log-bucket`.

## Cleanup

```sh
npx wrangler delete
```

## Architecture Diagram

![Architecture Diagram](./src/assets/arch-diagram.svg)
