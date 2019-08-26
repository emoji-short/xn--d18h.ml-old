# xn--d18h.ml Emoji shortener

**xn--d18h.ml** is a modern URL shortener with support for custom domains. Shorten URLs, manage your links and view the click rate statistics.

*Contributions and bug reports are welcome.*

## Table of Contents
* [Key Features](#key-features)
* [Stack](#stack)
* [Setup](#setup)
* [Browser Extensions](#browser-extensions)
* [API](#api)
* [Integrate with ShareX](#sharex)
* [3rd Party API Packages](#3rd-party-api-packages)
* [Contributing](#contributing)

## Key Features
* Free and Emoji supported.
* Custom domain support.
* Custom URLs for shortened links
* Setting password for links.
* Private statistics for shortened URLs.
* View and manage your links.
* RESTful API.

## Stack
* Node (Web server)
* Express (Web server framework)
* Passport (Authentication)
* React (UI library)
* Next (Universal/server-side rendered React)
* Redux (State management)
* styled-components (CSS styling solution library)
* Recharts (Chart library)
* Neo4j (Graph database)

## Setup
You need to have [Node.js](https://nodejs.org/), [Neo4j](https://neo4j.com/) and [Redis](https://redis.io/) installed on your machine.

1. Fork & download this repository or [download zip](https://github.com/emoji-short/xn--d18h.ml/fork).
2. Copy `.example.env` to `.env`  and fill it properly.
3. Install dependencies: `npm install`.
4. Start Neo4j database.
5. Run for development: `npm run dev`.
6. Run for production: `npm run build` then `npm start`.

**Docker:** You can use Docker to run the app. Read [docker-examples](/docker-examples) for more info.

## Browser Extensions
Download extension for web browsers via below links. You can also find the source code on [kutt-extension](https://github.com/emoji-short/extension).
* [Chrome](#)
* [Firefox](#)

## API
In addition to the website, you can use these APIs to create, delete and get URLs.

### Types

```
URL {
  createdAt {string} ISO timestamp of when the URL was created
  id {string} Unique ID of the URL
  target {string} Where the URL will redirect to
  password {boolean} Whether or not a password is required
  count {number} The amount of visits to this URL
  shortUrl {string} The shortened link (Usually https://xn--d18h.ml/id)
}
```

In order to use these APIs you need to generate an API key from settings. Never put this key in the client side of your app or anywhere that is exposed to others.

All API requests and responses are in JSON format.

Include the API key as `X-API-Key` in the header of all below requests. Available API endpoints with body parameters:

**Get shortened URLs list:**
```
GET /api/url/geturls
```

Returns:
```
{
  list {Array<URL>} List of URL objects
  countAll {number} Amount of items in the list
}
```

**Submit a link to be shortened**:
```
POST /api/url/submit
```
Body:
  * `target`: Original long URL to be shortened.
  * `customurl` (optional): Set a custom URL.
  * `password` (optional): Set a password.
  * `reuse` (optional): If a URL with the specified target exists returns it, otherwise will send a new shortened URL.

Returns: URL object

**Delete a shortened URL** and **Get stats for a shortened URL:**
```
POST /api/url/deleteurl
GET /api/url/stats
```
Body (or query for GET request)
  * `id`: ID of the shortened URL.
  * `domain` (optional):  Required if a custom domain is used for short URL.
  
## 3rd Party API packages
| Language  | Link                                                       | Description                                       |
|-----------|------------------------------------------------------------|---------------------------------------------------|
| C# (.NET) | [KuttSharp](https://github.com/0xaryan/KuttSharp)          | .NET package for xn--d18h.ml url shortener            |
| Python    | [kutt-cli](https://github.com/univa64/kutt-cli)            | Command-line client for Kutt written in Python    |
| Ruby      | [kutt.rb](https://github.com/univa64/kutt.rb)              | Kutt library written in Ruby                      |
| Node.js   | [node-kutt](https://github.com/ardalanamini/node-kutt)     | Node.js client for xn--d18h.ml url shortener          |
| Bash      | [kutt-bash](https://git.nixnet.xyz/caltlgin/kutt-bash)     | Simple command line program for Kutt              |

## Contributing
Pull requests are welcome. You'll probably find lots of improvements to be made.

Open issues for feedback, requesting features, reporting bugs or discussing ideas.
