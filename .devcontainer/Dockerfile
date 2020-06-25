FROM continuumio/miniconda3

# specifiy the version of the runtime of the target databricks cluster, must match the version of databricks-connect
ARG DB_CLUSTER_VERSION=6.5

# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

USER root

# Configure apt and install packages
RUN apt-get update \
    && apt-get -y install --no-install-recommends apt-utils dialog 2>&1 \
    #
    # Verify git, process tools, lsb-release (common in install instructions for CLIs) installed
    && apt-get -y install git iproute2 procps iproute2 lsb-release \
    #
    # Clean up
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Switch back to dialog for any ad-hoc use of apt-get
ENV DEBIAN_FRONTEND=dialog

# Conda and local install
COPY env.yml /tmp/conda-temp/env.yml
RUN conda update conda -y \
        && conda env update -n base -f "/tmp/conda-temp/env.yml" \
        && rm -rf /tmp/conda-temp


# Install Java 8 on Debian 10 - not as simple as I thought

# https://github.com/debuerreotype/docker-debian-artifacts/issues/24#issuecomment-360870939
RUN mkdir -p /usr/share/man/man1

# https://stackoverflow.com/a/59436618/6067848
RUN apt-get update -y \
        && apt-get install -y gnupg software-properties-common \
        && wget -qO - https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public | apt-key add - \
        && add-apt-repository --yes https://adoptopenjdk.jfrog.io/adoptopenjdk/deb/ \
        && apt-get update \
        && apt-get install adoptopenjdk-8-hotspot -y

# Install databricks-connect
RUN pip install -U databricks-connect==$DB_CLUSTER_VERSION.*
