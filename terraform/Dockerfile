# Variáveis que serão utilizadas dentro do Dockerfile
ARG VERSION=1.9
ARG KEYNAME=pipeline
ARG SSH_DIR=/root/.ssh

FROM hashicorp/terraform:$VERSION

# Re-declarar os ARGs após o FROM para usá-los no RUN
ARG KEYNAME
ARG SSH_DIR

RUN mkdir -p $SSH_DIR && \
    ssh-keygen -t ed25519 -f $SSH_DIR/$KEYNAME -C "docker used for pipelines" -N "" && \
    chmod 700 $SSH_DIR && \
    chmod 600 $SSH_DIR/$KEYNAME && \
    ssh-keyscan gitlab.com >> $SSH_DIR/known_hosts && \
    cat $SSH_DIR/pipeline.pub