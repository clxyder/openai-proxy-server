# openai-proxy-server

Use litellm as an openai proxy server for redis caching and llm observability with langfuse

Copy `.env.example` to `.env` and update missing environment variables.

Then, run the following command to start the proxy server:

```bash
docker compose up -d
```

## Traefik Reverse Proxy

Traefik allows one to connect to the following services from an easy to remember fully-qualified domain name (FQDN) from the browswer.

* litellm - litellm.docker.localhost
* langfuse - langfuse.docker.localhost
* whoami - whoami.docker.localhost
* traefik - traefik.docker.localhost

## Dnsmasq Configuration

To be able to `curl` one of those domains, we need a DNS server with a wildcard (.localhost) to point to our running traefik instance.

```conf
#log all dns queries
log-queries
#dont use hosts nameservers
no-resolv
# explicitly define host-ip mappings
address=/.localhost/127.0.0.1
```

Finally, to ensure that your local system leverages the newly created DNS server update your `/etc/resolv.conf` by adding `nameserver 127.0.0.1` to the first `nameserver` entry if it's not already present.
