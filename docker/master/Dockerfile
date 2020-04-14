# based on alpine:3.7
FROM buildbot/buildbot-master:master

# install pillow dependencies
RUN apk add build-base python3-dev jpeg-dev zlib-dev cairo cairo-dev

# install pip dependencies
RUN pip3 install buildbot-badges

CMD ["dumb-init", "/usr/src/buildbot/docker/start_buildbot.sh"]