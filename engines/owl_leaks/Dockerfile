FROM alpine:latest
MAINTAINER Patrowl.io "getsupport@patrowl.io"
LABEL Name="Patrowl\ Data\ Leaks\ \(Patrowl engine\)" Version="1.0.0"

# Install dependencies
RUN apk add --update \
    python \
    python-dev \
    py-pip \
  && rm -rf /var/cache/apk/*

# Create the target repo
RUN mkdir -p /opt/patrowl-engines/owl_leaks
RUN mkdir -p /opt/patrowl-engines/owl_leaks/results
RUN mkdir -p /opt/patrowl-engines/owl_leaks/utils

# Set the working directory to /opt/<engine_name>
WORKDIR /opt/patrowl-engines/owl_leaks

# Copy the current directory contents into the container at /
COPY __init__.py .
COPY engine-owl_leaks.py .
COPY requirements.txt .
COPY owl_leaks.json.sample owl_leaks.json

# Install python modules
RUN pip install --upgrade pip
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# TCP port exposed by the container (NAT)
EXPOSE 5012

# Run app.py when the container launches
CMD ["python", "engine-owl_leaks.py", "--port=5012", "--host=0.0.0.0"]
