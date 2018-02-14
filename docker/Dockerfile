FROM ubuntu:16.04

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

RUN              apt-get update --fix-missing \
    && apt-get install -y wget bzip2 ca-certificates \
    libglib2.0-0 libxext6 libsm6 libxrender1 libtool libffi-dev ruby ruby-dev make \
    libzmq3-dev autoconf pkg-config git mercurial subversion curl grep sed dpkg\
    software-properties-common python-software-properties \
    && add-apt-repository ppa:gophers/archive \
    && apt update \
    && apt-get install -y golang-1.9-go


RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/archive/Anaconda2-5.0.1-Linux-x86_64.sh -O ~/anaconda.sh && \
    /bin/bash ~/anaconda.sh -b -p /opt/conda && \
    rm ~/anaconda.sh

RUN TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` && \
    curl -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" > tini.deb && \
    dpkg -i tini.deb && \
    rm tini.deb && \
    apt-get clean

ENV PATH /opt/conda/bin:/usr/lib/go-1.9/bin:$PATH

RUN /opt/conda/bin/conda install jupyter -y --quiet \
    && mkdir /opt/notebooks

ENV PATH /opt/conda/bin:/usr/lib/go-1.9/bin:$GOPATH/bin:$PATH

RUN git clone https://github.com/zeromq/czmq \
    && cd czmq \
    && ./autogen.sh \
    && ./configure \
    && make \
    && make install

RUN gem install cztop iruby \
    && iruby register --force

RUN conda install -c conda-forge nodejs
RUN npm install ijavascript
ENV PATH $PATH:$HOME/node_modules/.bin
RUN ijsinstall


RUN go get github.com/fabian-z/gopherlab \
    && mkdir -p ~/.local/share/jupyter/kernels/gopherlab \
    && cp -r ~/go/src/github.com/fabian-z/gopherlab/kernel/* ~/.local/share/jupyter/kernels/gopherlab/ \
    && cp -a ~/go/bin/gopherlab ~/.local/share/jupyter/kernels/gopherlab/ \
    &&  sed -i "s#/go/bin/gopherlab#$HOME/.local/share/jupyter/kernels/gopherlab/gopherlab#g" $HOME/.local/share/jupyter/kernels/gopherlab/kernel.json

RUN /opt/conda/bin/pip install bash_kernel \
    && /opt/conda/bin/python -m bash_kernel.install

RUN apt-get clean

EXPOSE 8888

ENTRYPOINT [ "/opt/conda/bin/jupyter" ]
CMD [ "notebook",  "--notebook-dir=/opt/notebooks", "--ip='*'", "--port=8888", "--no-browser", "--allow-root"]
