# Running application in Docker

Assumptions:
The domain in this example is `xn--d18h.local`. This needs to be configured in your hosts file for this example to work _as written_. You should, of course, modify this domain to suit your needs. 

### Configure Kutt

server/config.js
```
module.exports = {

	PORT: process.env.EMOJI_PORT, # Or whatever you want to name the env var
    
    /* The domain that this website is on */
    DEFAULT_DOMAIN: process.env.EMOJI_DOMAIN, # Or whatever..
    
    ...
    
}
```

No docker-relevant modifications are necessary for client/config.js. However, you will still need to configure this as part of the standard application setup. 

### Neo4j in a container

You can run neo4j in a container and link it to the kutt container in Docker. 

Properly installing and running neo4j is outside of the scope of this document. But here's a simple one-liner to get neo4j running on docker for dev/test:

```
docker run \
    --publish=7474:7474 --publish=7687:7687 \
    --name neo4j \
    neo4j
```
**This is not a production-ready setup. There is no data persistence, nor proper security. Use for test/dev only.**

Then, configure xn--d18h:
server/config.js
```
...
/* Neo4j database credential details */
DB_URI: 'bolt://neo4j',
DB_USERNAME: 'neo4j', # Or pass this in via env var as before 
DB_PASSWORD: 'neo4j', # Or via env var..
...
```

Once you have neo4j running in a container, you'll link your xn--d18h container to it. This will be documented below.

### Build xn--d18h Image

First you'll need to build xn--d18h.
From the root directory of xn--d18h, execute the following:
`docker build -t xn--d18h .`

### Run xn--d18h

Once you've built the image, then all that is left to do is run xn--d18h.

`docker run -d -p80:3000 -e EMOJI_PORT=3000 -e EMOJI_DOMAIN=xn--d18h.local --link=neo4j xn--d18h`

Direct your browser to http://xn--d18h.local/ and begin compress URLs!
