FROM        --platform=$TARGETOS/$TARGETARCH node:18-bullseye-slim

LABEL       author="Ryujin" maintainer="ryudev.id@gmail.com"

RUN         apt update \
            && apt -y install imagemagick neofetch webp sudo ffmpeg iproute2 git sqlite3 libsqlite3-dev python3 python3-dev php php-curl libcurl4-openssl-dev python python-pip pip ca-certificates dnsutils tzdata zip tar curl build-essential libtool iputils-ping libnss3 tini \
            && useradd -m -d /home/container container

RUN 	    apt -y install libnss3 libatk-bridge2.0-0 libatk1.0-0 libcups2 libxcomposite1 libxrandr2 libgbm1 libasound2 libxtst6 xdg-utils \
    	    && npm i playwright --save-dev
    
RUN         npm install typescript ts-node @types/node --location=global

RUN	    npm i npm@latest -g && \
            npm i yarn -g && \
	    npm i pm2 -g 
RUN	    npx playwright install
USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

STOPSIGNAL SIGINT

COPY        --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
ENTRYPOINT    ["/usr/bin/tini", "-g", "--"]
CMD         ["/entrypoint.sh"]
