FROM rocker/rstudio

# Proxy configuration
ENV http_proxy http://proxy.fcen.uba.ar:8080
ENV https_proxy http://proxy.fcen.uba.ar:8080

# Install java
RUN apt-get update && apt-get install -y openjdk-8-jdk-headless

RUN mkdir -p /home/rstudio/libs/base

# Install libraries
ADD r_requirements.txt r_requirements.txt
RUN awk '{print "install.packages(\""$1"\", dependencies=TRUE, lib=\"/home/rstudio/libs/base\")"}' r_requirements.txt > commands.txt
RUN Rscript commands.txt

# Add library locations to libPaths, so library() can find them
RUN echo ".libPaths( c( .libPaths(), \"/home/rstudio/libs/base\", \"/home/rstudio/libs/extra\") )" >> /home/rstudio/.Rprofile \
	&& echo "Sys.setenv(http_proxy=\"http://proxy.fcen.uba.ar:8080\", https_proxy=\"http://proxy.fcen.uba.ar:8080\")" >> /home/rstudio/.Rprofile

RUN java -version
