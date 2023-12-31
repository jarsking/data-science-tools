# syntax=docker/dockerfile:1


# Set the base image using miniconda
FROM  continuumio/miniconda3:4.12.0


# Set working directory
WORKDIR /app

RUN mkdir /opt/oracle

COPY instantclient-basic-linux.x64-11.2.0.4.0.zip /opt/oracle/instantclient-basic-linux.x64-11.2.0.4.0.zip

# Clean and update
RUN apt-get update -y \
    && apt-get clean -y \
    && apt-get update -y

RUN apt-get install -y  unzip libaio1 build-essential  python-dev \
    && cd /opt/oracle/ \
    && unzip  instantclient-basic-linux.x64-11.2.0.4.0.zip \
    && cd /opt/oracle/instantclient_11_2 \
    && ln -s libclntsh.so.11.1 libclntsh.so \
    && ln -s libocci.so.11.1 libocci.so \
    && echo /opt/oracle/instantclient_11_2 > /etc/ld.so.conf.d/oracle-instantclient.conf \
    && ldconfig 

ENV LD_LIBRARY_PATH /opt/oracle/instantclient_11_2 
ENV PATH /opt/oracle/instantclient_11_2:$PATH
ENV PATH /opt/conda/bin:$PATH



    # install python lib
RUN conda install pip  \
    # basic lib
    && pip install cx_oracle python-docx pymysql pyhive pyspark
    # eda lib
RUN pip install minepy numpy   pandas dask pandarallel   toad  matplotlib seaborn scipy statsmodels fitter datetime pyecharts  -i https://pypi.tuna.tsinghua.edu.cn/simple  
    # ML DL 
RUN pip install  scikit-learn  -i https://pypi.tuna.tsinghua.edu.cn/simple \
    && pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu

          
RUN pip install jupyter 
 # jupyter notebook --notebook-dir=/app/notebooks --ip='*' --port=8888 --no-browser  --allow-root --NotebookApp.password='sha1:bf8f89981095:2b0b242b19e52b88e9b9f512924d6753cb67325d'
 # password abc123%
