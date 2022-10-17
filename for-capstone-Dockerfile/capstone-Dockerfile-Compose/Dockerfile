FROM alpine
ARG VERSION=1
#ADD https://github.com/james-clarusway/version-1/raw/main/version.tar /version.tar
#ADD https://github.com/james-clarusway/version-2/raw/main/version.tar /version.tar
ADD https://github.com/james-clarusway/version-${VERSION}/raw/main/version.tar version.tar
ENV KEY=value
# ENV newenvar=itisnew
RUN tar -xvf version.tar
CMD cat /version/version


# https://github.com/james-clarusway/version-1.git

