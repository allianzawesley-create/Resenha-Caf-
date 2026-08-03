# ☕ Resenha & Café

> Plataforma inteligente para descoberta, organização e análise de literatura científica.

## Visão Geral

O Resenha & Café é uma plataforma de busca científica que integra diversas bases acadêmicas em uma única interface, oferecendo resultados unificados, deduplicados e classificados por relevância.

Além da busca, a plataforma gera automaticamente:

- Resenhas críticas
- Resumos acadêmicos
- Fichamentos
- Organização bibliográfica
- Apoio à revisão de literatura

O objetivo é reduzir drasticamente o tempo necessário para localizar, avaliar e compreender artigos científicos.

---

# Objetivos

- Centralizar buscas em múltiplas bases científicas.
- Priorizar artigos relevantes.
- Evitar resultados duplicados.
- Priorizar acesso aberto (Open Access).
- Gerar análises utilizando IA.
- Oferecer uma experiência simples para pesquisadores, estudantes e professores.

---

# Arquitetura

```
Frontend (HTML/CSS/JS)
        │
        ▼
Search Worker V3 (Cloudflare Workers)
        │
        ├── OpenAlex
        ├── Semantic Scholar
        ├── Crossref
        ├── Europe PMC
        ├── SciELO
        ├── CORE
        ├── DOAJ
        ├── OpenAIRE
        ├── BASE
        ├── PubMed
        └── outras bases
        │
        ▼
Deduplicação
        ▼
Ranking Inteligente
        ▼
Cache
        ▼
Resposta ao Frontend
```

---

# Estrutura do Projeto

```
frontend/
workers/
docs/
tests/
```

---

# Componentes

## Search Worker V3

Responsável por:

- consultar múltiplas bases
- normalizar os dados
- deduplicar resultados
- aplicar filtros
- calcular ranking
- armazenar cache
- retornar JSON padronizado

---

## Review Worker

Responsável por:

- gerar resenhas críticas
- produzir resumos
- criar fichamentos
- responder perguntas sobre um artigo

---

# Bases Científicas

Atualmente o sistema suporta ou possui integração planejada para:

- OpenAlex
- Semantic Scholar
- Crossref
- Europe PMC
- SciELO
- CORE
- OpenAIRE
- BASE
- DOAJ
- PubMed
- Zenodo
- arXiv
- bioRxiv
- medRxiv
- HAL
- SSRN
- RePEc

---

# Funcionalidades

- Busca por palavras-chave
- Busca por DOI
- Busca por autor
- Busca por ano
- Busca por idioma
- Busca por acesso aberto
- Busca por tipo de documento
- Ranking por relevância
- Deduplicação inteligente
- Cache
- Geração de resenha crítica
- Exportação futura para BibTeX, RIS e ABNT

---

# Roadmap

## Fase 1

- Arquitetura
- Documentação
- Search Worker V3

## Fase 2

- Integração SciELO
- Integração CORE
- Integração DOAJ

## Fase 3

- Ranking Inteligente

## Fase 4

- IA para análise metodológica

## Fase 5

- Exportação bibliográfica

## Fase 6

- Dashboard do pesquisador

---

# Tecnologias

- Cloudflare Workers
- JavaScript
- HTML5
- CSS3
- Cloudflare Cache API
- OpenRouter
- APIs científicas

---

# Princípios do Projeto

Todo novo código deve seguir estas regras:

1. Código modular.
2. Funções pequenas e reutilizáveis.
3. Nunca duplicar lógica.
4. Sempre documentar funções públicas.
5. Priorizar desempenho.
6. Priorizar APIs gratuitas.
7. Reduzir consumo de tokens.
8. Manter compatibilidade com o frontend existente.
9. Sempre normalizar dados antes do ranking.
10. Todo novo recurso deve ser facilmente extensível.

---

# Licença

Projeto proprietário.

Todos os direitos reservados.
