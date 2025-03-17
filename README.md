# NGORK and Self-hosted AI starter kit

This repo combines the self-hosted n8n ai starter kit with ngrok, so external services can call n8n trigger nodes.

> [Original n8n starter kit](https://blog.n8n.io/self-hosted-ai/)

### What’s included

✅ [**Self-hosted n8n**](https://n8n.io/) - Low-code platform with over 400
integrations and advanced AI components

✅ [**Ollama**](https://ollama.com/) - Cross-platform LLM platform to install
and run the latest local LLMs

✅ [**Qdrant**](https://qdrant.tech/) - Open-source, high performance vector
store with an comprehensive API

✅ [**PostgreSQL**](https://www.postgresql.org/) -  Workhorse of the Data
Engineering world, handles large amounts of data safely.

## Installation

### Cloning the Repository

```bash
git clone https://github.com/zalias9/n8n-local-ai-kit-with-ngrok
cd n8n-local-ai-kit-with-ngrok
```

### Update .env and ngrok.yml [**Important**]

1. Copy `.env.sample` to `.env` and update the PostgreSQL values.
2. Go to [ngrok.com](https://ngrok.com/) and create an account.
3. Create a custom domain, every account gets 1 free domain.
4. Replace `your-domain.ngrok-free.app` with your domain in `ngrok.yml` (no https://)
5. Replace `https://your-domain.ngrok-free.app` with your domain in `.env` (with https://)
6. Copy your ngrok token and paste it in `NGROK_TOKEN` in .env


### Running n8n using Docker Compose

#### For Nvidia GPU users

```bash
docker compose --profile gpu-nvidia up
```

> [!NOTE]
> If you have not used your Nvidia GPU with Docker before, please follow the
> [Ollama Docker instructions](https://github.com/ollama/ollama/blob/main/docs/docker.md).

#### For AMD GPU users on Linux

``` bash
docker compose --profile gpu-amd up
```

#### For Mac / Apple Silicon users (not tested, instructions from [original starter kit](https://github.com/n8n-io/self-hosted-ai-starter-kit))

If you’re using a Mac with an M1 or newer processor, you can't expose your GPU
to the Docker instance, unfortunately. There are two options in this case:

1. Run the starter kit fully on CPU, like in the section "For everyone else"
   below
2. Run Ollama on your Mac for faster inference, and connect to that from the
   n8n instance

If you want to run Ollama on your mac, check the
[Ollama homepage](https://ollama.com/)
for installation instructions, and run the starter kit as follows:

```bash
docker compose up
```

##### For Mac users running OLLAMA locally

If you're running OLLAMA locally on your Mac (not in Docker), you need to modify the OLLAMA_HOST environment variable
in the n8n service configuration. Update the x-n8n section in your Docker Compose file as follows:

```yaml
x-n8n: &service-n8n
  # ... other configurations ...
  environment:
    # ... other environment variables ...
    - OLLAMA_HOST=host.docker.internal:11434
```

Additionally, after you see "Editor is now accessible via: <http://localhost:5678/>":

1. Head to <http://localhost:5678/home/credentials>
2. Click on "Local Ollama service"
3. Change the base URL to "http://host.docker.internal:11434/"

#### For CPU only setups:

```bash
docker compose --profile cpu up
```

