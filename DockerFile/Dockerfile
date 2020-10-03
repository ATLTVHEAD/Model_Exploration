#define base container
ARG BASE_CONTAINER=jupyter/scipy-notebook:36d857bb0121
FROM $BASE_CONTAINER
#create some metadata for the image
LABEL maintainer = "Nate Damen <nate.damen@gmail.com>" \
      version="0.1" \
      description = " Notebooks and data for creating tensorflow practice models"

#make a working directory
WORKDIR /app

COPY . /app

#mount point
VOLUME /app/data

#expose the port
EXPOSE 8888

USER root
RUN apt-get update && apt-get -qq install xxd

#install tensorflow 2.2
RUN pip install --quiet --no-cache-dir \
    'tensorflow==2.3.1' && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

RUN pip install -r requirements.txt

RUN jupyter contrib nbextension install --user

RUN jupyter nbextensions_configurator enable --user



#run notebook upon container launch
CMD ["jupyter","notebook","--ip='*'","--port=8888","--no-browser","--allow-root","--password=password"]

#to build the docker file, cd to the appropriate directory and copy past the following into the terminal: "docker build -t atltvhead/tensorflow_practice ."
#to run the this docker file use the following:  docker run -e PASSWORD=password -p 8888:8888 -v "C:/Users/nated/Documents/Python Scripts/Data Science Questions/Book Problems:/app/data" --name practice atltvhead/tensorflow_practice:latest
#to find out what the token is use the following docker exec practice jupyter notebook list
#when restarting the docker container use http://127.0.0.1:8888/tree? to go to the notebook
#when needing to add software or access the sudo command line for the docker use the following command in a windows cmd: docker exec -it -u root bracer bash