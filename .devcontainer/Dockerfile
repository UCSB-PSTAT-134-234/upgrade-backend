# R + Python + Julia kernels
# FROM jupyter/datascience-notebook:x86_64-2023-03-06
FROM jupyter/scipy-notebook:x86_64-2023-03-06
# FROM jupyter/r-notebook:x86_64-2023-03-06

USER root

### System dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        lmodern file curl && \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/* /tmp/library-scripts

### Quarto
# versions: https://quarto.org/docs/download/_download.json
# neat setup: https://github.com/jeremiahpslewis/reproducibility-with-quarto
RUN curl --silent -L --fail \
        https://github.com/quarto-dev/quarto-cli/releases/download/v1.2.269/quarto-1.2.269-linux-amd64.deb > /tmp/quarto.deb && \
    apt-get update && \
    apt-get install -y --no-install-recommends /tmp/quarto.deb && \
    rm -rf /tmp/quarto.deb /var/lib/apt/lists/* /tmp/library-scripts

USER ${NB_USER}

### Prints Jupyter server token when terminal is opened
RUN echo "echo \"Jupyter server token: \$(jupyter server list 2>&1 | grep -oP '(?<=token=)[[:alnum:]]*')\"" > ${HOME}/.get-jupyter-url.sh && \
    echo "sh \${HOME}/.get-jupyter-url.sh" >> ${HOME}/.bashrc

RUN pip install otter-grader==4.3.1