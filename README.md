# reverseproxy
A reverseproxy docker-compose file based on jwilder's dockerhub image : https://hub.docker.com/r/jwilder/nginx-proxy/

## How
1. `docker-compose up --build`
2. Make sure the docker container you want to publish have access to the `reverseproxy_default` network
3. Add a `VIRTUAL_HOST=hostname` environment variable to the container you want to publish
4. Add the hostname to your `/etc/hosts` file : `127.0.1.1 hostname`
5. Expose a single port on the docker container you want to publish. If multiple ports are exposed then add the `VIRTUAL_PORT=port_number` environment to the container
6. Access `http://hostname` on your browser

## Debug
1. Check that both the reverse proxy container and app container are running
2. Run `docker network inspect reverseproxy_default` and check that both containers appear
3. Run `docker exec -ti reverseproxy_reverseproxy_1 cat /etc/nginx/conf.d/default.conf` and check that the upstream is correctly defined, example : `upstream hostname { server 172.20.0.3:4200; }`
