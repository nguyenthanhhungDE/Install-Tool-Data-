
FROM python:3.9.16-slim

# Install spark and java
ARG openjdk_version="17"

RUN apt-get update --yes && \
    apt-get install --yes curl "openjdk-${openjdk_version}-jre-headless" ca-certificates-java procps && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Add repository code
WORKDIR /opt/dagster/app/etl_pipeline  
COPY requirements.txt /opt/dagster/app/etl_pipeline
RUN pip install --upgrade pip && pip install -r requirements.txt
COPY . /opt/dagster/app/etl_pipeline

# CMD allows this to be overridden from run launchers or executors that want to run other commands against your repository
CMD ["dagster", "api", "grpc", "-h", "0.0.0.0", "-p", "4000", "-m", "etl_pipeline"]
# CMD ["dagster", "code-server", "start", "-h", "0.0.0.0", "-p", "4000", "-f", "etl_pipeline"]