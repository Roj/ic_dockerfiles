## Dockerfile for RStudio server

Based on https://hub.docker.com/r/rocker/rstudio/dockerfile 

This dockerfile installs packages listed in `r_requirements.txt`
and sets up two volumes for data and temporary libraries.

The directory structure that you will end up seeing in RStudio
should be:
```
/home/rstudio
	data/
		# volume linked to ./data of host (at current directory)
	libs/
		base/
			# libraries installed during build (i.e. in r_requirements.txt)
		extra/
			# libraries installed while container is running via install.packages
			# volume linked to ./libs of host at CWD
	
``` 

Since there is no persistence for the container's disk, `libs/extra` serves
as a place to store libraries you may want to install and persist across
runs. Just remember to specify the directory when you do `install.packages`.


### Building

```sh
$ mkdir -p data libs
$ make build # sudo may be necessary
```

### Running

Before running, be sure to configure your password in the Makefile.

If you are running this Dockerfile on your local machine, you might
want to comment out the proxy settings.

```sh
$ make run # sudo may be necessary
```
