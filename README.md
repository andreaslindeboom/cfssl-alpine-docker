#CFSSL Docker image
This is a Docker image for CloudFlare's CFSSL including all CFSSL utilities provided by CloudFlare.

##Usage:
`docker run -it --rm -v $(pwd):/cfssl lindeboomio/cfssl <command>`

###Commands
The included commands are:
- cfssl
- cfssl-bundle
- cfssl-certinfo
- cfssl-newkey
- cfssl-scan
- cfssljson
- mkbundle
- multirootca

##Dumping convenience wrapper scripts
For each utility, a wrapper script is included with the proper `docker run` command.

To dump these wrapper scripts to the current directory, run the following command:
`docker run -i --rm -v $(pwd):/cfssl lindeboomio/cfssl dump-wrappers`

##To do
- Set up automated Docker Hub builds
- Clean up after the Go build
