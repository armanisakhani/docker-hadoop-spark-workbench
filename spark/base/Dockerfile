FROM bde2020/spark-base:2.1.0-hadoop2.8-hive-java8

#Install Anaconda
WORKDIR /
RUN curl https://repo.anaconda.com/archive/Anaconda3-4.2.0-Linux-x86_64.sh -o anaconda.sh
RUN chmod a+x anaconda.sh
RUN mv anaconda.sh /opt/anaconda.sh
RUN apt-get update & apt-get install bzip2
RUN ./opt/anaconda.sh -b
RUN /root/anaconda3/bin/conda install -y -q ipython notebook

#Environment vaiables for Spark to use Anaconda Python and iPython notebook
ENV PYSPARK_PYTHON /root/anaconda3/bin/python3
ENV PYSPARK_DRIVER_PYTHON /root/anaconda3/bin/ipython3
RUN export PATH=$PATH:/root/anaconda3/bin/

# ENV PYSPARK_DRIVER_PYTHON_OPTS "notebook --no-browser --port=8888 --ip='*'"

RUN apt-get update \
    && apt-get -y install python \
    && apt-get -y upgrade \
    && apt-get -y dist-upgrade \
    && apt-get -y autoremove \
    && apt-get -y autoclean

ENTRYPOINT ["entrypoint.sh"]