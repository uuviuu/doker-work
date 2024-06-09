FROM node:18

RUN apt-get update && apt-get install -y \
        curl \
        git \
        fish \
        nano \
        mc \
        zsh
RUN chsh -s /usr/bin/fish

COPY --from=spiralscout/roadrunner:2.9.1 /usr/bin/rr /usr/bin/rr

RUN yarn install
RUN npm install -g npm@10.3.0 \
    -g @vue/cli

RUN export DOCKER_SCAN_SUGGEST=false

USER node

WORKDIR /var/app

EXPOSE 3000
EXPOSE 8080
EXPOSE 8000

CMD ["node"]