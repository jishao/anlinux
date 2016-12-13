build environment
===

ubuntu 16.04 amd64
openjdk7

sudo apt-get install git-core gnupg flex bison gperf build-essential \
  zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 \
  lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache \
  libgl1-mesa-dev libxml2-utils xsltproc unzip

sudo apt-get purge libncurses5-dev:i386  libx11-dev:i386  libreadline6-dev:i386  tofrodos python-markdown  zlib1g-dev:i386   dpkg-dev  libsdl1.2-dev  libesd0-dev maven
