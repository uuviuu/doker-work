FROM node:22

RUN apt-get update && apt-get install -y \
        curl \
        git \
        fish \
        nano \
        mc \
        zsh
RUN chsh -s /usr/bin/fish

COPY --from=spiralscout/roadrunner:2.9.1 /usr/bin/rr /usr/bin/rr

RUN export DOCKER_SCAN_SUGGEST=false

USER node

WORKDIR /var/www

EXPOSE 3000
EXPOSE 8080
EXPOSE 8000

CMD ["node"]
