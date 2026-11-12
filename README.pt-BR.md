# Kasm Workspaces — Registry de Terceiros

Registry público para **Kasm Workspaces (schema 1.1)** com 420 templates de
aplicações do Portainer preparados como Protected Web Apps efêmeros. Adicione a
URL no Kasm e lance o workspace, sem clonar nem converter as fontes originais.

**URL do registry**

```
https://ph7ti.github.io/kasm-registry/
```

Adicione em **Admin → Workspaces → Registry → Add new** (sem `/1.1`).

## O que é fornecido

- 420 workspaces de navegador chamados `Teste: …`.
- Cada workspace abre o `kasmweb/chrome` em kiosk contra uma página de espera.
- A página verifica o backend a cada 2 segundos e redireciona quando ele
  responde.
- O orquestrador no host Docker do Kasm cria o contêiner da aplicação (nome =
  slug do workspace) na rede `kasm_default_network` e o remove quando a última
  sessão termina. Código, testes e deploy ficam no projeto principal:

  https://github.com/ph7ti/portainer-templates-to-kasm

## Estrutura

```
site/
├── versions.txt
├── list.json
├── index.html
├── backend_manifest.json
└── 1.1/
    ├── list.json
    ├── icons/
    └── workspaces/<slug>/workspace.json
```

## Requisitos

- Kasm Workspaces 1.19.x (schema 1.1).
- Contêiner `kasm-wait` na rede dos workspaces (página de espera).
- Orquestrador do projeto principal em execução no host Docker.
- Instalação das imagens dos workspaces que serão lançados
  (`tools/publish_images_to_kasm.py` no projeto principal).

Sem o orquestrador e o waiter, o registry continua válido, mas o navegador não
encontrará os contêineres das aplicações.

## O que não é

- Não é um Kasm com múltiplos contêineres por sessão; o Kasm continua com um
  contêiner de navegador por sessão e a aplicação fica em um segundo contêiner.
- Não rebuilda imagens dos apps; usa as imagens originais.
- Não oferece estado isolado por usuário para o mesmo workspace; um contêiner
  da aplicação é compartilhado por sessões simultâneas (com contagem de
  referência e remoção ao final).

## English

Public third-party Kasm registry with 420 Portainer app templates. Add
`https://ph7ti.github.io/kasm-registry/` to **Admin → Workspaces → Registry**
and launch a `Teste: …` workspace. A waiting page polls the backend every 2 s
and redirects when it is ready; the orchestrator from
https://github.com/ph7ti/portainer-templates-to-kasm manages the app container.

## Atribuição

Templates e logos pertencem aos autores originais
([lissy93/portainer-templates](https://github.com/lissy93/portainer-templates)
e mantenedores upstream). Os metadados do registry e a automação são MIT.
