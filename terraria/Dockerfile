# vanilla Terraria server
#
# docker run -dit --name=terraria -v <config dir>:/opt/terraria -p 7777:7777 jonmeacham/terraria:latest

# get mono base
FROM mono:5.14.0.177

# install unzip
RUN apt-get update && \
    apt-get install -y \
    unzip

# download server archive
ENV RELEASE 1353
RUN cd /opt && \
    curl -OL "http://terraria.org/server/terraria-server-${RELEASE}.zip" && \
    unzip terraria-server-${RELEASE}.zip && \
    rm -rfv ./${RELEASE}/Mac/ && \
    rm -rfv ./${RELEASE}/Windows/ && \
    rm -fv ./${RELEASE}/Linux/System.dll

# server config volume
VOLUME /opt/terraria

# set the working directory
WORKDIR /opt

# expose server port
EXPOSE 7777

# start server by default
ENTRYPOINT ["/usr/bin/mono", \
    "--server", \
    "--gc=sgen", \
    "-O=all", \
    "./1353/Linux/TerrariaServer.exe", \
    "-config", "/opt/terraria/serverconfig"]
