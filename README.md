# MITRE Caldera™

[![Release](https://img.shields.io/badge/dynamic/json?color=blue&label=Release&query=tag_name&url=https%3A%2F%2Fapi.github.com%2Frepos%2Fmitre%2Fcaldera%2Freleases%2Flatest)](https://github.com/mitre/caldera/releases/latest)  
[![Testing Status](https://github.com/mitre/caldera/actions/workflows/quality.yml/badge.svg?branch=master)](https://github.com/mitre/caldera/actions/workflows/quality.yml?query=branch%3Amaster)  
[![Security Status](https://github.com/mitre/caldera/actions/workflows/security.yml/badge.svg?branch=master)](https://github.com/mitre/caldera/actions/workflows/security.yml?query=branch%3Amaster)  
[![codecov](https://codecov.io/gh/mitre/caldera/branch/master/graph/badge.svg)](https://codecov.io/gh/mitre/caldera)  
[![Documentation Status](https://readthedocs.org/projects/caldera/badge/?version=stable)](http://caldera.readthedocs.io/?badge=stable)

## Overview

**MITRE Caldera™** is a cybersecurity platform designed to:
- Automate adversary emulation,
- Assist manual red teams,
- Automate incident response.

Caldera is built on the [MITRE ATT&CK™ framework](https://attack.mitre.org/) and is an active research project at MITRE.

---

## Framework Components

### Core System
The main framework, which includes:
- An asynchronous command-and-control (C2) server,
- A REST API,
- A web interface.

### Plugins
Extend the framework’s capabilities with plugins for agents, reporting, TTPs, and more.

---

## Resources & Social Links
- 📜 [Documentation](https://caldera.readthedocs.io/en/latest/)  
- ✍️ [Caldera's Blog](https://medium.com/@mitrecaldera/welcome-to-the-official-mitre-caldera-blog-page-f34c2cdfef09)  
- 🌐 [Homepage](https://caldera.mitre.org)  

---

## Plugins

### Default Plugins
Supported and maintained by the Caldera team:
- **[Access](https://github.com/mitre/access)**: Initial access tools and techniques.
- **[Atomic](https://github.com/mitre/atomic)**: Atomic Red Team TTPs.
- **[Builder](https://github.com/mitre/builder)**: Compile payloads dynamically.
- **[Compass](https://github.com/mitre/compass)**: ATT&CK visualizations.
- **[Magma](https://github.com/mitre/magma)**: VueJS UI for Caldera v5.
- **[Sandcat](https://github.com/mitre/sandcat)**: Default agent.
- **[Stockpile](https://github.com/mitre/stockpile)**: Technique and profile storehouse.
- **[Training](https://github.com/mitre/training)**: Training and certification resources.

### Additional Plugins
These plugins are not included by default and are not maintained by the Caldera team:
- **[Arsenal](https://github.com/mitre-atlas/arsenal)**: ATLAS techniques and profiles.
- **[Pathfinder](https://github.com/center-for-threat-informed-defense/caldera_pathfinder)**: Vulnerability scanning.
- **[SAML](https://github.com/mitre/saml)**: SAML authentication.

---

## Requirements
- Linux or macOS.
- Python 3.8+ (with Pip3).
- Recommended: 8GB+ RAM and 2+ CPUs.
- **Optional**: GoLang 1.17+ for compiling agents dynamically.
- NodeJS (v16+ recommended for VueJS UI).

---

## Installation

### Quick Setup:
```bash
git clone https://github.com/mitre/caldera.git --recursive
cd caldera
pip3 install -r requirements.txt
python3 server.py --insecure --build


## Full Steps

Start by cloning this repository recursively, passing the desired version/release in `x.x.x` format. This will pull in all available plugins.

```bash
git clone https://github.com/mitre/caldera.git --recursive --tag x.x.x
```

Next, install the PIP requirements:

```bash
pip3 install -r requirements.txt
```

**Super-power your Caldera server installation!**  
[Install GoLang (1.19+)](https://go.dev/doc/install) to enable advanced features.

Finally, start the server:

```bash
python3 server.py --insecure --build
```

The `--build` flag automatically installs any VueJS UI dependencies, bundles the UI into a `dist` directory, writes the Magma plugin's `.env` file, and serves it via the Caldera server. You only need to use the `--build` flag again if you add plugins or make changes to the UI.

Once the server is started, log in at [http://localhost:8888](http://localhost:8888) using the default credentials `red/admin`. Then, go to Plugins -> Training and complete the capture-the-flag style training course to learn how to use Caldera.

In some cases, the default configuration values may cause the UI to appear unresponsive due to misrouted requests. Modify the `app.frontend.api_base_url` config value and restart the server with the `--build` flag to update the UI's request URL environment variable.

If you prefer not to use the new VueJS UI, revert to Caldera v4.2.0. For earlier versions, the `--build` flag is not required.

---

## User Interface Development

If you'll be developing the UI, additional setup steps are required.

### Requirements
- NodeJS (v16+ recommended)

### Setup

1. Add the Magma submodule (if not already added):
   ```bash
   git submodule add https://github.com/mitre/magma
   ```
2. Install NodeJS dependencies:
   ```bash
   cd plugins/magma && npm install && cd ..
   ```
3. Start the Caldera server with an additional flag:
   ```bash
   python3 server.py --uidev localhost
   ```

Your Caldera server will be available at [http://localhost:8888](http://localhost:8888), but there will also be a hot-reloading development server for the VueJS front-end at [http://localhost:3000](http://localhost:3000). Logs from both the server and the front-end will appear in the terminal where you launched the server.

---

## Docker Deployment

To build a Caldera Docker image, ensure Docker is installed and follow these steps:

```bash
# Recursively clone the Caldera repository (if not already done)
git clone https://github.com/mitre/caldera.git --recursive

# Build the Docker image (customize tagging as needed)
# WIN_BUILD allows Caldera to compile Windows-based agents.
cd caldera
docker build . --build-arg WIN_BUILD=true -t caldera:latest

# Run the Docker image (customize port forwarding as needed)
docker run -p 8888:8888 caldera:latest
```

To gracefully terminate your Docker container:

```bash
# List all running containers
docker ps

# Stop the container
docker stop [container ID]
```

---

## Contributing

Refer to the [contributor documentation](CONTRIBUTING.md) for guidelines on how to contribute.

---

## Vulnerability Disclosures

Refer to the [Vulnerability Disclosure Documentation](SECURITY.md) for submitting bugs or security issues.

---

## Licensing

For licensing opportunities, please reach out via email to [caldera@mitre.org](mailto:caldera@mitre.org) or contact [MITRE's Technology Transfer Office](https://www.mitre.org/about/corporate-overview/contact-us#technologycontact).

---

## Caldera Benefactor Program

If you are interested in supporting, sustaining, or evolving MITRE Caldera™'s open-source capabilities, please contact us at [caldera@mitre.org](mailto:caldera@mitre.org).
