

## 📋 DIRETIVAS DO PROJETO E REGRAS DE CÓDIGO
# Regras
- Use princípios de Clean Code.
- Comente lógicas complexas.


## 🧠 MEMÓRIA DE CONTEXTO ISOLADO (APPHUB)
## 2026-04-10 — Biome 2.x + Vitest (v04.00.08)
- Biome 2.x adicionado (lint + format — antes sem qualquer lint/format)
- Vitest 4.1.4 adicionado (antes sem framework de testes)
- vite 8.0.7 → 8.0.8
- Dependabot groups: @vitest/* e @biomejs/* adicionados

# AI Memory Log - apphub

## 2026-04-17 — AppHub v04.00.10 (Pages observability rollback after GHA failure)
### Escopo
Hotfix de deploy no `apphub` após o GitHub Actions confirmar que `observability` não é suportado em config de Cloudflare Pages.
### Alterado
- `wrangler.json` deixou de declarar `observability` por ser config de Pages.
### Motivação
- Restaurar o deploy do `apphub` sem reintroduzir configuração inválida para Pages.
### Versão
- APP v04.00.09 → APP v04.00.10

## 2026-04-17 — AppHub v04.00.09 (wrangler observability + traces)
### Escopo
Padronização do baseline de observabilidade Cloudflare no `apphub`.
### Alterado
- `wrangler.json` agora garante `observability.logs.enabled = true`, `observability.logs.invocation_logs = true` e `observability.traces.enabled = true`.
- `src/App.tsx`, `src/main.tsx`, `src/components/ComplianceBanner.tsx`, `src/modules/compliance/LicencasModule.tsx` e `package.json` foram saneados para o Biome atual, preservando a UX intencional dos cards e removendo bloqueios preexistentes do gate local.
### Motivação
- Alinhar o app ao padrão operacional do workspace para logs de invocação e traces.
### Versão
- APP v04.00.08 → APP v04.00.09


## 2026-04-08 — Restauração: Card URL Status Bar Suppression
### Escopo
Restaurada funcionalidade que impede exibição da URL na barra de status do browser ao hover nos cards.
### Feito
- Componente `Card` migrado de `<a href>` para `<div role="link">` com `onClick` → `window.open()`.
- Acessibilidade mantida: `tabIndex={0}`, `onKeyDown` (Enter/Space), `role="link"`, `aria-label`.
### Versão
- APP v04.00.06 → APP v04.00.07

## 2026-04-08 — GitHub Actions Purge & Dependabot Standardization
### Escopo
Auditoria completa de CI/CD para eliminação de "ghost runs" em toda a rede de repositórios do workspace, juntamente com a universalização da configuração do Dependabot ajustada às necessidades de empacotamento locais para mitigar tráfego e limites no API.


## 2026-04-03 — Cloudflare Paid Scale Integration
### Escopo
Migração arquitetural unificada para aproveitamento da infraestrutura Cloudflare Paid. Implementação de **Smart Placement** transversal para redução de latência via proximidade física com o banco de dados (BIGDATA_DB). Adoção da diretiva `usage_model: unbound` para mitigar o `Error 1102` (CPU limit excess). Embutimento global do proxy **Cloudflare AI Gateway** sobrepondo o SDK nativo (`@google/genai`) e habilitando Caching, Rate limiting Nativo e Observabilidade Unificada, mantendo operação híbrida com os LLMs da rede.

### Diretivas Respeitadas
- Conformidade 100% com `wrangler.json`.
- `tlsrpt-motor` e `cron-taxa-ipca` revalidados em infraestrutura moderna sem timeout.

## 2026-03-28 — AppHub v04.00.00 — Migração Arquitetural Completa (React 19 + TypeScript + Vite)
### Alterado (MAJOR)
- **Stack**: migrado de HTML estático + JS vanilla + CSS para **React 19 + TypeScript 5.9 + Vite 8**.
- **Componentização**: `public/app.js` + `public/index.html` decompostos em `src/App.tsx` + `src/types.ts` + `src/main.tsx`.
- **CSS preservado**: design system tiptap.dev (Google Blue) portado 1:1 para `src/App.css`.
- **Build**: 194KB JS (61KB gzip), 6.5KB CSS (2KB gzip), 16 módulos, <1s.
- **Deploy**: `deploy.yml` com `setup-node` + `npm ci` + `npm run build`.
- **Dependabot**: seção `npm` adicionada ao `dependabot.yml`.
### Removido
- `public/app.js`, `public/index.html`, `public/styles.css`.
### Preservado
- `functions/api/config.js`, `public/cards.json`, `public/favicon.svg`, `public/_headers`.
### Controle de versão
- `apphub`: APP v03.04.00 → APP v04.00.00

## 2026-03-26 — AdminHub v01.05.00 + AppHub v03.04.00 — UI/UX Redesign (tiptap.dev, Google Blue)

### Escopo
- **Ambos apps** receberam redesign completo do CSS seguindo design language do tiptap.dev.
- Paleta: violet/pink → Google Blue `#1a73e8`. Background: warm gray `#f5f4f4`. Texto: `#0d0d0d`.
- Glassmorphism pesado removido → superfícies sólidas brancas com shadows `0 1px 3px`.
- Hero/footer pill-shaped (100px radius). Cards 30px radius. Orbs mais sutis (opacity 0.25, blur 100px).
- `Inter` via Google Fonts adicionada a ambos `index.html`.
- Favicon admin SVG (gear+monitor) adicionado a ambos.
- WCAG/eMAG: focus-visible `#1a73e8`, skip-link, reduced-motion, dark mode preservados.

### Controle de versão
- `adminhub`: v01.04.02 → v01.05.00.
- `apphub`: v03.03.01 → v03.04.00.

## 2026-04-03 — Enforcing Canonical Domain Security & TypeScript Audit
### Escopo
Implementação de bloqueio em Edge para impedir a exposição pública de roteamentos sob o domínio interno `*.pages.dev`. Aplicado redirect mandatório (301) para os domínios canônicos definidos (`lcv.app.br` e suas ramificações) em todos os apps com exceção dos puramente internos, protegendo infraestrutura e performance SEO. Também foram resolvidos erros de compilação (`Unexpected any`) e typings TypeScript do motor do editor Post no `admin-app` referentes a integração Word Mammoth, bem como a injeção Cloudflare `PagesFunction` em `mainsite-frontend`.

### Controle de versão
- `admin-app`: APP v01.77.31 → APP v01.77.32
- `oraculo-financeiro`: APP v01.08.00 → APP v01.08.01
- `astrologo-app`: APP v02.17.02 → APP v02.17.03
- `mainsite-frontend`: APP v03.04.14 → APP v03.04.15
- `calculadora-app`: middleware deployment, versioning handled internally
- `apphub`: middleware deployment, versioning handled internally
- `adminapps`: middleware deployment, versioning handled internally



> **DIRETIVA DE SEGURANÇA:** Ao sugerir código ou responder perguntas, leia rigorosamente o contexto e as memórias históricas acima para não divergir das decisões já tomadas pelo outro agente.
