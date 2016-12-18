# CFSSL-Alpine Docker image
This is a Docker image for CloudFlare's CFSSL including all CFSSL utilities provided by CloudFlare, based on the Alpine base image.

## Usage:
There are two ways to use this image: with a `docker run` command, or with the bundled wrapper scripts.

### Docker run command
`docker run -i --rm -v $(pwd):/cfssl lindeboomio/cfssl <command>`

Where command is one of:
- cfssl
- cfssl-bundle
- cfssl-certinfo
- cfssl-newkey
- cfssl-scan
- cfssljson
- mkbundle
- multirootca

## Wrapper scripts
For each CFSSL command, a wrapper script is included with the proper `docker run` command.

### Deploying the wrapper scripts
To dump the wrapper scripts, run the following command:
`docker run -i --rm -v $(pwd):/cfssl lindeboomio/cfssl dump-wrappers`

The wrapper scripts will be placed in the `wrappers` directory, and have to be moved to a location in your path, e.g. `/usr/local/bin`:
`sudo mv wrappers/* /usr/local/bin`

### Using the wrapper scripts
With the wrapper scripts in your path, the CFSSL commands should be usable as usual, with one minor but important caveat: _because only the current directory (pwd) is mounted into the container, only paths relative to the current directory will generally work_.

Note: the wrapper scripts runs `cfssl` and `multirootca` with host networking enabled, to allow for running the servers on custom ports.

## Examples
To get going with CFSSL, there is an article over at [the CloudFlare blog](https://blog.cloudflare.com/how-to-build-your-own-public-key-infrastructure/) with examples that have been demonstrated to work, with one addition: to enable a CFSSL server to sign certificates, a `sign cert` usage needs to be added to the CA policy file (`config_ca.json`):

```
[..]
    "usages": [
        "signing",
        "key encipherment",
        "server auth",
        "sign cert"
    ]
[..]
```

## To do
- Clean up after the Go build
