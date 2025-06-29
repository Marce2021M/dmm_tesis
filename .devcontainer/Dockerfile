# Usa la imagen base oficial de Codespaces (Ubuntu x86_64)
FROM mcr.microsoft.com/vscode/devcontainers/base:ubuntu

# Instala dependencias del sistema
RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-dev \
                       libblas-dev liblapack-dev gfortran && \
    rm -rf /var/lib/apt/lists/*

# Instala Theano (v1.0.5) y librerías científicas
RUN pip3 install --no-cache-dir theano==1.0.5 numpy scipy