FROM ethereum/client-go

RUN apk update &&\
    apk add git nodejs bash perl build-base cmake boost-dev sed &&\
	sed -i -E -e 's/include <sys\/poll.h>/include <poll.h>/' /usr/include/boost/asio/detail/socket_types.hpp  && \
	git clone --depth 1 --recursive -b release https://github.com/ethereum/solidity                           && \
	cd /solidity && cmake -DCMAKE_BUILD_TYPE=Release -DTESTS=0 -DSTATIC_LINKING=1                             && \
	cd /solidity && make solc && install -s  solc/solc /usr/bin                                               && \
	cd / && rm -rf solidity                                                                                   && \
	apk del sed build-base git make cmake gcc g++ musl-dev curl-dev boost-dev                                 && \
	rm -rf /var/cache/apk/*

ADD start.sh /root/start.sh
RUN chmod +x /root/start.sh

ENTRYPOINT /root/start.sh
