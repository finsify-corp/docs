# Architecture

## API architecture

![api](https://i.imgur.com/OgOj32W.png)

### Webhook listen events

- request.ready
- request.running
- request.failed
- request.successful
- merchant.progress
- merchant.successful

### Router listen events

- *.failed.#
- merchant.successful
- transaction.successful

## Crawler architecture

![crawler](https://i.imgur.com/sugN3JB.png)

