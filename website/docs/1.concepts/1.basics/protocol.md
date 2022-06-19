---
id: protocol
title: Protocol
---

GPUX aims to be a planetary supercomputer that anyone use or can add resources to. 

1. **Stay Online** and be nearly impossible to bring down, no central mechanisms, each node is independent
2. **Deploy** any job that fits into a Dockerfile
3. **Scale** simply through sheppard applications
4. **Onboard** users with a smooth experience
5. **Be Green and Purposeful** like finding a cure to alzheimer's through protein-folding

## Why build this? {#why-are-we-building-gpux}
Currently, most of our services run "in the cloud", meaning large companies like AWS, Azure and GCP compete to 
bait you into their quagmire, once you are in, it becomes very expensive to get out.

GPUX takes a different approach, instead of being forced to choose the lesser of an evil why not
create a standard ecosystem and protocol that any compute resource can be connected to and utilized. 
By the standardization of a work unit down to a Dockerfile, that can run on any system in the network.

There exists various attempts at something like this but they require you to write code in a certain 
intermediary language like WASM, or they are too cumbersome to use, or too expensive.

## What can we do on the network?
There are two main roles that any user can perform in the GPUX ecosystem: `creating jobs` or `running a node`.

**Creating Jobs**: Transferring credits to node runners who execute your Dockerfile. Your container can have as much
cpus, ram or gpus attached as you request.

**Running a Node**: Farmers aka node runners run the `./farm` binary on each piece of hardware they want to connect. By
connecting their hardware they allow job creators to find it and can collect fees from executing said jobs.

## How secure is GPUX?
GPUX is as secure as any datacenter or hosting provider you use. Node runners have ratings and can provide extra credentials like their physical tier of datacenter or carbon footprint. You will have more security with a node runner who is Tier4 certified than you would with someone providing out their homelab. The choice is up to you.

## How is my job protected from prying eyes 👀?
GPUX is working on Enclave Technology (SGX, AMDSEV, and MKTME), once chip implementation problems are ironed out (like AMDSEV being cleartexted with physical access + root (https://arxiv.org/pdf/2108.04575.pdf)). Once creased out you can run your Dockerfile on a remote homelab and be confident your app+data+ram are fully encrypted. No prying eyes.

