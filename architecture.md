# Architecture

## API architecture

![api](https://i.imgur.com/OgOj32W.png)

### Webhook listen events

- request.ready: The request is received and on queue.
- request.running: The request start running.
- request.failed: Request failed.
- request.successful: Request completed successful.
- merchant.request: Request for otp, secret password
- merchant.progress: Current state of the crawler.
- merchant.successful: Crawler completed successful.
- request.successful: Request completed successful.

### Router listen events

- *.failed.#
- merchant.successful
- transaction.successful

## Crawler architecture

![crawler](https://i.imgur.com/sugN3JB.png)

