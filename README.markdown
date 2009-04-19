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

These tools need environment vars. Check where the tools are installed:

    stat  -t -c %N `which ec2run`           # use for EC2_HOME
    stat  -t -c %N `which ec2-bundle-vol`   # use for EC2_AMITOOL_HOME

then add to ~/.bash_profile or equivalent:

    export EC2_HOME=/opt/ec2-api-tools-1.3.33670
    export EC2_AMITOOL_HOME=/opt/ec2-ami-tools-1.3.31780

or add this experimental hack -- please improve!

    export EC2_HOME=`ruby -e 'p %x{stat  -t -c %N /usr/bin/ec2run}.split[2].split("/")[0..-3].join("/")[1,999]'| sed -e 's/"//g'`
    export EC2_AMITOOL_HOME=`ruby -e 'p %x{stat  -t -c %N /usr/bin/ec2-bundle-vol}.split[2].split("/")[0..-3].join("/")[1,999]'| sed -e 's/"//g'`

Feedback via github please.
