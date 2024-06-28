FROM python:3.10-slim

# Keep some tools inside the container for debugging
RUN apt update -y && apt install build-essential wget git vim tmux -y

RUN echo "Running install dependencies"

RUN apt-get -y install musl-dev wget git gcc make cmake
# Installation of TA-Lib
RUN wget http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-src.tar.gz && \
  tar -xvzf ta-lib-0.4.0-src.tar.gz && \
  cd ta-lib/ && \
  ./configure --prefix=/usr --build=arm-linux && \
  make && \
  make install

# install finlab
RUN pip install jupyterlab
RUN pip install ipywidgets
RUN pip install yfinance
RUN pip install ffn
RUN pip install ta-lib

RUN apt install libopenblas-dev -y
RUN pip install PyPortfolioOpt

COPY . /workspace
WORKDIR /workspace

RUN pip install -r requirements.txt

EXPOSE 8888
RUN mkdir -p /opt/app/data
CMD jupyter lab --ip=* --port=8888 --no-browser --allow-root
