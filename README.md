# Web3 Image Generation

This project aims at creating a decentralized system for text-to-image processing using smart contracts.

## Current State of Image Generation

With the advent of text-to-image processing with AI, many companies are developing new products to capitalize on this technology. Examples include Wombo, NightCafe and StarryAI (not to mention OpenAI and DALL-E). These probably make use of open-source technology, but the platforms are closed. The creators either take the risk of purchasing their own hardware or renting Cloud GPUs, and need to come up with a profitable business model. Users are limited to what the platform provides.

## Decentralized Flow

What is proposed here is an alternative system where users and providers can interact in a mutually beneficial way through blockchain smart contracts. Below is a very high-level description of how the typical flow might work. Many details still need to be worked out.

* Users submit a request to the system with a specific configuration. This may include a text prompt, the model to use, and parameters that are specific to the model, such as number of iterations, etc.
  * Question: How can a user send requests to the smart contract? This could be modeled as a payment with the request details embedded in the transaction metadata.
* Images can be stored on IPFS.
* Many worker nodes will be waiting to accept requests. When a request is received from the smart contract, the worker node will process the request. The resulting image will be placed on IPFS, and the CLIP ranking of the image vs the prompt will be recorded.
* Multiple verifier nodes can check the CLIP ranking against the generated image.
* Once the CLIP ranking has been verified, a payment is made from the smart contract to the worker node.
* The user can download the image from IPFS.

## Preventing Bad Actors

One problem with the system described above is that bad actors can set up worker nodes that just generate white noise, using very little compute resources. In order to prevent this, additional safeguards are proposed:

* Given the same exact model and configuration, any worker node should produce CLIP rankings with the same statistical distribution as any other. An auditing system will be put in place that will analyze the CLIP rankings produced by worker nodes to detect deviation from "good behavior".
* In order to have a worker node join the system, some amount of funds must be posted as collateral.
* If a worker node is identified as a bad actor, the collateral will be forfeited and the worker node will be removed from the system.