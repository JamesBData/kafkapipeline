FROM confluentinc/cp-kafka:latest

# set user to root to allow for package installation
USER root


# install updates
RUN yum update -y
RUN yum install gcc openssl-devel bzip2-devel libffi-devel zlib-devel libxml2-devel libxslt-devel -y

# add requirements.txt file
WORKDIR /code
COPY ./requirements.txt /code/requirements.txt

# add files to directory
COPY . /code/

# install pip and install librarires
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py --force-reinstall
RUN python -m pip install --upgrade pip
#RUN yum install python3-devel -y
RUN python -m pip install --no-cache-dir --upgrade -r /code/requirements.txt
RUN pyxbgen --schema-root=ppv16 --module PPv16 rttiPPTSchema_v16.xsd

# run main.py using python
CMD ["python", "opendata-nationalrail-client.py"] 
