# TShock provides Terraria servers with server-side characters, anti-cheat, and community management tools.
#
# docker run -d --name=tshock -v <config path>:/data -p 7777:7777 

# get mono base
FROM mono:5.14.0.177

# install required packages
RUN apt-get update && \
    apt-get install -y \
    git

# grab tshock source
RUN git clone --recurse-submodules https://github.com/Pryaxis/TShock.git /opt/tshock

# run the build
RUN cd /opt/tshock && \
    nuget restore ./TerrariaServerAPI/ && \
    xbuild ./TerrariaServerAPI/TShock.4.OTAPI.sln /p:Configuration=Release && \
    cd ./TerrariaServerAPI/TShock.Modifications.Bootstrapper/bin/Release/ && \
    mono TShock.Modifications.Bootstrapper.exe -in=OTAPI.dll \
    -mod=../../../TShock.Modifications.**/bin/Release/TShock.Modifications.*.dll \ 
    -o=Output/OTAPI.dll && \
    cd ./../../../ && \
    xbuild ./TerrariaServerAPI/TerrariaServerAPI.csproj /p:Configuration=Release && \
    cd .. && \
    nuget restore && \
    xbuild ./TShock.sln /p:Configuration=Release

# volume for tshock data.
VOLUME /data

# set the working directory
WORKDIR /

# Expose ports.
EXPOSE 7777

# Define default command.
ENTRYPOINT ["/usr/bin/mono", \
    "--server", "--gc=sgen", "-O=all", \
    "/opt/tshock/TShockAPI/bin/Release/TerrariaServer.exe", \
    "-config", "/data/serverconfig", \
    "-configpath", "/data"]
CMD ["--nolaunch", "--datadir=/data"]
