# Tooling for using haproxy on Triton.

This is a file to build a zone using packer to give the basic tooling
that I rely upon when using haproxy on Triton.

The file haproxy is the packer build file that will establish a zone
image.  It assumes you have an in place [triton-cli](https://docs.joyent.com/public-cloud/api/triton-cli)
environment variables and that the profile name is joyent. 

Build with the command line:

```packer build -var-file=config/$TRITON_PROFILE.vars haproxy```

I mutate variables for the build on a per triton profile basis, thus the above command

The built zone contains a number of useful bits including:

 - acme.sh for getting letsencrypt certs.
 - a default self signed certificate created upon zone init.
 - manta-backup, a script that will snag your config and put it in a manta
 - example haproxy.cfg, including the routing to get letsencrypt tests to the standalone acme server
 - acme-get-cert, a shell of a command to ask acme to get a cert for $domain
 - logging of haproxy to /var/log/haproxy.date-hour

Hope you find it handy

