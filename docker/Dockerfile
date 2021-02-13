FROM ubuntu:20.04
MAINTAINER CommonTK Community <ctk-developers@commontk.org>
# Build and package the CTK AppLauncher

WORKDIR /usr/src

ARG QT_INSTALL_DIR=/usr/src/qt-everywhere-release-build-5.12.10

ARG DEBIAN_FRONTEND=noninteractive

RUN \
 apt update -y && \
 #
 # Qt dependencies: https://doc.qt.io/archives/qt-4.8/requirements-x11.html
 #
 apt install -y \
   libx11-dev \
   libxt-dev \
   libxext-dev \
   libxrender-dev \
   curl \
   build-essential \
   cmake \
 && \
 #
 # Download Qt sources
 #
 QT_ROOT=qt-everywhere-src-5.12.10 && \
 curl -LO http://mirror.csclub.uwaterloo.ca/qtproject/archive/qt/5.12/5.12.10/single/${QT_ROOT}.tar.xz && \
 echo "a781a0e247400e764c0730b8fb54226f  ${QT_ROOT}.tar.xz" > ${QT_ROOT}.tar.xz.md5 && \
 md5sum -c ${QT_ROOT}.tar.xz.md5 && \
 tar -xvf ${QT_ROOT}.tar.xz && \
 rm -f ${QT_ROOT}.tar.xz && \
 rm -f ${QT_ROOT}.tar.xz.md5 && \
 QT_SRC_DIR=/usr/src/qt-everywhere-opensource-release-src-5.12.10 && \
 mv ${QT_ROOT} ${QT_SRC_DIR} && \
 #
 # Build Qt
 #
 cd /usr/src && \
 mkdir ${QT_INSTALL_DIR} && \
 cd ${QT_SRC_DIR} && \
 LD=${CXX} ./configure \
   -prefix ${QT_INSTALL_DIR} \
   -confirm-license \
   -opensource \
   -static \
   -release \
   -no-accessibility \
   -no-sql-db2 \
   -no-sql-ibase \
   -no-sql-mysql \
   -no-opengl \
   -no-vulkan \
   -no-sql-oci \
   -no-sql-odbc \
   -no-sql-psql \
   -no-sql-sqlite \
   -no-sql-sqlite2 \
   -no-sql-tds \
   -skip xmlpatterns \
   -skip multimedia \
   -skip svg \
   -skip webengine \
   -skip script \
   -skip declarative \
   -no-gif \
   -no-tiff \
   -no-mng \
   -no-openssl \
   -no-cups \
   -no-dbus \
   -no-opengl \
   -no-openvg \
   -nomake examples \
   -nomake tests \
   -nomake tools \
   -no-webp \
   -skip location && \
  make -j$(grep -c processor /proc/cpuinfo) && \
  make install && \
  rm -rf ${QT_SRC_DIR} && \
  rm -rf ${QT_INSTALL_DIR}/q3porting.xml && \
  rm -rf ${QT_INSTALL_DIR}/demos && \
  rm -rf ${QT_INSTALL_DIR}/doc && \
  rm -rf ${QT_INSTALL_DIR}/examples && \
  rm -rf ${QT_INSTALL_DIR}/phrasebooks && \
  rm -rf ${QT_INSTALL_DIR}/tests && \
  rm -rf ${QT_INSTALL_DIR}/translations && \
  #
  # cleanup
  #
  apt clean

# Build-time metadata as defined at http://label-schema.org
ARG BUILD_DATE
ARG IMAGE
ARG VCS_REF
ARG VCS_URL
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name=$IMAGE \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url=$VCS_URL \
      org.label-schema.schema-version="1.0"
