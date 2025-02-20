FROM mambaorg/micromamba:1.5.1

COPY checkm2.yml /tmp/checkm2.yml

USER root
RUN apt-get update && apt-get install -y git

USER $MAMBA_USER
RUN micromamba create -n checkm2 -f /tmp/checkm2.yml && \
    micromamba clean --all --yes

# Make RUN commands use the new environment:
SHELL ["micromamba", "run", "-n", "checkm2", "/bin/bash", "-c"]

RUN git clone --recursive https://github.com/chklovski/checkm2.git && \
    cd checkm2 && \
    python setup.py install

# The code to run when container is started:
ENTRYPOINT ["micromamba", "run", "-n", "checkm2", "checkm2"]