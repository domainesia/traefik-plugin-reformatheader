# Rewrite Header Regex

Rewrite Header Regex is a middleware plugin for [Traefik](https://traefik.io) which extracts data via regexp from the target header and creates a new field with extracted content formatted using regex substitution.

## Configuration

### Static 

```toml
[pilot]
  token = "xxxx"

[experimental.plugins.reformatheader]
  modulename = "github.com/domainesia/traefik-plugin-reformatheader"
  version = "v0.0.1"
```


### Dynamic

To configure the Rewrite Head plugin you should create a [middleware](https://docs.traefik.io/middlewares/overview/) in your dynamic configuration as explained [here](https://docs.traefik.io/middlewares/overview/). The following example creates and uses the rewritehead middleware plugin to create a new header with extracted data foo from the HTTP request head.

```
[http]
  [http.routers]
    [http.routers.my-router]
      rule = "Host(`localhost`)"
      service = "my-service"
      middlewares = ["reformatheader"]

  [http.services]
    [http.services.my-service.loadBalancer]
      [[http.services.my-service.loadBalancer.servers]]
        url = "http://127.0.0.1"

  [http.middlewares]
    [http.middlewares.reformatheader.plugin.dev]
      fromhead  = "X-TargetHeader" //required
      regex     = "f(oo).?"        //required
      create    = "X-NewHeader"    //required
      format    = "${0}${1}"       //required

```

## Acknowledgement
This project is based on https://github.com/mrdrelar/traefik-plugin-rewriteheader.

## Licensing & Support Notice
MIT Licensed.

**[DomaiNesia](https://www.domainesia.com) neither support nor guarantee maintenance of this project**.

This is a part of giving back to open source community commitment from our company.
Yet, our team still small, so we will contribute and maintain on what we currently use.
