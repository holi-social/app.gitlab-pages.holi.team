---
layout: default
---

# Introduction

This document will help you dive into holi quickly. It will lay out the structure of the project (runtime and
repositories) and hopefully give you guidance on where to head for working on what you want to accomplish.

## Repositories

holi is comprised of many parts (deployment units). This section will explain, in rough order of importance, all of
them.

### Meta

TL;DR: Check out this repository to get going quickly.

[holi-meta](https://gitlab.holi.team/app/holi-meta)

holi-meta is your helper for quickly setting up a full development environment. It contains scripts for setting up a
full workspace, checking out all necessary repositories. It also contains helpers for running local environments from
minimal to full.

The [README](https://gitlab.holi.team/app/holi-meta) contains everything you need to start actually fetching, building
and running code, no matter which area you want to focus on.

### Frontends

[holi-frontends](https://gitlab.holi.team/app/holi-frontends)

holi-frontends contains all code for the [Web App](https://app.holi.social) as well as for the 
[iOS](https://apps.apple.com/pt/app/holi-social-eco-impact/id6446693757) and 
[Android](https://apps.apple.com/pt/app/holi-social-eco-impact/id6446693757) Mobile Apps.

The [README](https://gitlab.holi.team/app/holi-frontends) contains further documentation regarding the frontends.

### Unified API

[holi-unified-api](https://gitlab.holi.team/app/holi-unified-api)

The holi-unified-api is the component providing the frontend with a single API, merging different backend APIs into one
and taking care of authentication and authorization.

The [README](https://gitlab.holi.team/app/holi-unified-api) contains further documentation regarding the Unified API.

### Social

[holi-okuna](https://gitlab.holi.team/app/holi-okuna)

holi-okuna is the backend that takes care of the social components of holi. In here, there's user profiles &
preferences, posts, insights and a lot more. This project was forked by us. Originally, it had been developed as a
social network.

The [README](https://gitlab.holi.team/app/holi-okuna) contains further documentation regarding the Unified API.

### the app repositories

[holi-app-donations](https://gitlab.holi.team/app/holi-app-donations)
[holi-app-goodnews](https://gitlab.holi.team/app/holi-app-goodnews)
[holi-app-volunteering](https://gitlab.holi.team/app/holi-app-volunteering)

holi can integrate so called Apps. These can be developed by third parties. We have implemented three of them up to
now. The repositories above contain their respective backend.

### Chat

[holi-chat-server](https://gitlab.holi.team/app/holi-chat-server)

holi contains a chat based on [synapse](https://github.com/matrix-org/synapse) by the Matrix.org Foundation. This
repository contains the deployment configuration for this service.

### Geo-API

[[Repository](https://gitlab.holi.team/app/holi-geo-api)

Some searches on holi can be filtered by geolocation (e.g. initiatives, users, ...). This repository contains a backend
service for accessing geolocation data.

### Cloud

[holi-ocis](https://gitlab.holi.team/app/holi-ocis)
[holi-ocis-integration](https://gitlab.holi.team/app/holi-ocis-integration)

For initiatives, holi provides cloud storage and collaborative document editing. The technical component these are
provided with is Owncloud OCIS. These two repositories contain the deployment configuration for this service.

### Videoconferences

[holi-meet](https://gitlab.holi.team/app/holi-meet)

For initiatives, holi also provides Video Chat. It is based on Jitsi Meet. This repository contains the deployment
configuration for this service.

## Runtime Architecture

This section describes the runtime architecture of holi. Let's start with a (simplified) diagram, and then dive into some details:

![Runtime Architecture Diagram](/assets/images/runtime-architecture.png)

### Frontends

The Web Frontend and the Mobile Apps work a little bit different from each other.

The Mobile Apps directly connect to the Unified API for fetching data. For authenticating users, they directly interact
with our Identity Provider, [Ory](https://ory.sh).

The Web App proxies requests to the Unified API and to Ory through a server component, which also handles Server Side
Rendering (Web SSR in the diagram).

### Identity Provider

We are using an external service, [Ory](https://ory.sh), as Identity Provider.

### Services

Most services are completely hidden from the clients and only accessible via the Unified API. There is some services like
Cloud, Chat, Video Calls that are accessible from Clients because they need to be for proper function. This is not
accurately portrayed in the diagram.

### Google Cloud

Almost all our services/infrastructure run in the Google Cloud.

#### Pub/Sub

As an asynchronous data exchange & replication mechanism, some backend services communicate with one another via the Google Pub/Sub message queue.

