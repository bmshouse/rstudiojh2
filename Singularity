Bootstrap:docker
From:jupyter/r-notebook:29e069665f5f

%files

%post

apt-get update -y \
    && apt-get upgrade -y --no-install-recommends \
    && apt-get install -y --no-install-recommends default-jdk default-jre libcairo2-dev libpq-dev r-cran-rcpp \
    && curl --silent -L --fail https://download2.rstudio.org/server/bionic/amd64/rstudio-server-1.2.5033-amd64.deb > /tmp/rstudio.deb \
    && apt-get install -y --no-install-recommends /tmp/rstudio.deb \
    && rm /tmp/rstudio.deb \
    && apt-get clean

PATH=$PATH:/usr/lib/rstudio-server/bin

conda install --yes --quiet -c conda-forge nbgitpuller nbrsessionproxy jupyter-rsession-proxy openjdk r-webp gdal tesseract leptonica \
    && jupyter serverextension enable --py nbgitpuller --sys-prefix \
    && conda clean --all --yes \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/*


JAVA_HOME=/opt/conda/pkgs/openjdk-11.0.1-h600c080_1018
PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/opt/conda/lib/pkgconfig
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$JAVA_HOME/lib/server/

R --vanilla CMD javareconf
R --vanilla -e "install.packages('rJava',dependencies=TRUE, repos='http://cran.rstudio.com/')"
R --vanilla -e "install.packages('gutenbergr',dependencies=TRUE, repos='http://cran.rstudio.com/')"
R --vanilla -e "install.packages('RcppParallel',dependencies=TRUE, repos='http://cran.rstudio.com/')"
R --vanilla -e "install.packages('tidytext',dependencies=TRUE, repos='http://cran.rstudio.com/')"
R --vanilla -e "install.packages('dplyr',dependencies=TRUE, repos='http://cran.rstudio.com/')"
R --vanilla -e "install.packages('textdata',dependencies=TRUE, repos='http://cran.rstudio.com/')"
R --vanilla -e "install.packages('widyr',dependencies=TRUE, repos='http://cran.rstudio.com/')"
R --vanilla -e "install.packages('pdftools',dependencies=TRUE, repos='http://cran.rstudio.com/')"

%environment

#permanent: 

export PATH=$PATH:/usr/lib/rstudio/bin:/usr/lib/rstudio-server/bin
JAVA_HOME=/opt/conda/pkgs/openjdk-11.0.1-h600c080_1018
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$JAVA_HOME/lib/server/
PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/opt/conda/lib/pkgconfig
