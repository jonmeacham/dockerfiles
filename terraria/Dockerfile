# vanilla Terraria server
#
# docker run -dit --name=terraria -v <config dir>:/opt/terraria -p 7777:7777 jonmeacham/terraria:latest

# get mono base
FROM mono:6.8.0.96

# install unzip
RUN apt-get update && \
    apt-get install -y \
    unzip

# download server archive
ENV RELEASE 1402
RUN cd /opt && \
    #curl -OL "http://terraria.org/server/terraria-server-${RELEASE}.zip" && \
    # temporarily use new nonstandard server archive download URL
    curl -OL "https://terraria.org/system/dedicated_servers/archives/000/000/036/original/terraria-server-1402.zip" && \
    unzip terraria-server-${RELEASE}.zip && \
    rm -rfv ./${RELEASE}/Mac/ && \
    rm -rfv ./${RELEASE}/Windows/ && \
    chmod +x ./${RELEASE}/Linux/TerrariaServer && \
    chmod +x ./${RELEASE}/Linux/TerrariaServer.bin.x86_64

# server config volume
VOLUME /opt/terraria

# set the working directory
WORKDIR /opt

# expose server port
EXPOSE 7777

# start server by default
ENTRYPOINT ["./1402/Linux/TerrariaServer", \
    "-config", "/opt/terraria/serverconfig"]
