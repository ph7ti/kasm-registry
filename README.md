# Kasm Workspaces — Third-Party Registry

A public **Kasm Workspaces registry (schema 1.1)** with 420 Portainer app
templates prepared as ephemeral Protected Web Apps. Add it to Kasm and launch a
workspace without cloning or converting the original Portainer sources.

**Registry URL**

```
https://ph7ti.github.io/kasm-registry/
```

Add it in **Admin → Workspaces → Registry → Add new** (no `/1.1` suffix).

## What it provides

- 420 browser workspaces named `Teste: …` (Nextcloud, Gitea, Uptime Kuma,
  AdGuard, MinIO, and hundreds more).
- Each workspace opens `kasmweb/chrome` in kiosk mode against a waiting page.
- The waiting page polls the application every 2 seconds and redirects when the
  backend is ready: no more “site can’t be reached” on the first click.
- A Docker orchestrator on the Kasm agent starts the app container (named after
  the workspace slug) on `kasm_default_network` and removes it when the last
  session ends. Runtime code, tests and deployment docs live in the main
  project:

  https://github.com/ph7ti/portainer-templates-to-kasm

## Repository layout

```
site/
├── versions.txt        # 1.1
├── list.json           # registry catalog
├── index.html          # redirect for humans
├── backend_manifest.json
└── 1.1/
    ├── list.json
    ├── icons/
    └── workspaces/<slug>/workspace.json
```

`site/` is published to GitHub Pages by [deploy-pages.yml](.github/workflows/deploy-pages.yml).

## Requirements

- Kasm Workspaces 1.19.x (schema 1.1).
- `kasm-wait` container on the Kasm workspace network (waiting page).
- The backend orchestrator from the main project running on the Docker host.
- Kasm image creation/installation for the workspaces you want to launch
  (`tools/publish_images_to_kasm.py` in the main project).

Without the orchestrator and waiter, the registry is still valid but the
browser workspaces will not find the app containers.

## What this is not

- It is not a Kasm build with multiple containers per session. Kasm still runs
  one browser container per session; the app runs in a second container managed
  externally.
- It is not a rebuild of the app images. Original upstream images are used
  as-is.
- It does not provide per-user isolated app state for the same workspace; one
  app container is shared by concurrent sessions of that workspace (reference
  counted and removed when the last session ends).

## Português

Registry público de **terceiros** para o Kasm Workspaces, com 420 templates de
aplicações do catálogo Portainer convertidos para Protected Web Apps efêmeros.
Adicione a URL `https://ph7ti.github.io/kasm-registry/` em
**Admin → Workspaces → Registry → Add new** — não é preciso clonar nem
converter os repositórios de origem.

A página de espera exibida no navegador verifica o backend a cada 2 segundos e
redireciona quando ele responde. O orquestrador do projeto principal
(https://github.com/ph7ti/portainer-templates-to-kasm) cria e remove o contêiner
da aplicação.

## Attribution

Templates and logos belong to their original authors
([lissy93/portainer-templates](https://github.com/lissy93/portainer-templates)
and the upstream template maintainers). The registry metadata and automation
are MIT licensed.
