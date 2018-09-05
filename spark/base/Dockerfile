FROM bde2020/spark-base:2.1.0-hadoop2.8-hive-java8


ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

RUN apt-get update --fix-missing && apt-get install -y wget bzip2 ca-certificates \
    libglib2.0-0 libxext6 libsm6 libxrender1 \
    git mercurial subversion

RUN wget --quiet https://repo.anaconda.com/archive/Anaconda3-4.2.0-Linux-x86_64.sh -O ~/anaconda.sh && \
    /bin/bash ~/anaconda.sh -b -p /opt/conda && \
    rm ~/anaconda.sh
# && \
#    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh 
#&& \
#    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc
# && \ echo "conda activate base" >> ~/.bashrc

RUN apt-get install -y curl grep sed dpkg && \
    TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` && \
    curl -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" > tini.deb && \
    dpkg -i tini.deb && \
    rm tini.deb && \
    apt-get clean


#Environmentiables for Spark to use Anaconda Python and iPython notebook
RUN ln -s /opt/conda/bin/python /usr/bin/python3
ENV PYSPARK_PYTHON /usr/bin/python3
ENV PYSPARK_DRIVER_PYTHON /usr/bin/python3
ENV PATH /opt/conda/bin/:$PATH

#
## ENV PYSPARK_DRIVER_PYTHON_OPTS "notebook --no-browser --port=8888 --ip='*'"
#
#RUN apt-get update \
#    && apt-get -y install python \
#    && apt-get -y upgrade \
#    && apt-get -y dist-upgrade \
#    && apt-get -y autoremove \
#    && apt-get -y autoclean

ENTRYPOINT [ "/usr/bin/tini", "--" ]
CMD [ "/bin/bash" ]
