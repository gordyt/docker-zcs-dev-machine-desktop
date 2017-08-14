# Notes

## build-image

This will build a base ZCS developer image, software-only install, with the idea that we
can more quickly bring it up with all the prerequisites for doing development.
For this test I'm basing it on Ubuntu Desktop, 16.04.
Repository and tag are as follows:

    gordy/zcs-ubuntu-desktop-1604:8.8.1-zcs-base 

## software-install-responses

The `software-install-responses` file is used to feed responses to the command 
`./install.sh -s`.  The lines in the file are responding to the following
questions:

    Y - license?
    Y - zimbra repos?
    Y - LDAP?
    Y - LOGGER?
    Y - MTA?
    Y - DNSCACHE?
    Y - SNMP?
    Y - STORE?
    Y - APACHE?
    Y - SPELL?
    Y - MEMCACHED?
    Y - PROXY?
    Y - CHAT?
    Y - DRIVE?
    Y - IMAP?
    Y - System will be modified, continue?

## run-image

This will run the image created by the `build-image` script.  Two host directories are 
mapped into the image:

    slash-zimbra -> /zimbra
    home-zimbra -> /home/zimbra


NOTE: This takes a while (like 10 minutes or so on my mac) to complete because our configuration
process is slow.  We are working on that!  The name of the container will be `zcs-dev`.  

Several ports are mapped to the host by the `run-image` script. Adjust this as required.
At the last part of the run setup you are asked to enter a password. That is the password
you wish to use to connect to the running image via `vnc` (to localhost:5901).

You can use `C-p C-q` to switch the container to daemon mode after startup is complete.
You can pause the container when you are not using it to save resources on the host (`docker pause zcs-dev`).
Also, you should add an entry in `/etc/hosts` that maps `zcs-dev.test` to your host's IP address
so that the `HOST` header is set correctly when you want to use the Zimbra Web Client.

