# Arquitetura e Fluxo de Dados

Visão técnica sobre a integração dos serviços da stack `*arr` com o Jellyfin e utilitários.

---

## 🎬 Diagrama de Automação de Mídia

```text
┌─────────────────────────────────────────────────────────────┐
│                    Usuário Final                            │
└───────────────┬─────────────────────────────▲───────────────┘
                │                             │
    1. Solicita filme/série          6. Reproduz streaming
                ▼                             │
┌───────────────────────────────┐             │
│          Jellyseerr           │             │
└───────────────┬───────────────┘             │
                │                             │
    2. Envia pedido                           │
                ▼                             │
┌───────────────────────────────┐             │
│   Radarr (Filmes) / Sonarr    │             │
└───────────────┬───────────────┘             │
                │                             │
    3. Busca releases                         │
                ▼                             │
┌───────────────────────────────┐             │
│           Prowlarr            │             │
└───────────────┬───────────────┘             │
                │                             │
    4. Envia .torrent / magnet                │
                ▼                             │
┌───────────────────────────────┐             │
│          qBittorrent          │             │
└───────────────┬───────────────┘             │
                │                             │
    5. Salva arquivo e notifica               │
                ▼                             │
┌───────────────────────────────┐             │
│           Jellyfin            ├─────────────┘
└───────────────────────────────┘
```

---

## 🗂️ Mapeamento de Volumes e Persistência

| Container | Origem no Host | Destino no Container | Finalidade |
| :--- | :--- | :--- | :--- |
| `jellyfin` | `./config/jellyfin` | `/config` | Banco de dados e metadados |
| `jellyfin` | `./Movies`, `./Tv Shows`, `./Animes`, `./Music` | `/media/*` | Leitura de mídia |
| `radarr` | `./config/radarr` | `/config` | Configurações do app |
| `radarr` | `./Movies` | `/media/Movies` | Destino final dos filmes |
| `radarr` | `./downloads` | `/downloads` | Acesso ao download temporário |
| `sonarr` | `./config/sonarr` | `/config` | Configurações do app |
| `sonarr` | `./Tv Shows`, `./Animes` | `/media/*` | Destino final das séries |
| `sonarr` | `./downloads` | `/downloads` | Acesso ao download temporário |
| `qbittorrent` | `./downloads` | `/downloads` | Gravação dos arquivos baixados |
| `portainer` | `portainer_data` (volume Docker) | `/data` | Configuração interna da UI |

---

## 🔌 Integrações por API

* **Prowlarr ➔ Sonarr/Radarr/Lidarr:** Gerencia e sincroniza indexers automaticamente via API Token.
* **Sonarr/Radarr/Lidarr ➔ qBittorrent:** Comunicação direta via Web UI API (porta 8080) para disparo e monitoramento de downloads.
* **Jellyseerr ➔ Jellyfin:** Sincronização de bibliotecas e contas de usuários via API Key do Jellyfin.
