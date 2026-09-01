# 🏠 Meu HomeLab

[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat-square&logo=docker)](https://www.docker.com/)
[![Portainer](https://img.shields.io/badge/Portainer-Community%20Edition-13BEF9?style=flat-square&logo=portainer)](https://www.portainer.io/)
[![Jellyfin](https://img.shields.io/badge/Jellyfin-Media%20Server-AA1B2F?style=flat-square&logo=jellyfin)](https://jellyfin.org/)
[![Tailscale](https://img.shields.io/badge/Tailscale-VPN-grey?style=flat-square&logo=tailscale)](https://tailscale.com/)

Repositório de documentação e orquestração do meu ambiente de HomeLab. Este projeto centraliza automação de mídia, streaming e ferramentas utilitárias executadas em containers Docker.

---

## 🎯 Propósito

Centralizar e automatizar o gerenciamento da minha biblioteca de mídia (filmes, séries, animes e músicas), garantindo download automático, organização de metadados e reprodução multiplataforma com acesso seguro via VPN mesh (Tailscale).

---

## 🧩 Stack de Serviços

### 🎬 Mídia e Automação
| Serviço | Função | Porta Padrão |
| :--- | :--- | :--- |
| **Jellyfin** | Servidor de streaming e reprodução de mídia | `8096` |
| **Jellyseerr** | Interface de busca e requisição de novos títulos | `5055` |
| **Radarr** | Gerenciador e organizador de filmes | `7878` |
| **Sonarr** | Gerenciador e organizador de séries e animes | `8989` |
| **Lidarr** | Gerenciador e organizador de músicas | `8686` |
| **Prowlarr** | Gerenciador e indexador de trackers de torrent | `9696` |
| **qBittorrent** | Cliente torrent para realização dos downloads | `8080` |

### 🛠️ Gerenciamento e Utilidades
| Serviço | Função | Porta Padrão |
| :--- | :--- | :--- |
| **Portainer** | Gestão visual de containers, redes e volumes | `9000` |
| **Stirling PDF** | Conjunto completo de utilitários locais para manipulação de PDFs | `8088` |
| **Without BG** | Remoção de fundo de imagens por IA rodando 100% local | `8081` |

---

## 🚀 Como Executar

**Pré-requisitos:**
* Docker e Docker Compose instalados no host.
* Usuário adicionado ao grupo Docker.

**1. Clonar o repositório:**
```bash
git clone https://github.com/Silva-D-Romario/HomeLab.git
cd HomeLab
```

**2. Configurar variáveis de ambiente:**
```bash
cp .env.example .env
# Ajuste PUID/PGID e fuso horário se necessário
```

**3. Criar a estrutura de diretórios:**
```bash
mkdir -p Movies "Tv Shows" Animes Music downloads config/{jellyfin,jellyseerr,prowlarr,qbittorrent,radarr,sonarr,lidarr}
```

**4. Subir a stack:**
```bash
docker compose up -d
```

---

## 📚 Documentação Complementar

Para instruções aprofundadas, consulte os guias na pasta `docs/`:

* [Guia de Configuração Completo](docs/setup-guide.md)
* [Arquitetura e Fluxo de Dados](docs/architecture.md)
* [Guia de Resolução de Problemas (Troubleshooting)](docs/troubleshooting.md)
