ARG BUILD_FROM
FROM $BUILD_FROM

ENV MOPIDY_VERSION='2.2.2-1'
ENV YOUTUBEDL_VERSION='2020.1.24'

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN apt-get update && apt-get -y --no-install-recommends install wget=1.20.1-1.1 gnupg=2.2.12-1+deb10u1 &&\
    wget -q -O - https://apt.mopidy.com/mopidy.gpg | apt-key add - &&\
    debian_codename=$(dpkg --status tzdata | grep Provides | cut -f2 -d'-') &&\
    wget -q -O /etc/apt/sources.list.d/mopidy.list "https://apt.mopidy.com/${debian_codename}.list" &&\
    apt-get update &&\
    apt-get -y --no-install-recommends install \
        mopidy=${MOPIDY_VERSION} \
        jq=1.5+dfsg-2+b1 \
        python-pip=18.1-5 \
        python-setuptools=40.8.0-1 \
        python-wheel=0.32.3-2 \
        gstreamer1.0-alsa=1.14.4-2 \
        gstreamer1.0-plugins-bad=1.14.4-1+b1 \
        sudo=1.8.27-1+deb10u1 &&\
    apt-get -y autoremove && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN pip install youtube-dl=="$YOUTUBEDL_VERSION" certifi==2019.11.28 pafy==0.5.5 Mopidy-Iris==3.42.2 Mopidy-Local-SQLite==1.0.0 
# hadolint ignore=DL3013
RUN pip install https://github.com/natumbri/mopidy-youtube/archive/v2.1.0.zip
#Let mopidy run local scans
RUN echo "mopidy ALL=NOPASSWD: /usr/local/lib/python2.7/dist-packages/mopidy_iris/system.sh" >> /etc/sudoers

COPY mopidy.conf /var/lib/mopidy/.config/mopidy/mopidy.conf

COPY run.sh /
RUN chmod a+x /run.sh

EXPOSE 6600 6680
CMD [ "/run.sh" ]
