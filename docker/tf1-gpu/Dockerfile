FROM tensorflow/tensorflow:1.15.2-gpu-py3

# Required for MPI setup
RUN apt-get update && apt-get install -y openssh-client libopenmpi-dev

ENV PYTHONUNBUFFERED 1

# We install all requirements into the local Docker instance
RUN pip install --upgrade pip

COPY . /app

WORKDIR /app

# Don't cache installers to reduce image size
RUN pip install --no-cache-dir .

# Create a user and group that is not the root user
RUN groupadd -r trainer && useradd --no-log-init -r -g trainer trainer

# Run all commands as trainer
USER trainer:trainer
