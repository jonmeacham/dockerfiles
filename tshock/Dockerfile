# TShock provides Terraria servers with server-side characters, anti-cheat, and community management tools.
#
# docker run -dit --name=tshock -v <config path>:/opt/tshock -p 7777:7777 <image>

# get mono base
FROM mono:6.8.0.96

# install unzip
RUN apt-get update && \
    apt-get install -y \
    unzip

# grab tshock release
ENV RELEASE 4.3.26
RUN cd /opt && \
    curl -OL "https://github.com/Pryaxis/TShock/releases/download/v${RELEASE}/tshock_${RELEASE}.zip" && \
    unzip tshock_${RELEASE}.zip

# volume for tshock data
VOLUME /opt/tshock

# set the working directory
WORKDIR /opt

# expose server port
EXPOSE 7777

# define default command
ENTRYPOINT ["/usr/bin/mono", \
    "--server", \
    "--gc=sgen", \
    "-O=all", \
    "TerrariaServer.exe", \
    "-config", "/opt/tshock/serverconfig"]
