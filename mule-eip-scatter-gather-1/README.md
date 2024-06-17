# Enterprise Integration Patterns: The Scatter Gather (Distribution Style)



This Mule application implements a trivial use-case for the aggregator pattern and accompanies a series of [blog posts](https://quadcorps.co.uk/eip-mule-scatter-gather-distribution/).

## Overview

### Caveat

This is a simple use-case of the Mule aggregator. This specific implementation could easily be replaced by a DataWeave transformation. However, the implementation is used purely as a vehicle to demonstrate splitting and aggregation at its most basic.

### Components

1. **mule-main-flow**: This flow is triggered by an HTTP request and performs the following actions:
    - Receives HTTP requests through the configured listener.
    - Sets a payload containing an array of shipment IDs.
    - Stores the size of the payload in a variable called `groupSize`.
    - Splits the payload into individual messages using a foreach loop.
    - Calls the `mule-aggregator-subflow` for each message.
    - Sets the payload of the response to the processed shipment.


2. **mule-aggregator-subflow**: This sub-flow is called by the main flow to process individual messages. It performs the following tasks:
    - Transforms the payload into a JSON object representing a package entity, including a package ID, tax, and delivery option.
    - Aggregates packages using a group-based aggregator based on the `groupSize` variable.
    - Upon aggregation completion, transforms the payload into a JSON object representing a shipment entity, including a shipment ID, tracking ID, and packages.
    - Stores the aggregated content in a variable called `shipment`.

## Prerequisites

To run this Mule project, you need:
- Anypoint Studio
- Mule Runtime installed (optional for standalone deployment)

## Installation

1. Clone or download the project repository.
2. Import the project into Anypoint Studio or deploy it to your Mule Runtime.

## Configuration

- Ensure that the HTTP listener configuration (`HTTP_Listener_config`) is properly set, including the host address and port number.
- Adjust the paths and endpoints in the HTTP listener and flow references as needed.

## Usage

1. **mule-main-flow**:
    - Send an HTTP GET request to the configured endpoint, by default: `http://0.0.0.0:8081`
    - The flow will process the shipment IDs and return the processed shipment details.

## Additional Information

- This Mule project uses Mule 4.x.
- Customise the payload values and business logic as per your requirements.
- Ensure proper error handling and logging configurations are in place for production deployments.