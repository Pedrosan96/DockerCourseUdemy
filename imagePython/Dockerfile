FROM ubuntu
RUN apt-get update
RUN apt-get install -y python
RUN echo 1.0 >> /etc/version && apt-get install -y git \
    && apt-get install -y iputils-ping

##WORKDIR##
RUN mkdir /datos
WORKDIR /datos
RUN touch f1.txt
RUN mkdir /datos1
WORKDIR /datos1
RUN touch f2.txt

##COPY## copia los archivos indicados al directorio WORKDIR (.)
COPY index.html .
COPY app.log /datos

##ADD## La diferencia con COPY es que puede copiar ficheros .tar o de un url
#crea el directorio docs a partir de /datos1 (WORKDIR)
ADD docs docs 
ADD f* /datos/
ADD f.tar . 
 ##Descomprime el f.tar (archivo que no he creado pero deberia existir)

##ENV##
ENV dir=/data dir1=/data1
RUN mkdir $dir && mkdir $dir1

##ARG## A diferencia de ENV, permite crear el espacio al construir la imagen 
ARG dir2	
##Ej. docker build -t image:v6 --build-arg dir2=/data2 .
RUN mkdir $dir2 
ARG user
ENV user_docker $user
ADD add_user.sh /datos1
RUN /datos1/add_user.sh
#Nuevo usuario creado desde script add_user.sh
##Ej. docker build -t image:v6 --build-arg dir2=/datos2 --build-arg user=tom .

##ENTRYPOINT##
ENTRYPOINT ["/bin/bash"]


