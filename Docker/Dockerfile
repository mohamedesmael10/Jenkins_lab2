FROM ubuntu:22.04

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        vim \
    && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

CMD ["bash"]

