# SYNAPSE Dashboard

**Inteligência biológica e otimização econômica para biodigestores industriais**

---

## Sobre o projeto

O Synapse é um sistema de monitoramento preditivo para biodigestores industriais. Ele combina vigilância biológica do microbioma com otimização econômica em tempo real, permitindo que operadores previnam colapsos com 2–5 dias de antecedência e maximizem receita com um clique.

Este repositório contém o **frontend completo** do dashboard — desenvolvido em HTML, CSS e JavaScript puro, sem dependências de build, pronto para rodar no browser ou integrar ao Mendix.

---

## Estrutura do arquivo

```
synapse.html          ← arquivo único, zero dependências locais
```

Dependências externas (carregadas via CDN):

| Lib | Versão | Uso |
|---|---|---|
| Chart.js | 4.4.1 | Gráficos dinâmicos (cdnjs) |
| Google Fonts | — | Syne (display) + DM Sans (body) |

---

## Telas / Abas

### 🏠 Home
Apresentação do produto e proposta de valor.

- **Hero** com call-to-action e cards flutuantes de métricas ao vivo (pH, CH₄, lucro)
- **Stats strip** com os quatro KPIs de mercado (R$ 360k perda evitável, USD 63bi mercado, +3.000 plantas, 2–5 dias de antecipação)
- **Como funciona** — 3 pilares: Monitoramento Biológico, Guard Biológico, Otimização Econômica
- **Fontes de receita** — Energia Elétrica, CBIO, Tipping Fee, Biofertilizante
- **Card de perda** — Impacto financeiro do colapso sem Synapse

### 🔬 Saúde
Dashboard de métricas biológicas em tempo real.

- **Alerta crítico** de acidificação (animado, piscando)
- **4 gauges circulares** — pH, CH₄, Temperatura, AGV — com threshold colorido (verde/vermelho)
- **Gráfico de tendência do pH** (últimas 6h) — segmento vermelho abaixo do limite 6.5 + linha tracejada de threshold
- **Painel de alertas ativos** com badge pulsante
- **Card de recomendação** com botões Aprovar / Rejeitar

### 💹 Econômico
Painel de receitas e recomendação de venda.

- **4 métricas** — Receita Energia, CBIO, Tipping Fee, Lucro líquido
- **Gráfico de barras empilhadas** (7 dias) por fonte de receita com gradientes da paleta da marca
- **Card de recomendação** com breakdown financeiro e botão de aprovação

### 📋 Histórico
Registro completo de recomendações passadas.

- **3 métricas de resumo** — total de recomendações, taxa de aprovação, receita gerada
- **Tabela filtrável** com busca por texto em tempo real
- **Gráfico de linha** de receita diária (30 dias) com animação de entrada
- **Donut chart** de resultados (aprovadas × rejeitadas) com gradiente da logo

---

## Paleta de cores

Derivada diretamente da logo Synapse:

| Token | Valor | Uso |
|---|---|---|
| `--green` | `#5fe0b4` | Indicadores saudáveis, CTAs |
| `--green-2` | `#31c48d` | Gradiente primário |
| `--green-3` | `#7ded6a` | Ponto de destaque na logo |
| `--blue` | `#2563c8` | Gradiente secundário |
| `--blue-2` | `#3b82f6` | Gráfico de linha histórico |
| `--purple` | `#8b5cf6` | Cards de recomendação |
| `--danger` | `#f4b4b5` | Alertas, pH crítico, AGV |
| `--amber` | `#f4cf75` | Status pendente |
| `--bg` | `#020907` | Fundo principal |

---

## Tipografia

| Papel | Família | Peso |
|---|---|---|
| Display / títulos | Syne | 700, 800, 900 |
| Corpo / UI | DM Sans | 300, 400, 500, 600 |

---

## Gráficos dinâmicos

Todos os gráficos são renderizados com **Chart.js 4** e animados na entrada:

| Gráfico | Tipo | Aba | Animação |
|---|---|---|---|
| Tendência pH 6h | Line com segmento colorido | Saúde | 1.2s easeInOutQuart |
| Receita 7 dias | Bar empilhado | Econômico | 1.0s easeOutQuart |
| Receita diária 30d | Line com fill | Histórico | 1.4s easeInOutCubic |
| Resultados | SVG Donut nativo | Histórico | — |
| Gauges | SVG stroke-dashoffset | Saúde | CSS transition 1s |

O pH no card flutuante da Home é **atualizado a cada 3 segundos** simulando leitura ao vivo.

---

## Como usar

### Browser direto
```bash
open synapse.html
# ou
python3 -m http.server 8000
# acesse http://localhost:8000/synapse.html
```

### Mendix
O arquivo é um snippet HTML/JS/CSS autossuficiente. Opções de integração:

1. **HTML/JavaScript Snippet widget** — cole o conteúdo do `<body>` direto no widget
2. **Snippets por aba** — divida cada `section[data-tab]` em páginas Mendix separadas
3. **Nativebridge** — adapte os `fetch()` para consumir REST APIs do Mendix

---

## Funcionalidades interativas

- ✅ Navegação por abas com estado ativo
- ✅ Inicialização lazy de gráficos (só renderiza ao entrar na aba)
- ✅ Busca/filtro ao vivo na tabela de histórico
- ✅ Botões Aprovar / Rejeitar (prontos para conectar a handlers)
- ✅ Alerta pulsante animado
- ✅ Métricas ao vivo simuladas (pH)
- ✅ Responsivo — breakpoints em 1200px e 860px

---

## Regra do Guard Biológico

Conforme o modelo de negócio do Synapse: **se o biodigestor está em colapso, nenhuma recomendação econômica é exibida.** A aba Econômico e o card de otimização só devem estar ativos quando a saúde do sistema estiver dentro dos parâmetros. Esta lógica deve ser implementada no backend/BFF ao integrar dados reais.

---

## Parâmetros monitorados

| Parâmetro | Threshold crítico | Significado |
|---|---|---|
| pH | < 6.5 | Acidificação avançada — risco imediato |
| AGV | > 4000 mg/L | Acúmulo de ácidos — precede colapso em 2–5 dias |
| CH₄ | < 50% | Queda na produção de metano |
| NH₃ | > 3000 mg/L | Inibição progressiva das bactérias |

---

## Contexto de mercado

- **USD 63 bilhões** — mercado global de biodigestores até 2037
- **6–10% a.a.** de crescimento anual
- **+3.000 novas plantas** no Brasil até 2030
- **Lei 15.042/2024** — criou o mercado regulado de carbono no Brasil, aumentando diretamente o valor dos CBIOs gerados por biodigestores

---

*Synapse — 2026*
