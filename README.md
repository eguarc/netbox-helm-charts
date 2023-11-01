# netbox-docker

[![GitHub release (latest by date)](https://img.shields.io/github/v/release/netbox-community/netbox-docker)][github-release]
[![GitHub stars](https://img.shields.io/github/stars/netbox-community/netbox-docker)][github-stargazers]
![GitHub closed pull requests](https://img.shields.io/github/issues-pr-closed-raw/netbox-community/netbox-docker)
![Github release workflow](https://img.shields.io/github/workflow/status/netbox-community/netbox-docker/release)
![Docker Pulls](https://img.shields.io/docker/pulls/netboxcommunity/netbox)
[![GitHub license](https://img.shields.io/github/license/netbox-community/netbox-docker)][netbox-docker-license]

[The GitHub repository][netbox-docker-github] houses the components needed to build NetBox as a container.
Images are built regularly using the code in that repository and are pushed to [Docker Hub][netbox-dockerhub], [Quay.io][netbox-quayio] and [GitHub Container Registry][netbox-ghcr].

[github-stargazers]: https://github.com/netbox-community/netbox-docker/stargazers
[github-release]: https://github.com/netbox-community/netbox-docker/releases
[netbox-dockerhub]: https://hub.docker.com/r/netboxcommunity/netbox/
[netbox-quayio]: https://quay.io/repository/netboxcommunity/netbox
[netbox-ghcr]: https://github.com/netbox-community/netbox-docker/pkgs/container/netbox
[netbox-docker-github]: https://github.com/netbox-community/netbox-docker/
[netbox-docker-slack]: https://join.slack.com/t/netdev-community/shared_invite/zt-mtts8g0n-Sm6Wutn62q_M4OdsaIycrQ
[netbox-docker-slack-channel]: https://netdev-community.slack.com/archives/C01P0GEVBU7
[netbox-slack-channel]: https://netdev-community.slack.com/archives/C01P0FRSXRV
[netbox-docker-license]: https://github.com/netbox-community/netbox-docker/blob/release/LICENSE



---
This chart works with the (11-2023) latest version of netbox container image (v3.6.4-2.7.0).

based from https://github.com/netbox-community/netbox-docker/blob/release/docker-compose.yml

created from `helm create` command

`helm version`

 `version.BuildInfo{Version:"v3.13.1", GitCommit:"3547a4b5bf5edb5478ce352e18858d8a552a4110", GitTreeState:"clean", GoVersion:"go1.20.8"}`

---

`kubectl create ns netbox`

`kubectl apply -n netbox -f netbox/secrets.yaml`

`helm upgrade -i netbox -n netbox -f netbox/values.yaml netbox/`

`helm upgrade -i netbox-worker -n netbox -f netbox-worker/values.yaml netbox/`

`helm upgrade -i netbox-housekeeping -n netbox -f netbox-housekeeping/values.yaml netbox-housekeeping/`

`helm upgrade -i redis -n netbox -f redis/values.yaml redis/`

`helm upgrade -i redis-cache -n netbox -f redis-cache/values.yaml redis-cache/`


---
misc/tricks:

https://github.com/ray-project/ray/issues/8023 -- you must set in redis and redis-cache the value of the envvar REDIS_PASSWORD using redis-cli:

`kubectl -n netbox -it [redis-pod] -- redis-cli`

`127.0.0.1:6379> config set requirepass value-of-envvar`

`kubectl -n netbox -it [redis-cache-pod] -- redis-cli`

`127.0.0.1:6379> config set requirepass value-of-envvar`

