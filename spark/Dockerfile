FROM bitnami/spark:3.3

USER root

# Install prerequisites
RUN apt-get update && apt-get install -y curl make gcc wget

RUN apt-get install -y --no-install-recommends \
    rsync && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*


# AWS S3/Minio Connector 
# Already have hadoop-aws: /opt/bitnami/spark/jars/hadoop-aws-*.jar , aws-java-sdk-bundle-*.jar
RUN curl -O https://repo1.maven.org/maven2/software/amazon/awssdk/s3/2.18.41/s3-2.18.41.jar \
    && curl -O https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk/1.11.1026/aws-java-sdk-1.11.1026.jar \
    && curl -O https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk-bundle/1.11.1026/aws-java-sdk-bundle-1.11.1026.jar \
    && curl -O https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-aws/3.3.2/hadoop-aws-3.3.2.jar  \
    && mv s3-2.18.41.jar /opt/bitnami/spark/jars \
    && mv aws-java-sdk-1.11.1026.jar /opt/bitnami/spark/jars \
    && mv aws-java-sdk-bundle-1.11.1026.jar /opt/bitnami/spark/jars \
    && mv hadoop-aws-3.3.2.jar /opt/bitnami/spark/jars

COPY ojdbc11.jar /opt/bitnami/spark/jars/

# Create and event logging directory to store job logs
RUN mkdir /tmp/spark-events

RUN chmod u+x /opt/bitnami/spark/sbin/* && \
    chmod u+x /opt/bitnami/spark/bin/*

COPY ./conf/spark-defaults.conf "$SPARK_HOME/conf/spark-defaults.conf"

# COPY entrypoint.sh .

# ENTRYPOINT ["./entrypoint.sh"]