FROM debian:latest

ENV PORT=54321

RUN DEPENDS="xinetd tcpd curl ca-certificates unzip build-essential" && \
    apt-get update && \
    apt-get -y install --no-install-recommends $DEPENDS && \
    apt-get clean

RUN set -e -x && \
    curl -L https://github.com/official-stockfish/Stockfish/archive/master.zip -o master.zip && \
    unzip master.zip && \
    rm master.zip && \
    cd Stockfish-master/src/ && \
    make -j build ARCH=x86-64-modern && \
    make install && \
    make clean && \
    apt-get purge -y --autoremove $DEPENDS && \ 
    rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/*

COPY stockfish.conf /etc/xinetd.d/stockfish

RUN useradd -m netuser && \
    sed -i "s/54321/$PORT/g" /etc/xinetd.d/stockfish

EXPOSE $PORT

CMD ["xinetd", "-dontfork"]
