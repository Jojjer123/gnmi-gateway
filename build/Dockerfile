FROM golang:1.14-alpine

ENV INSTALL_DIR gnmi-gateway

RUN mkdir -p $INSTALL_DIR/
COPY . $INSTALL_DIR

RUN apk add --update make gcc g++ git openssl
# RUN make buildExecutable
# RUN make download
# RUN make tls
# RUN ./gnmi-gateway -version

# RUN chmod +x ./bin/github.com/openconfig/gnmi-gateway

COPY bin/github.com/openconfig testing
COPY targets.json targets.json

CMD ["./testing/gnmi-gateway", \
    "-TargetLoaders=json", \
    "-TargetJSONFile=./targets.json", \
    # "-EnableGNMIServer", \
    "-ExporterKafkaBatchSize=1", \
    "-Exporters=kafka", \
    "-ExporterKafkaBrokers=10.91.216.17:9092", \
    "-ExporterKafkaTopic=counter_testing", \
    "-OpenConfigDirectory=./oc-models/", \
    "-ServerTLSCert=server.crt", \
    "-ServerTLSKey=server.key"]