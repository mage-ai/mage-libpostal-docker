FROM mageai/mageai:latest

ENV DEBIAN_FRONTEND noninteractive
ENV LIBPOSTAL_VERSION   v1.0.0
ENV LIBPOSTAL_DIR       /opt/libpostal
ENV LIBPOSTAL_DATA_DIR  /opt/libpostal_data

########################################
# libpostal
########################################
# RUN echo "deb http://cz.archive.ubuntu.com/ubuntu trusty main" > /etc/apt/sources.list

RUN apt-get update && apt-get -qq update && apt-get install -y --force-yes \
  libsnappy-dev \
  autoconf \
  automake \
  libtool \
  pkg-config \
  git

RUN wget https://github.com/openvenues/libpostal/archive/$LIBPOSTAL_VERSION.tar.gz
RUN mkdir -p $LIBPOSTAL_DIR
RUN tar -xvzf $LIBPOSTAL_VERSION.tar.gz -C $LIBPOSTAL_DIR --strip 1
WORKDIR $LIBPOSTAL_DIR
COPY ./build_libpostal.sh .

USER root 
RUN chmod 755 ./build_libpostal.sh

RUN ./build_libpostal.sh
#############

WORKDIR ${USER_CODE_PATH}

COPY requirements.txt requirements.txt
RUN pip install --upgrade pip && pip install -r requirements.txt