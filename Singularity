Bootstrap:docker
From:jupyter/r-notebook:f200ab964cea

%files

%post

export PATH=/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/lib/rstudio/bin:/usr/lib/rstudio-server/bin

apt-get update -y
apt-get upgrade -y --no-install-recommends
apt-get install -y --no-install-recommends default-jdk default-jre libcairo2-dev libpq-dev r-cran-rcpp


conda install --yes --quiet -c conda-forge nbgitpuller nbrsessionproxy jupyter-rsession-proxy openjdk r-webp gdal tesseract leptonica
jupyter serverextension enable --py nbgitpuller --sys-prefix

cd  /opt
wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-1.2.5033-amd64.deb
apt-get install -y --no-install-recommends /opt/rstudio-server-1.2.5033-amd64.deb
rm /opt/*.deb

PATH=$PATH:/usr/lib/rstudio-server/bin
JAVA_HOME=/opt/conda/pkgs/openjdk-11.0.1-h600c080_1018
PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/opt/conda/lib/pkgconfig
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$JAVA_HOME/lib/server/

R --vanilla CMD javareconf

%environment

export PATH=/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/lib/rstudio/bin:/usr/lib/rstudio-server/bin
export JAVA_HOME=/opt/conda/pkgs/openjdk-11.0.1-h600c080_1018
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$JAVA_HOME/lib/server/
export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/opt/conda/lib/pkgconfig
