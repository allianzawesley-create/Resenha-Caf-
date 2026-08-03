# Projeto: Search Worker V3 (Resenha & Café)

## 1. O Propósito do Projeto
Este é o backend de um motor de busca científica inteligente. Ele agrega, deduplica e ranqueia artigos de 6 bases de dados (OpenAlex, Semantic Scholar, Crossref, Europe PMC, SciELO, CORE) para alimentar uma plataforma de resenhas acadêmicas.

## 2. Stack Tecnológica
- **Runtime:** Cloudflare Workers (JavaScript/TypeScript)
- **APIs:** OpenAlex, Semantic Scholar, CORE, SciELO, Europe PMC, Crossref
- **Armazenamento:** Cache do Cloudflare para pesquisas (TTL de 30 minutos)
- **Monitoramento:** Endpoints `/health` e `/usage`

## 3. Estrutura do Código (A Base)
- `src/index.js`: Entry point do Worker, define as rotas (`/work`, `/health`, `/usage`).
- `src/modules/`: Arquivos modulares para cada fonte de dados.
    - `openalex.js`, `semantic.js`, `core.js`, `scielo.js`, `europepmc.js`, `crossref.js`.
- `src/modules/ranking.js`: Lógica que pontua e ordena os resultados (por citações, acesso aberto, etc.).
- `src/modules/cache.js`: Gerencia o armazenamento e a recuperação das pesquisas.
- `src/modules/deduplication.js`: Remove artigos duplicados usando DOI e similaridade de título.
- `src/modules/merge.js`: Combina dados de diferentes APIs em um único registro.
- `src/utils/`: Funções auxiliares para logging, validação, etc.

## 4. Padrões e Convenções de Código
- **Async/Await:** Use `async/await` para todas as chamadas de API e manipulação de promises, para garantir que o código seja limpo e não bloqueante.
- **Tratamento de Erros:** Todas as chamadas de API devem ser envolvidas em `try...catch`. Se uma API falhar, o Worker deve falhar silenciosamente (logar o erro) e tentar a próxima API. O usuário final nunca deve ver um erro 5xx por falha de uma API específica.
- **Safe Mode:** Qualquer alteração no consumo de API deve respeitar a lógica do "Safe Mode" no `openalex.js`.
- **Formatação:** Use `Prettier` com as configurações padrão.
- **Comentários:** Comente a lógica de negócio, não o óbvio. Explique *por que* uma decisão foi tomada (ex: "Priorizamos a busca em cache para reduzir custos").

## 5. Comandos Essenciais para o Desenvolvimento
```bash
# Rodar localmente (simulando o ambiente do Cloudflare)
wrangler dev

# Publicar o Worker no Cloudflare
wrangler publish

# Rodar os testes (assumindo que você usará um framework de teste)
npm test

# Verificar a sintaxe e formatação
npm run lint