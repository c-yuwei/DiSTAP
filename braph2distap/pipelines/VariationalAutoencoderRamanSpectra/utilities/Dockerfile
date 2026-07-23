# Fixed R 4.4.1 environment.
# Available for amd64 and arm64/Apple Silicon.
FROM rocker/r-ver:4.4.1

ARG DEBIAN_FRONTEND=noninteractive

ENV LANG=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8

# System dependencies for tidyverse, sf, magick, hdf5r, ragg,
# hrbrthemes, fs, and related packages.
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    gfortran \
    cmake \
    patch \
    pkg-config \
    git \
    fontconfig \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev \
    libicu-dev \
    libuv1-dev \
    libhdf5-dev \
    libmagick++-dev \
    ghostscript \
    libcairo2-dev \
    libharfbuzz-dev \
    libfribidi-dev \
    libfontconfig1-dev \
    libfreetype6-dev \
    libpng-dev \
    libjpeg-dev \
    libtiff-dev \
    libwebp-dev \
    libudunits2-dev \
    libgdal-dev \
    libgeos-dev \
    libproj-dev \
    libabsl-dev \
    fonts-roboto \
    fonts-ibm-plex \
 && rm -rf /var/lib/apt/lists/*

# Refresh the font cache for hrbrthemes.
RUN fc-cache -f

# Do not override the repository configured by rocker/r-ver.
# Its snapshot contains packages compatible with R 4.4.1.
RUN R -q -e " \
  pkgs <- c( \
    'tidyverse', \
    'ggpubr', \
    'R.matlab', \
    'hdf5r', \
    'cowplot', \
    'ggpattern', \
    'magick', \
    'here', \
    'sf', \
    'ragg', \
    'ggrepel', \
    'viridis', \
    'ggsci', \
    'remotes', \
    'hrbrthemes' \
  ); \
  missing <- setdiff(pkgs, rownames(installed.packages())); \
  if (length(missing)) { \
    install.packages(missing); \
  }; \
  missing <- setdiff(pkgs, rownames(installed.packages())); \
  if (length(missing)) { \
    stop('Failed to install: ', paste(missing, collapse=', ')); \
  }; \
  unloadable <- pkgs[!vapply( \
    pkgs, requireNamespace, logical(1), quietly=TRUE \
  )]; \
  if (length(unloadable)) { \
    stop('Failed to load: ', paste(unloadable, collapse=', ')); \
  }; \
  message('All requested R packages installed successfully.')"

WORKDIR /work

CMD ["R", "--quiet"]