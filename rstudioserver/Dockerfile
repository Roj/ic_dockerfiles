FROM rocker/rstudio

# Proxy configuration
#ENV http_proxy http://proxy.fcen.uba.ar:8080
#ENV https_proxy http://proxy.fcen.uba.ar:8080

RUN mkdir -p /home/rstudio/libs/base

# Install libraries
ADD r_requirements.txt r_requirements.txt
RUN awk '{print "install.packages(\""$1"\", dependencies=TRUE, lib=\"/home/rstudio/libs/base\")"}' r_requirements.txt > commands.txt
RUN Rscript commands.txt

# Add library locations to libPaths, so library() can find them
RUN echo '.libPaths( c( .libPaths(), "/home/rstudio/libs/base", "/home/rstudio/libs/extra") )' > /home/rstudio/.Rprofile
