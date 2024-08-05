


# K8sGPT Installation and Configuration Guide

## DEB-based Installation (Ubuntu/Debian)

### Download the .deb Package:

```bash
curl -LO https://github.com/k8sgpt-ai/k8sgpt/releases/download/v0.3.24/k8sgpt_amd64.deb
sudo dpkg -i k8sgpt_amd64.deb
```

### Verify Installation

Ensure K8sGPT is installed correctly:

```bash
k8sgpt version
```

## Setting Up the K8sGPT CLI Backend

To set up the K8sgpt backend, we will use the LocalAI service as an inference provider which will use the model `Meta-Llama-3.1-8B-Instruct`.

### Add the LocalAI Backend:

```bash
k8sgpt auth add --backend localai --model ${MODEL_NAME} --baseurl http://${IP_LOCALAI}/v1
```

### Set LocalAI as the Default Provider:

```bash
k8sgpt auth default --provider localai
```

### List Your Backends

You can list your backends with the following command, which should return something like this:

```bash
k8sgpt auth list
```

Output:
```
Default: 
> localai
Active: 
> localai
Unused: 
> openai
> azureopenai
> noopai
> cohere
> amazonbedrock
> amazonsagemaker
```

### Making a Query

To make a query to the model hosted in LocalAI, use the following command. It should return something like this:

```bash
k8sgpt analyze --explain
```

Output:
```
100% ███████████████████████████████████████████████████████████████████████████████████████████████████| (2/2, 3 it/min)         
AI Provider: localai

0 default/pod-test-invalid(pod-test-invalid)
- Error: Back-off pulling image "nonexistentimage123"

Error: Unable to pull image "nonexistentimage123" due to back-off.
Solution: 
1. Check the image name and ensure it exists in the Docker registry.
2. Verify the Docker registry is accessible and running.
3. Pull the correct image using `docker pull nonexistentimage123` command.

1 default/miotropod(miotropod)
- Error: Back-off pulling image "noexistetampoco"

Error: Unable to pull non-existent Docker image "noexistetampoco".
Solution: 
1. Check the image name for spelling mistakes.
2. Verify the image exists in Docker Hub or local registry.
3. Update the pod configuration with the correct image name.
```

### Help Command

To view all the commands provided by K8sGPT, use the `--help` flag:

```bash
k8sgpt --help
```
