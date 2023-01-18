# [Choice] Java version (use -bullseye variants on local arm64/Apple Silicon): 11, 17, 11-bullseye, 17-bullseye, 11-buster, 17-buster
ARG VARIANT=17
FROM mcr.microsoft.com/devcontainers/java:${VARIANT}

# [Optional] Clojure version
ARG CLOJURE_VERSION=1.11.1

# [Optional] Clojure tools version
ARG CLOJURE_CLI_VERSION=1.11.1.1208


# [Option] Install Clojure CLI tool
ARG INSTALL_CLOJURE_CLI="true"

RUN if [ "${INSTALL_CLOJURE_CLI}" = "true" ]; then \
    apt-get update \
    && apt-get -y install rlwrap \
    && curl -OL "https://download.clojure.org/install/linux-install-${CLOJURE_CLI_VERSION}.sh" \
    && chmod +x linux-install-${CLOJURE_CLI_VERSION}.sh \
    && /linux-install-${CLOJURE_CLI_VERSION}.sh \
    && rm /linux-install-${CLOJURE_CLI_VERSION}.sh \
    && su vscode -c "clj --version"; fi

# install additional OS packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
     && apt-get -y install --no-install-recommends python3-pip python3-venv libpython3.9 r-base


# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1
# Clean up package lists
RUN apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*
RUN bash -c "bash < <(curl -s https://raw.githubusercontent.com/babashka/babashka/master/install)"

RUN pip install numpy
RUN Rscript -e 'install.packages("tidyverse")'

USER vscode

