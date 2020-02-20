FROM        node:10

ENV         TINI_VERSION=v0.18.0
ADD         https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini

WORKDIR     /opt/hospitalrun

COPY        /root/opt/hospitalrun/package.json /opt/hospitalrun

RUN         apt-get update && \
            apt-get install -y ca-certificates && \
            rm -rf /var/lib/apt/lists/* && \
            yarn install && \
            chmod +x /tini

COPY        /root/opt/hospitalrun/config.js /opt/hospitalrun
COPY        /root/opt/hospitalrun/app.js /opt/hospitalrun

VOLUME      ["/opt/hospitalrun/patientimages", "/opt/hospitalrun/attachments"]

EXPOSE      3000

ENTRYPOINT  ["/tini", "--"]

CMD         ["npm", "start", "/opt/hospitalrun/app.js"]
