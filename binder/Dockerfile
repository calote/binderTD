FROM rocker/binder:3.6.0

USER root

RUN apt-get update \
&& apt-get install -y \
libudunits2-dev \
libqpdf-dev \
libnetcdf-dev \
libmagick++-dev
&& apt-get clean

COPY . ${HOME}
RUN chown -R ${NB_USER} ${HOME}

## Become normal user again
USER ${NB_USER}

#RUN R -e "packrat::restore()"

#RUN R -e "source('.Rprofile'); install.packages('tinytex'); tinytex::install_tinytex()"



RUN R -e "install.packages('tidyverse')"
RUN R -e "install.packages('rmarkdown')"
RUN R -e "install.packages('httr')"
RUN R -e "install.packages('shinydashboard')"
RUN R -e "install.packages(c('leaflet','flexdashboard'))"
RUN R -e "install.packages(c('kableExtra','huxtable','xtable','gt','texreg','flextable','rhandsontable'))"

RUN R -e "install.packages(c('rio','fBasics','skimr'))"

RUN R -e "install.packages(c('fractional','bookdown','rticles','printr','officer','xaringan','openxlsx','eurostat','DT'))"

RUN R -e "install.packages(c('hflights','nycflights13','sparklyr','RSQLite','stargazer','reticulate'))"

RUN R -e "install.packages(c('Rglpk','lpSolve'))"

RUN R -e "install.packages('devtools')"

RUN R -e "install.packages(c('caTools','bitops'))"

RUN R -e "tinytex::install_tinytex()"

RUN R -e "devtools::install_github('rapporter/pander')"

RUN R -e "remotes::install_github('dcomtois/summarytools',dependencies=TRUE,force=TRUE)"

