FROM rocker/tidyverse
MAINTAINER Steph Locke <steph@itsalocke.com>

RUN apt-get install libudunits2-0 libudunits2-dev whois nano

# Install TinyTeX (subset of TeXLive)
# From FAQ 5 and 6 here: https://yihui.name/tinytex/faq/
# Also install ae, parskip, and listings packages to build R vignettes

RUN wget -qO- \
    "https://github.com/yihui/tinytex/raw/master/tools/install-unx.sh" | \
    sh -s - --admin --no-path \
    && ~/.TinyTeX/bin/*/tlmgr path add
RUN tlmgr install ae parskip listings beamer \
         translator multirow changepage multirow sttools float dblfloatfix \
         ulem soul subfig footmisc varwidth stix eso-pic \
         algorithms algorithmicx wrapfig tabu colortbl threeparttable \
         threeparttablex environ trimspaces makecell
RUN tlmgr path add
RUN Rscript -e "source('https://install-github.me/yihui/tinytex'); tinytex::r_texmf()"

# This is necessary for non-root users to follow symlinks to /root/.TinyTeX
RUN chmod 755 /root

RUN  R -e 'install.packages(c("huxtable","fractional","bookdown","rticles","rmdshower","kableExtra","printr", \ 
       "rmdTemplates","flextable","officer","shinydashboard","xaringan","openxlsx","eurostat","DT","leaflet"))'
RUN  R -e 'install.packages(c("hflights","nycflights13","sparklyr","RSQLite","stargazer","reticulate"))'
#RUN  R -e 'devtools::install_github("rstudio/radix")'
RUN service rstudio-server stop
RUN  apt-get -y install gdebi-core

#RUN wget https://s3.amazonaws.com/rstudio-ide-build/server/trusty/amd64/rstudio-server-1.2.1000-amd64.deb
#RUN gdebi -n rstudio-server-1.2.1000-amd64.deb
RUN wget https://download2.rstudio.org/server/trusty/amd64/rstudio-server-1.2.5001-amd64.deb
RUN gdebi rstudio-server-1.2.5001-amd64.deb

RUN service rstudio-server start

RUN apt-get update && apt-get -y install \
     procps libpython-dev libpython3-dev \ 
     python-virtualenv \
     python-pip && \
     pip install h5py pyyaml requests Pillow scipy tensorflow-gpu keras  && \
     install2.r --error keras 

RUN  R -e 'update.packages(ask = FALSE)'

#RUN rm -rf rstudio-server-1.2.1000-amd64.deb
RUN rm -rf rstudio-server-1.2.5001-amd64.deb

RUN tlmgr install fancyhdr microtype psnfss setspace titlesec placeins palatino mathpazo

EXPOSE 8787

# CMD ["/usr/lib/rstudio-server/bin/rserver", "--server-daemonize=0"]
