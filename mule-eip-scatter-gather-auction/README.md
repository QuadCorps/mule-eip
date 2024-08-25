# Enterprise Integration Patterns: The Scatter Gather (Distribution Style)



This Mule application implements a simple use-case for the Scatter-Gather 
pattern and accompanies a series of [blog posts](https://quadcorps.co.uk/eip-mule-scatter-gather-1/).
## Overview

### Caveat

This is a basic implementation of the Mule Scatter-Gather pattern. The specific
implementation could be adapted to various business needs but is used here to demonstrate
the Scatter-Gather pattern in a simple scenario based on the Distribution variant of the
pattern as provided out-of-the-box by MuleSoft.

### Components

1. **mule-get-best-quote-main-flow**: This flow is triggered by an HTTP request and performs the following actions:
   - Receives HTTP requests through the configured listener.
   - Uses a Scatter-Gather component to distribute the request to multiple routes.
   - Transforms the aggregated results into the desired format.
   - Logs the final output.
   

2. **call-carrier1-subflow, call-carrier2-subflow, call-carrier3-subflow**: These sub-flows process the requests for three different carriers. Each sub-flow performs the following tasks:
   - Sends an HTTP request to the respective carrier.
   - Transforms the carrier's response into a standardised format.
   - Logs the transformed response.

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

1. **mule-get-best-quote-main-flow**:
   - Send an HTTP GET request to the configured endpoint, by default: `http://0.0.0.0:8081`
   - The flow will process the request using Scatter-Gather, aggregate the results from different carriers, and return the best quote.
   
## Additional Information

- This Mule project uses Mule 4.x.
- Customise the payload values and business logic as per your requirements.
- Ensure proper error handling and logging configurations are in place for production deployments.