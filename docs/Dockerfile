FROM jenkins/jenkins
USER root

# Instalar dependencias para Python y crear un entorno virtual
RUN apt-get update && apt-get install -y \
    lsb-release \
    python3 \
    python3-venv \
    && rm -rf /var/lib/apt/lists/*

# Crear un directorio para el entorno virtual y activarlo
RUN python3 -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

# Instalar pytest
RUN pip3 install pytest

# Instalar PyInstaller
RUN pip3 install pyinstaller

# Instalar Docker CLI
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.asc] https://download.docker.com/linux/debian $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce-cli

USER jenkins

# Instalar plugins de Jenkins
RUN jenkins-plugin-cli --plugins "blueocean docker-workflow"