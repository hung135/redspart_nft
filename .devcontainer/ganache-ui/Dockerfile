
FROM mcr.microsoft.com/vscode/devcontainers/base:0-buster
 
USER root 
RUN apt-get update

RUN apt-get install -y wget libgtk-3-dev libgtkextra-dev libgconf2-dev libnss3 libasound2 libxtst-dev libxss1 libx11-6 libx11-xcb-dev

RUN apt-get -y install curl gnupg
RUN curl -sL https://deb.nodesource.com/setup_15.x  | bash -
RUN apt-get -y install nodejs make fish
RUN npm install -g n
RUN n 12.13.1  
RUN apt-get install -y webpack
WORKDIR /tmp
RUN wget https://github.com/trufflesuite/ganache-ui/archive/refs/tags/v2.6.0-beta.3.tar.gz
RUN tar -xvf v2.6.0-beta.3.tar.gz 
WORKDIR /tmp/ganache-ui-2.6.0-beta.3 
RUN apt-get install -y gcc g++ build-essential git python
RUN npm config set loglevel verbose
RUN sed -i 's/x64/arm64/g' package.json
RUN npm install
#RUN npm run dev
RUN sed -i 's/x64/arm64/g' package.json
RUN npm run build-linux  
WORKDIR /tmp/ganache-ui-2.6.0-beta.3/dist

#RUN chmod +x ganache-2.6.0-beta.3-linux-x86_64.AppImage
# RUN ./ganache-2.6.0-beta.3-linux-x86_64.AppImage --appimage-extract
# RUN rm ganache-2.6.0-beta.3-linux-x86_64.AppImage

ENV DISPLAY=host.docker.internal:0
EXPOSE 7545
ENTRYPOINT ["./squashfs-root/AppRun"]
# EXPOSE 7545
# ENTRYPOINT ["./squashfs-root/AppRun"]
CMD [ "sleep", "infinity" ]