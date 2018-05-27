# Troubleshooting

Since we are using a Hackintosh we should find problem during the use of particular application like:

* Docker

## Docker

In the [requirements](https://daton.gitbook.io/daton-mac/~/edit/primary/hackintosh/troubleshooting) section of this chapter, we changed some configuration of the BIOS, but if we need to use `Docker` or `VirtualBox` probably we need to enable Intel Virtualisation in our BIOS setting, otherwise we should fall in a issue like: [Fatal Error: com.docker.supervisor failed to start. Exit code 1 at docker startup on mac](https://github.com/docker/for-mac/issues/2535).

