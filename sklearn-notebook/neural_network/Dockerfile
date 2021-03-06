# Usage:
# docker build -t andaag/sklearn-notebook-neural .
# mkdir ml
# docker run -v $(pwd)/ml:/ml -t andaag/sklearn-notebook-neural

FROM ubuntu:14.04
RUN sed 's:/archive\.:/no.archive.:g' /etc/apt/sources.list -i
RUN apt-get update
RUN apt-get upgrade -y

RUN mkdir /ml
RUN locale-gen en_US en_US.UTF-8
RUN apt-get -y install python-scikits-learn python-pandas cython python-pip python-mechanize python-matplotlib python-numexpr
RUN apt-get -y install libzmq3-dev libzmq3 git-core
RUN pip install --upgrade ipython[all]
RUN pip install bottleneck
RUN pip install seaborn
RUN pip install --upgrade git+git://github.com/IssamLaradji/scikit-learn.git@generic-multi-layer-perceptron
RUN chmod 755 /ml

#Minimize image size
RUN (apt-get remove -y --purge libzmq-dev python-dev libc-dev libzmq3-dev git-core; \
     apt-get remove -y --purge gcc cpp binutils build-essential; \
     apt-get autoremove -y; \
     apt-get clean -y)
RUN apt-get remove -y python-scikits-learn python-sklearn python-sklearn-lib

WORKDIR /ml

EXPOSE 8888
CMD ipython notebook --no-browser --ip=$(hostname -i) --port 8888
