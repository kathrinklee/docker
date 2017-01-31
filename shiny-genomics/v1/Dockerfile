############################################################ 
# Dockerfile to build container with shiny server to run
# genomics analysis suite
# Based on r-base 
############################################################ 

FROM r-base:latest 

# File Author / Maintainer
MAINTAINER Kathrin Klee <klee@uni-bonn.de>

# Update the repository sources list and install libs
RUN apt-get update && apt-get install -y -t unstable \
    sudo \
    gdebi-core \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev/unstable \
    libxt-dev

# Download and install shiny server with required R packages
RUN wget --no-verbose https://s3.amazonaws.com/rstudio-shiny-server-os-build/ubuntu-12.04/x86_64/VERSION -O "version.txt" && \
    VERSION=$(cat version.txt)  && \
    wget --no-verbose "https://s3.amazonaws.com/rstudio-shiny-server-os-build/ubuntu-12.04/x86_64/shiny-server-$VERSION-amd64.deb" -O ss-latest.deb && \
    gdebi -n ss-latest.deb && \
    rm -f version.txt ss-latest.deb && \
    R -e "install.packages(c('shiny','shinyjs','shinyBS','rmarkdown','RColorBrewer','stringr','formula.tools','yarrr','data.table','fdrtool','VennDiagram','colorspace','gplots','webshot'), dependencies = TRUE, repos='https://cran.rstudio.com/')" && \
    R -e "library(c('shiny','shinyjs','shinyBS','rmarkdown','RColorBrewer','stringr','formula.tools','yarrr','data.table','fdrtool','VennDiagram','colorspace','gplots','webshot'))" && \
    R -e "source('https://bioconductor.org/biocLite.R')" && \
    R -e "biocLite(c('DESeq2','clusterProfiler','org.Mm.eg.db','org.Dm.eg.db','sva','limma','geneplotter','biomaRt'))" && \
    R -e "library(c('DESeq2','clusterProfiler','org.Mm.eg.db','org.Dm.eg.db','sva','limma','geneplotter','biomaRt'))" && \
    R -e "devtools::install_github(c('ropensci/plotly','rstudio/crosstalk'), force = TRUE)" && \
    R -e "library(c('plotly','crosstalk'))" && \
    cp -R /usr/local/lib/R/site-library/shiny/examples/* /srv/shiny-server/ && \
    chown -R shiny:shiny /srv/shiny-server/

EXPOSE 3838 COPY shiny-server.sh /usr/bin/shiny-server.sh

CMD ["/usr/bin/shiny-server.sh"]
