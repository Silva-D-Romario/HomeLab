# 🏠 Meu HomeLab

[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat-square&logo=docker)](https://www.docker.com/)
[![Portainer](https://img.shields.io/badge/Portainer-Community%20Edition-13BEF9?style=flat-square&logo=portainer)](https://www.portainer.io/)
[![Jellyfin](https://img.shields.io/badge/Jellyfin-Media%20Server-AA1B2F?style=flat-square&logo=jellyfin)](https://jellyfin.org/)

Bem-vindo ao meu laboratório caseiro! Este repositório documenta a configuração completa dos serviços que utilizo para criar um ambiente de mídia e utilidades pessoais, tudo orquestrado com **Docker Compose** e gerenciado pelo **Portainer**.

## 🎯 Propósito

Centralizar e automatizar o gerenciamento da minha biblioteca de mídia (filmes, séries, animes e músicas), garantindo acesso fácil de qualquer dispositivo, tanto dentro de casa quanto remotamente com segurança, além de oferecer ferramentas úteis para o dia a dia.

## 🧩 Stack de Serviços

### 🎬 Mídia e Automação
| Serviço | Descrição | Porta |
| :--- | :--- | :--- |
| **Jellyfin** | Servidor de mídia para organizar e reproduzir filmes, séries e músicas. | `8096` |
| **Jellyseerr** | Interface para solicitar e gerenciar novos conteúdos. | `5055` |
| **Sonarr** | Gerenciador de séries de TV. | `8989` |
| **Radarr** | Gerenciador de filmes. | `7878` |
| **Lidarr** | Gerenciador de música. | `8686` |
| **Prowlarr** | Agregador de indexadores para busca de conteúdo. | `9696` |
| **qBittorrent** | Cliente BitTorrent para downloads. | `8080` |

### 🛠️ Gerenciamento e Utilidades
| Serviço | Descrição | Porta |
| :--- | :--- | :--- |
| **Portainer** | Interface web para gerenciar o Docker e os containers. | `9000` |
| **Stirling PDF** | Ferramenta completa para manipulação de PDFs (mesclar, dividir, comprimir, etc.). | `8088` |
| **Without BG** | Remoção de fundo de imagens utilizando IA localmente. | `8081` |

## 🛠️ Como Usar

**Pré-requisitos:**
- Docker e Docker Compose instalados.
- (Opcional) Tailscale para acesso remoto seguro.

**Passos:**

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/Silva-D-Romario/HomeLab.git
   cd HomeLab