ARG NODE_VERSION=6
FROM node:${NODE_VERSION}

ENV USER=node-red USER_ID=1033 USER_GID=100

# Home directory for Node-RED application source code.
RUN mkdir -p /usr/src/node-red

# User data directory, contains flows, config and nodes.
RUN mkdir /data

WORKDIR /usr/src/node-red

# Add node-red user so we aren't running as root.
RUN useradd --home-dir /usr/src/node-red --uid ${USER_ID} --gid ${USER_GID} --no-create-home ${USER} \
    && chown -R ${USER}:${USER_GID} /data \
    && chown -R ${USER}:${USER_GID} /usr/src/node-red

USER ${USER}

# package.json contains Node-RED NPM module and node dependencies
COPY package.json /usr/src/node-red/
RUN npm install

# User configuration directory volume
EXPOSE 1880

# Environment variable holding file path for flows configuration
ENV FLOWS=flows.json
ENV NODE_PATH=/usr/src/node-red/node_modules:/data/node_modules

CMD ["npm", "start", "--", "--userDir", "/data"]
