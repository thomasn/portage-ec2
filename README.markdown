# portage-ec2 - Amazon ec2-* tools for Gentoo Portage

## Intro

The Amazon [apitools](http://developer.amazonwebservices.com/connect/entry.jspa?externalID=351&categoryID=88) and 
[amitools](http://developer.amazonwebservices.com/connect/entry.jspa?externalID=368) packages are commandline
tools for managing EC2. The ec2-sources are the Amazon-tweaked Xen sources.  
Requirements: Ruby, Java.  
Use this overlay to install using Gentoo's `layman`.

## Installation

As root:

    emerge -av layman
    $EDITOR /etc/layman/layman.cfg    # Add to 'overlays' section:
      http://github.com/gentoo/portage-ec2/blob/master/overlay.xml?raw=true
    layman -a portage-ec2
    layman -S
    layman -l    # should show 'portage-ec2'
    echo 'source /usr/portage/local/layman/make.conf' >> /etc/make.conf
    emerge -av sys-cluster/ec2-ami-tools sys-cluster/ec2-api-tools
    # and if you want to build custom kernels:
    emerge -av sys-kernel/ec2-sources

Feedback via github please.