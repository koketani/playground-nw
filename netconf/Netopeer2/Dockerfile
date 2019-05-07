FROM gcc

RUN apt-get update \
 && apt-get install -y git cmake openssh-server
RUN git config --global http.sslVerify false

# libyang
RUN apt-get install -y libpcre3 libpcre3-dev
RUN git clone https://github.com/CESNET/libyang.git /tmp/libyang
RUN cd /tmp/libyang; mkdir build; cd build \
 # && cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr .. \
 && cmake .. \
 && make \
 && make install

# libssh
RUN git clone http://git.libssh.org/projects/libssh.git /tmp/libssh
RUN cd /tmp/libssh; mkdir build; cd build \
 # && cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr .. \
 && cmake .. \
 && make \
 && make install

# libnetconf2
RUN git clone https://github.com/CESNET/libnetconf2 /tmp/libnetconf2
RUN cd /tmp/libnetconf2; mkdir build; cd build \
# && cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr .. \
# && cmake -DLIBYANG_LIBRARY=/usr/lib -DLIBYANG_INCLUDE_DIR=/usr/include -DLIBSSH_INCLUDE_DIR=/usr/include .. \
 && cmake .. \
 && make \
 && make install

# sysrepo
# RUN apt-get install git cmake build-essential bison flex libpcre3-dev libev-dev libavl-dev libprotobuf-c-dev protobuf-c-compiler
RUN apt-get install -y build-essential bison flex libpcre3-dev libev-dev libavl-dev libprotobuf-c-dev protobuf-c-compiler
RUN git clone https://github.com/sysrepo/sysrepo.git /tmp/sysrepo
RUN cd /tmp/sysrepo; mkdir build; cd build \
 && cmake .. \
 && make \
 && make install \
 # workaround
 && ldconfig

# Netopeer2
RUN git clone https://github.com/CESNET/Netopeer2.git /tmp/Netopeer2
RUN cd /tmp/Netopeer2/server; mkdir build; cd build \
 && cmake .. \
 && make \
 && make install

RUN rm -rf /var/lib/apt/lists/*
