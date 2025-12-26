# Base image as requested
FROM jupyter/base-notebook:x86_64-ubuntu-22.04

# Switch to root for OS package installs
USER root

# Avoid interactive prompts during apt installs
ENV DEBIAN_FRONTEND=noninteractive

# System deps: LaTeX toolchain for jupyter-book PDF builds + ImageMagick + build tools
RUN apt-get update && apt-get install -y --no-install-recommends \
    make \
    ghostscript \
    latexmk \
    imagemagick \
    texlive-latex-base \
    texlive-latex-recommended \
    texlive-latex-extra \
    texlive-xetex \
    texlive-fonts-recommended \
    texlive-fonts-extra \
    texlive-lang-german \
    gosu \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*



# Upgrade pip and install Python dependencies
# Expect a doc-requirements.txt in the build context (same folder as Dockerfile)
COPY --chown=${NB_UID}:${NB_GID} doc-requirements.txt /tmp/doc-requirements.txt
RUN python -m pip install --no-cache-dir --upgrade pip \
 && python -m pip install --no-cache-dir -r /tmp/doc-requirements.txt \
 && rm -f /tmp/doc-requirements.txt

# Set a sensible working directory (matches typical jupyter images)
WORKDIR /home/jovyan/work
