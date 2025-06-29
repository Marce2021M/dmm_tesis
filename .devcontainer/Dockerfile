###############################################################################
# Deep-Markov-Model – DevContainer sólo con Python 2.7
###############################################################################
FROM mcr.microsoft.com/vscode/devcontainers/base:ubuntu-22.04

# ── Paquetes de sistema que SÍ necesitamos ────────────────────────────────────
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        python2 python2-dev build-essential curl git unzip && \
    rm -rf /var/lib/apt/lists/*

# ── Instalar pip/virtualenv compatibles con Py-2.7 ────────────────────────────
# (el script “get-pip.py” especial congela pip 20.x y setuptools 44.x,
# últimas versiones que soportan 2.7)
RUN curl -sS https://bootstrap.pypa.io/pip/2.7/get-pip.py -o /tmp/get-pip.py && \
    python2 /tmp/get-pip.py && rm /tmp/get-pip.py && \
    python2 -m pip install --no-cache-dir virtualenv && \
    virtualenv -p python2 /opt/venv

# Activar el virtualenv por defecto en todas las shells
ENV PATH="/opt/venv/bin:${PATH}"
RUN echo 'source /opt/venv/bin/activate' > /etc/profile.d/use_venv.sh

# ── Librerías necesarias para el DMM ──────────────────────────────────────────
#  • numpy/scipy en sus últimas versiones soportadas por Py-2.7
#  • theano 0.9.0 (la versión empleada por el paper original)
#  • theanomodels fijado al commit bb1c81a (funciona; el ‘aa8104c’ no existe)
RUN pip install --no-cache-dir \
        numpy==1.16.6 \
        scipy==1.2.3 \
        theano==0.9.0

# ── (Opcional) Deno – sigue instalado, por si lo usas en otro punto ──────────
ENV DENO_INSTALL="/usr/local"
ENV PATH="${DENO_INSTALL}/bin:${PATH}"
RUN curl -fsSL https://deno.land/install.sh | sh

# ── Directorio de trabajo por defecto ────────────────────────────────────────
WORKDIR /workspaces