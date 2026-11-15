# DragonZord — Teste 1

**Instância prática** do ecossistema DragonZord: painel centralizador de homologação para os **24 agentes
e frameworks de IA open-source** mapeados no vídeo de referência de André Lug.

O Teste 1 é derivado do molde coringa [`DragonZord Teste Zero`](https://github.com/renatosfcontador-ops/grupo-reis-dragonzord-teste-zero).
Ele mantém a mesma arquitetura leve: front-end responsivo, back-end sem dependências e catálogo JSON
centralizado. O painel funciona como **cordão umbilical** para os repositórios oficiais, demonstrações,
vídeos e notebooks de teste — sem clonar código pesado para a máquina local.

> **Regra de isolamento:** todo processamento pesado (Python, GPU, embeddings, motores locais) vai para
> notebooks do Kaggle. A infraestrutura de produção da AWS permanece 100% blindada e intocada.

---

## 1. Como rodar

```bash
npm start
# abra http://localhost:3000
```

Requisitos: Node.js 18+. Não é necessário `npm install`.

### Modo estático

A raiz do repositório é 100% estática. Publique no GitHub Pages ou em qualquer host estático. Sem
back-end, o painel usa `localStorage` para relatórios e overrides.

---

## 2. Estrutura

```
dragonzord-teste-1/
├── index.html                  # grid, relatórios, Kaggle e configurações
├── assets/
│   ├── styles.css              # tema "Zord"
│   └── app.js                  # render, filtros, modal, relatórios, overrides
├── projects.json               # 24 projetos + 4 categorias
├── server.js                   # back-end leve
├── package.json                # sem dependências
├── docs/
│   ├── ARCHITECTURE.md
│   ├── CATALOG.md              # lista dos 24 projetos
│   ├── INSTANCE-GUIDE.md
│   └── KAGGLE.md
├── reports/
│   └── README.md
└── .github/workflows/deploy-pages.yml
```

---

## 3. Os 24 projetos

| # | Projeto | Categoria | Repositório |
| --- | --- | --- | --- |
| 01 | OpenClaw | Navegador | https://github.com/openclaw/openclaw |
| 02 | Hermes Agent | Navegador | https://github.com/NousResearch/hermes-agent |
| 03 | Browser Use | Navegador | https://github.com/browser-use/browser-use |
| 04 | Stagehand | Navegador | https://github.com/browserbase/stagehand |
| 05 | Skyvern | Navegador | https://github.com/Skyvern-AI/skyvern |
| 06 | Nanobrowser | Navegador | https://github.com/nanobrowser/nanobrowser |
| 07 | Agent S | Navegador | https://github.com/simular-ai/Agent-S |
| 08 | CrewAI | Multi-Agent | https://github.com/crewAIInc/crewAI |
| 09 | AutoGen | Multi-Agent | https://github.com/microsoft/autogen |
| 10 | LangGraph | Multi-Agent | https://github.com/langchain-ai/langgraph |
| 11 | MetaGPT | Multi-Agent | https://github.com/FoundationAgents/MetaGPT |
| 12 | OpenAI Agents SDK | Multi-Agent | https://github.com/openai/openai-agents-python |
| 13 | AutoGPT | Multi-Agent | https://github.com/Significant-Gravitas/AutoGPT |
| 14 | OpenHands | Multi-Agent | https://github.com/OpenHands/OpenHands |
| 15 | SuperAGI | Multi-Agent | https://github.com/TransformerOptimus/SuperAGI |
| 16 | mem0 | Memória | https://github.com/mem0ai/mem0 |
| 17 | Letta | Memória | https://github.com/letta-ai/letta |
| 18 | Zep | Memória | https://github.com/getzep/zep |
| 19 | Graphiti | Memória | https://github.com/getzep/graphiti |
| 20 | Cognee | Memória | https://github.com/topoteretes/cognee |
| 21 | Langflow | Low-Code | https://github.com/langflow-ai/langflow |
| 22 | Flowise | Low-Code | https://github.com/FlowiseAI/Flowise |
| 23 | Dify | Low-Code | https://github.com/langgenius/dify |
| 24 | n8n | Low-Code | https://github.com/n8n-io/n8n |

A lista completa com demos, vídeos e tags está em [`docs/CATALOG.md`](docs/CATALOG.md).

---

## 4. Fluxo de homologação

1. Filtre o grid por categoria ou busque por nome.
2. Clique em **Testar interface**.
3. Abra o repositório, a demo, o vídeo ou o atalho Kaggle.
4. Registre **veredito** (`aprovado`, `patina`, `reprovado`, `pendente`), nota de usabilidade (0-5) e
   observações objetivas.
5. O status do card passa a refletir o último veredito.

O objetivo é responder rápido: **o projeto entrega valor operacional ou patina em excesso de botões e
complexidade visual?**

---

## 5. Relatórios

- Aba **Relatórios de Teste**: formulário + histórico.
- Exportação em JSON e CSV.
- Com servidor: `reports/reports.json`.
- Sem servidor: `localStorage`.
- A pasta `reports/` contém apenas relatórios e logs de homologação.

---

## 6. Kaggle Sandbox

A aba **Kaggle Sandbox** reúne:

- link para criar um notebook novo;
- atalho por projeto;
- checklist de isolamento;
- regra de nunca usar credenciais ou recursos de produção da AWS.

Detalhes em [`docs/KAGGLE.md`](docs/KAGGLE.md).

---

## 7. Deploy

### GitHub Pages

O workflow `.github/workflows/deploy-pages.yml` publica a raiz do repositório na branch `main`.
Ative **Settings → Pages → Source: GitHub Actions**.

### Servidor Node

Publique em Render, Railway, Fly.io ou VM. Configure `PORT` por variável de ambiente.

---

## 8. API

| Método | Rota | Descrição |
| --- | --- | --- |
| `GET` | `/api/health` | status do serviço |
| `GET` | `/api/projects` | catálogo de 24 projetos |
| `GET` | `/api/reports` | lista relatórios |
| `POST` | `/api/reports` | cria relatório |
| `DELETE` | `/api/reports?id=` | remove relatório |
| `GET` | `/api/urls` | lê overrides |
| `PUT` | `/api/urls` | salva overrides |

---

## 9. Governança

- Catálogo em `projects.json`: editável por qualquer IA ou desenvolvedor.
- Relatórios e overrides em `reports/`, ignorados pelo Git.
- Nenhum binário, dependência pesada ou credencial no repositório.
- O Teste Zero é a fonte do molde; o Teste 1 é a primeira instância prática.

---

## 10. Acesso

O painel abre com um overlay de login. A sessão é guardada em `localStorage` na chave `dragonzord_auth`;
para encerrar, use **Configurações → Sair / Encerrar sessão**.

> **Aviso de segurança:** por ser um site estático no GitHub Pages, a validação é client-side e pode ser
> inspecionada ou contornada por quem tem o link. Para proteção real, use Cloudflare Access, GitHub OAuth
> ou um back-end autenticado.

## 11. Licença

MIT.