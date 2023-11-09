FROM debian:stretch-slim
LABEL Maintainer="Matthew Pearce <mattpearce85@gmail.com>"
RUN sed -i -e 's/deb.debian.org/archive.debian.org/g' \
    -e 's|security.debian.org|archive.debian.org/|g' \
    -e '/stretch-updates/d' /etc/apt/sources.list && \
apt-get update && \
apt-get install -y \
perl \
fcgiwrap \
build-essential \
default-libmysqlclient-dev \
libimage-magick-perl \
libexpat1-dev \
perl-openssl-defaults \
openssl \
libssl-dev \
--no-install-recommends && \
rm -r /var/lib/apt/lists/*
RUN cpan -i MIME::Lite
RUN cpan -i Net::Telnet
RUN cpan -i Crypt::CBC
RUN cpan -i DateTime
RUN cpan -i DBI
RUN cpan -i DBD::MariaDB
RUN cpan -i CGI
RUN cpan -i Archive::Zip
RUN cpan -i LWP
RUN cpan -i XML::Simple
RUN cpan -i Lingua::EN::Numbers
RUN cpan -i JSON
RUN cpan -i Crypt::JWT
RUN cpan -i Net::SSLeay
RUN cpan -i CAM::PDF
RUN cpan -i XML::Writer
ENTRYPOINT [ "fcgiwrap", "-s", "tcp:0.0.0.0:9000", "-f" ]
EXPOSE 9000
