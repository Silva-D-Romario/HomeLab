# Guia de Configuração do Homelab

Passo a passo para replicar a instalação do sistema base, dependências e inicialização dos serviços.

---

## 🐧 1. Sistema Operacional e Dependências

Recomenda-se o **Ubuntu Server 22.04 LTS** (ou superior) ou qualquer distribuição baseada em Debian.

```bash
# 1. Atualizar repositórios
sudo apt update && sudo apt upgrade -y

# 2. Instalar Docker e utilitários
sudo apt install -y docker.io docker-compose-v2 curl git

# 3. Habilitar o serviço do Docker
sudo systemctl enable --now docker

# 4. Permitir execução sem root
sudo usermod -aG docker $USER
newgrp docker
```

---

## 📁 2. Estrutura do Diretório

A organização do projeto separa configurações persistentes dos arquivos de mídia brutos:

```text
HomeLab/
├── docker-compose.yml
├── .env
├── docs/
├── config/             # Dados persistentes de cada container
│   ├── jellyfin/
│   ├── jellyseerr/
│   ├── prowlarr/
│   ├── qbittorrent/
│   ├── radarr/
│   └── sonarr/
├── downloads/          # Área temporária do qBittorrent
├── Movies/             # Biblioteca de filmes
├── Tv Shows/           # Séries de TV
├── Animes/             # Animes
└── Music/              # Biblioteca de músicas
```

Criação rápida das pastas e ajuste de permissões:

```bash
mkdir -p Movies "Tv Shows" Animes Music downloads config/{jellyfin,jellyseerr,prowlarr,qbittorrent,radarr,sonarr,lidarr}
sudo chown -R $UID:$GID Movies "Tv Shows" Animes Music downloads config
```

---

## 🔒 3. Acesso Remoto com Tailscale

Para acessar o painel de qualquer lugar sem abrir portas no roteador (port forwarding):

```bash
# Instalação do Tailscale
curl -fsSL https://tailscale.com/install.sh | sh

# Autenticação na sua tailnet
sudo tailscale up
```

Após autenticado, os serviços estarão acessíveis via IP fornecido pela Tailscale: `http://<SEU-IP-TAILSCALE>:<PORTA>`.

---

## 🌐 4. Tabela de Acesso aos Serviços

| Serviço | URL Local | URL Remota (Tailscale) |
| :--- | :--- | :--- |
| **Jellyfin** | `http://localhost:8096` | `http://<IP-TAILSCALE>:8096` |
| **Jellyseerr** | `http://localhost:5055` | `http://<IP-TAILSCALE>:5055` |
| **Sonarr** | `http://localhost:8989` | `http://<IP-TAILSCALE>:8989` |
| **Radarr** | `http://localhost:7878` | `http://<IP-TAILSCALE>:7878` |
| **Lidarr** | `http://localhost:8686` | `http://<IP-TAILSCALE>:8686` |
| **Prowlarr** | `http://localhost:9696` | `http://<IP-TAILSCALE>:9696` |
| **qBittorrent** | `http://localhost:8080` | `http://<IP-TAILSCALE>:8080` |
| **Portainer** | `http://localhost:9000` | `http://<IP-TAILSCALE>:9000` |
| **Stirling PDF** | `http://localhost:8088` | `http://<IP-TAILSCALE>:8088` |
| **Without BG** | `http://localhost:8081` | `http://<IP-TAILSCALE>:8081` |
