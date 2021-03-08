FROM python:{{cookiecutter.python_version}}-slim

# Sets the name for the user to be used in the container.
# In order to have no problems with file permision make sure that
# the USER_UID matches your ID if you are using a ~unix system.
ARG USERNAME=dev
ARG UID=1000
ARG GID=1000

ENV PIPENV_SKIP_LOCK=1

# Gets all updates and installs sudo
RUN apt update && apt install -y sudo
RUN pip3 install pipenv

# Adds the user and allows it sudo privileges without needing a password

# RUN adduser ${USERNAME} --uid ${UID} --gid ${GID} --gecos "" --disabled-password &&\
RUN groupadd -g ${GID} -o ${USERNAME} &&\
    useradd -m -u ${UID} -g ${GID} -o -s /bin/bash ${USERNAME} && \
    echo ${USERNAME} ALL=\(ALL\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} &&\
    chmod 0440 /etc/sudoers.d/${USERNAME}


# Switches to the user
USER ${USERNAME}
WORKDIR /app

# Recursively change permisions in folder in case there are files
# that still belong to root
RUN sudo chown -R ${USERNAME} .

# It copies all the files that do not change often. Speeds up rebuild process.
# The flag --chown copies the file directly as the wanted user
COPY --chown=${USERNAME} Pipfile setup.py ./
COPY --chown=${USERNAME} src/__init__.py src/

# Install all the dependencies
RUN pipenv install

# Copy the rest of the files and directories
COPY --chown=${USERNAME} . .

# Makes out a nice prompt in case you have to go inside of the container for any reason
RUN echo 'export PS1="🐳 \[\033[1;36m\][\u@docker] \[\033[1;34m\]\W\[\033[0;35m\] # \[\033[0m\]"' >> ~/.bashrc
