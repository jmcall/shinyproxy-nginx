FROM openanalytics/r-base

MAINTAINER John McAllister "john@john-mcallister.com"

# system libraries of general use
RUN apt-get update && apt-get install -y \
    sudo \
    pandoc \
    pandoc-citeproc \
    libcurl4-openssl-dev \
    libcairo2-dev \
    libxt-dev \
    libssl-dev \
    libssh2-1-dev \
    libssl1.1 \
    libxml2-dev \
    openssl \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# system library dependency
RUN apt-get update && apt-get install -y \
    libmpfr-dev \
    && rm -rf /var/lib/apt/lists/*

# basic shiny functionality
RUN R -e "install.packages(c('shinydashboard','shinyWidgets', 'rmarkdown','xml2'), repos='https://cloud.r-project.org/')"

# install dependencies of the turnarounds app
RUN R -e "install.packages(c('tidyverse','lubridate','dplyr','stringr','highcharter','DT','fst'), repos='https://cloud.r-project.org/')"

# copy the app to the image
RUN mkdir /root/app
COPY app /root/app

COPY Rprofile.site /usr/lib/R/etc/

RUN mkdir /root/data

EXPOSE 3838

CMD ["R", "-e", "shiny::runApp('root/app')"]
