FROM pun4drunk/rpi-selenium-node-base
MAINTAINER pun4drunk "pun4drunk@gmail.com"

USER root

#=========
# Firefox
#=========
ARG FIREFOX_VERSION=52.0

RUN apt-get update
RUN apt-get -y --no-install-recommends install firefox \
&& apt-get -y purge firefox \
&& rm -rf /var/lib/apt/lists/* /var/cache/apt/*

RUN wget --no-verbose -O /tmp/firefox.deb \
  http://launchpadlibrarian.net/311357638/firefox_$FIREFOX_VERSION.1+build2-0ubuntu0.14.04.1_armhf.deb \
  && dpkg -i /tmp/firefox.deb

#============
# GeckoDriver
#============
ARG GECKODRIVER_VERSION=0.15.0

RUN wget --no-verbose -O /tmp/geckodriver.tar.gz \
  https://github.com/mozilla/geckodriver/releases/download/v$GECKODRIVER_VERSION/geckodriver-v$GECKODRIVER_VERSION-arm7hf.tar.gz \
  && rm -rf /opt/geckodriver \
  && tar -C /opt -zxf /tmp/geckodriver.tar.gz \
  && rm /tmp/geckodriver.tar.gz \
  && mv /opt/geckodriver /opt/geckodriver-$GECKODRIVER_VERSION \
  && chmod 755 /opt/geckodriver-$GECKODRIVER_VERSION \
  && ln -fs /opt/geckodriver-$GECKODRIVER_VERSION /usr/bin/geckodriver

#========================
# Selenium Configuration
#========================
ENV NODE_MAX_INSTANCES 1
ENV NODE_MAX_SESSION 1
ENV NODE_REGISTER_CYCLE 5000
ENV NODE_PORT 5555
ENV NODE_APPLICATION_NAME ""
COPY generate_config /opt/selenium/generate_config
RUN chmod +x /opt/selenium/generate_config \
  && chown -R seluser:seluser /opt/selenium

USER seluser
