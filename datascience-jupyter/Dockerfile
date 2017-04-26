# Base image
FROM ubuntu:16.04

# Put my hand up as maintainer
MAINTAINER chishui<chishui2@gmail.com>

# Suppress debian frontend warnings from Ubuntu base image
RUN DEBIAN_FRONTEND=noninteractive

USER root

# Install OS tools we'll need
RUN \
    apt-get update && \
    apt-get -y install \
        git \
        # Python libraries
        python \
        python-pip 

RUN pip install --upgrade pip
RUN pip install --no-cache-dir numpy scipy pandas matplotlib sympy jupyter

# variables
ENV USER_NAME chishui
ENV DIR run

# add user
RUN useradd -m -s /bin/bash -N -u 1000 $USER_NAME

USER $USER_NAME

RUN mkdir /home/$USER_NAME/.jupyter
RUN mkdir /home/$USER_NAME/$DIR
COPY .jupyter/jupyter_notebook_config.py /home/$USER_NAME/.jupyter
COPY .jupyter/mycert.pem /home/$USER_NAME

RUN git clone https://github.com/chishui/fortaoli.git /home/$USER_NAME/fortaoli
RUN cp /home/$USER_NAME/fortaoli/taoli.ipynb /home/$USER_NAME/$RUN


# Configure container startup
ENTRYPOINT ["jupyter", "notebook"]
CMD ["--allow-root"]
