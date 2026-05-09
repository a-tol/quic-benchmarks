# QUIC Benchmarks

Credit to https://github.com/triplewy/quic-benchmarks
for their original benchmark code. This repository is a
fork with preset configurations to benchmark our EC2 instance,
as well as any local servers from quic-multitest-server.

use python3 -m venv [environment_directory] and place all the files
from this repository there, then install all the required dependencies.

./run_benchmarks.sh runs the QUIC HTTP3 client various network traffic shaping conditions. Please ensure that the name of the network device specified in each file in the ./networks directory matches the one used by your local PC, specifically your network device.
If it is different, please run
sed -i 's/wlp2s0/[device_name]/g' *
where your network device name is specified in [device_name].

Follow the same steps as listed below to run the benchmark.
Install http3-curl from https:github.com/stunnel/static-curl
and set the path of the curl binary you downloaded to the first attribute of the "curl_h3" item in ./clients.json to the path where your curl binary is placed.

We obtain the dataset of runtimes in ./data/runtimes.
Please ask Meghana how she created the plots for the paper, in that regard.

-----------------------------------------------------------------

This repository is a set of scripts to benchmark, compare, and analyze QUIC performance, modified from Alexander Yu's QUIC benchmarking toolset in https://github.com/triplewy/quic-benchmarks, originally used for **Dissecting Performance of Production QUIC." These tools are preconfigured for usage with our Amazon EC2 instance, alongside other optional, local endpoints which are detailed in `endpoints.json`.

The general workflow for this benchmark comprises of the below steps:

1. Use a QUIC clients to send requests to "production" endpoints
2. Gather logs and metrics from these requests via QLOG.

## Clients

- QUIC (HTTP/3)
  - Ngtcp2 via CURL
- TCP, unused (HTTP/2)
  - cURL

A static curl binary is included.

## Setup

### Building Locally

1. Download and build the cURL client, or download a static cURL binary from https://github.com/stunnel/static-curl.
2. Once you have these clients installed, modify `local.json` with their respective paths. You will notice in `local.json` that the paths are currently from my machine.
3. So you will need Node.js to run `npm install` in the `./chrome` directory.
4. You will need Python 3 to run the benchmarking script.
5. Run `./bin/pip3 install -r requirements.txt` to download Python depedencie to run the benchmarking script.

## Usage

```
sudo ./run_benchmarks.sh

Sudo permission is necessary to perform network shaping.