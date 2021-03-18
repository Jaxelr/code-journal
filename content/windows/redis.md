# Running redis on windows

1. Install using [chocolatey](https://chocolatey.org/)
1. run `cinst redis-64`
1. run `redis-server --service-install`
1. run `redis-server --service-start`
1. When finished run `redis-server --service-stop`

## Uninstall

1. run `redis-server service-uninstall`
1. run `cuninst redis-64`
