FROM ubuntu:22.04

RUN apt-get update && apt-get install -y \
    wget perl unzip fontconfig xz-utils \
    && rm -rf /var/lib/apt/lists/*

COPY texlive.profile /

ARG TEXLIVE_VERSION=2025

RUN wget http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz && \
    mkdir /install-tl-unx && \
    tar -xvf install-tl-unx.tar.gz -C /install-tl-unx --strip-components=1 && \
    /install-tl-unx/install-tl \
        -repository http://ftp.math.utah.edu/pub/tex/historic/systems/texlive/${TEXLIVE_VERSION}/tlnet-final \
        -profile /texlive.profile && \
    rm -rf /install-tl-unx install-tl-unx.tar.gz

# version-independent PATH
ENV PATH="/usr/local/texlive/${TEXLIVE_VERSION}/bin/x86_64-linux:${PATH}"

# install packages
RUN tlmgr install \
    xetex etoolbox xifthen ifmtarg \
    microtype fontspec pgf parskip \
    setspace multirow fontawesome5 progressbar \
    titlesec enumitem tcolorbox environ \
    listings paracol booktabs pagecolor \
    lipsum xkeyval collectbox adjustbox \
    tikzfill pdfcol

ENV HOME=/tex-cvbuilder
WORKDIR /tex-cvbuilder
