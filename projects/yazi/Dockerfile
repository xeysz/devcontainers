FROM docker.io/library/fedora:latest

# Parameters for user configuration
ARG USERNAME=devuser
ARG UID=1000
ARG GID=1000

# Global system config
RUN dnf update -y && \
    dnf install -y \
    @development-tools \
    git \
    rust \
    cargo \
    fish \
    && dnf clean all

RUN groupadd -g $GID $USERNAME && \
    useradd -m -u $UID -g $GID -s /usr/bin/fish $USERNAME

# User configuration
USER $USERNAME
RUN cargo install --locked --bin jj jj-cli
ENV PATH="/home/$USERNAME/.cargo/bin:${PATH}"

# Workspace setup
RUN jj git clone --colocate https://github.com/xeysz/yazi /home/$USERNAME/workspaces/yazi-dev
WORKDIR /home/$USERNAME/workspaces/yazi-dev

CMD ["/usr/bin/fish"]
