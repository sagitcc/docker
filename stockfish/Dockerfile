FROM debian:latest

RUN set -e -x && \
    DEPENDS="curl ca-certificates unzip build-essential" && \
    apt-get update && \
    apt-get -y install --no-install-recommends xinetd tcpd $DEPENDS && \
    apt-get clean && \
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

RUN useradd -m netuser

EXPOSE 54321/tcp

CMD ["xinetd", "-dontfork"]
