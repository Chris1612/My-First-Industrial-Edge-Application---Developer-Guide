# My first Industrial Edge App - App Developer Guide

Creating a first Industrial Edge App on a development environment to deploy it to an Industrial Edge Device based on App Developer Guide.

- [Prerequisites](#prerequisites)
- [Description](#description)
- [Contribution](#contribution)
- [Licence and Legal Information](#licence-and-legal-information)

## Prerequisites

The Prerequisites are the App Developer Guide which will be available on SIOS soon. It will contain all the description of the requirements as well as the step-by-step description of the distributed content in this repository.

## Description

As the example app will cover the most common use case in the Industrial Edge environment, the app on the Industrial Edge Device will look like the architectural overview in the figure below. The goal of the app will be to collect, process and store data from an OPC UA Server, which provides data from a PLC.

![Overview of app architecture](./docs/Picture_5_3_Architecture_IED.png)

The app contains three parts – the connectivity to collect the data from the OPC UA Server by system apps, the IE Databus for distributions of the data and the process, storing and visualization of data in the Edge App.

1. The IE Databus based on MQTT is responsible to distribute data to certain topics, which are filled by system or custom apps by publishing and subscribing to these topics.
2. To receive the data from the OPC UA server, which is providing data from a PLC, the SIMATIC S7 Connector connectivity is used. SIMATIC S7 Connector is a system app, which publish the data to IE Databus. Another system app, the IE Flow Creator, consumes the data from the SIMATIC S7 Connector topics on the IE Databus. The data is preprocessed in the SIMATIC Flow Creator and published again on the IE Databus.
3. The developed data analytics container with Python is consuming the preprocessed data on the topics from the SIMATIC Flow Creator. The Python data analytics is doing calculations and evaluations and provides the results like KPIs back on the IE Databus.The data analytics container needs a MQTT client to handle the publishes and subscriptions of the IE Databus
4. The IE Flow Creator consumes the analyzed data again. The IE Flow Creator stores the (raw) data and analyzed data to the InfluxDB persistently.
5. The InfluxDB is a time series database which is optimized for fast, high-availability storage and retrieval of time series data. It stores the data, which is transmitted by the OPC UA server to the app as well as the analyzed data.
6. Grafana is a visualization and analytics software. It allows to query, visualize, alert and explore metrics. It provides tools to turn time-series database data to graphs and visualization. There is the possibility to build custom dashboards. Grafana is used to visualize the data from the InfluxDB database

## Documentation

- Here is a link to the [SIOS](https://support.industry.siemens.com/cs/sc?lc=de-WW) where the App Developer Guide of this application example can be found.
- You can find further documentation and help in the following links
  - [Industrial Edge Hub](https://iehub.eu1.edge.siemens.cloud/#/documentation)
  - [Industrial Edge Forum](https://www.siemens.com/industrial-edge-forum)
  - [Industrial Edge landing page](http://siemens.com/industrial-edge)
  
## Contribution

Thanks for your interest in contributing. Anybody is free to report bugs, unclear documenation, and other problems regarding this repository in the Issues section or, even better, is free to propose any changes to this repository using Merge Requests.

## Licence and Legal Information

Please read the [Legal information](LICENSE.md).
