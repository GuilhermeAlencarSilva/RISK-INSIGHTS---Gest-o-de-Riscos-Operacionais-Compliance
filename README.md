# RISK INSIGHTS
## Gestão de Riscos Operacionais & Compliance

Projeto analítico sênior focado em **identificação, priorização, monitoramento e mitigação de riscos corporativos**, com base em dados simulados realistas e dashboard executivo em Power BI.

Este projeto foi desenvolvido para representar um cenário real de grandes organizações, atendendo necessidades de **governança, auditoria, compliance e tomada de decisão executiva**.

---

## 🎯 Objetivo do Projeto

Criar um **dashboard executivo** capaz de:
- Visualizar o mapa corporativo de riscos
- Avaliar a exposição total ao risco
- Monitorar incidentes e perdas financeiras
- Priorizar planos de ação
- Apoiar decisões de governança e compliance

---

## 🧠 Público-alvo

- Executivos
- Comitê de Riscos
- Auditoria Interna
- Compliance
- Gestores de Área
- Lideranças Analíticas

---

## 🛠️ Ferramentas Utilizadas

- Python (pandas, numpy)
- Power BI
- DAX
- Modelo Estrela

---

## 📈 Diferencial do Projeto

- Dados simulados **não homogêneos**
- Distribuições assimétricas
- Incidentes concentrados em riscos críticos
- Perdas financeiras com cauda longa
- Separação clara entre visão executiva e análise técnica

---

# Data Dictionary — RISK INSIGHTS

## Fato_Riscos

| Campo | Descrição |
|-----|---------|
| ID_Risco | Identificador único do risco |
| ID_Tempo | Chave para dimensão tempo |
| ID_Area | Chave para dimensão área |
| ID_Processo | Chave para dimensão processo |
| ID_TipoRisco | Chave para tipo de risco |
| ID_Impacto | Chave para nível de impacto |
| ID_Probabilidade | Chave para nível de probabilidade |
| ID_Status_Acao | Chave para status da ação |
| Score_Risco | Impacto × Probabilidade |
| Valor_Potencial_Perdido | Perda potencial estimada |
| Incidente | Indicador de ocorrência (0/1) |
| Valor_Perdido_Real | Perda financeira efetiva |
| Data_Incidente | Data do incidente |

---

## Dimensões

### Dim_Area
- ID_Area
- Area

### Dim_Processo
- ID_Processo
- Processo

### Dim_TipoRisco
- ID_TipoRisco
- Tipo_Risco

### Dim_Impacto
- ID_Impacto
- Nivel_Impacto
- Peso_Impacto

### Dim_Probabilidade
- ID_Probabilidade
- Nivel_Probabilidade
- Peso_Probabilidade

### Dim_Status_Acao
- ID_Status_Acao
- Status_Acao

### Dim_Tempo
- ID_Tempo
- Data
- Ano
- Mes
- Mes_Nome

# Modelo Estrela — RISK INSIGHTS

O projeto utiliza um **modelo estrela clássico**, garantindo:
- Performance
- Simplicidade
- Clareza analítica

## Tabela Fato
- Fato_Riscos

## Dimensões
- Dim_Tempo
- Dim_Area
- Dim_Processo
- Dim_TipoRisco
- Dim_Impacto
- Dim_Probabilidade
- Dim_Status_Acao

Todos os relacionamentos são:
- 1:N
- Direção simples (Dimensão → Fato)

📊 DASHBOARD

# Dashboard  — RISK INSIGHTS

## Página 1 — Visão Executiva de Riscos

<img width="1262" height="798" alt="pag1" src="https://github.com/user-attachments/assets/32138323-2360-4532-b061-194b240c7ce6" />

- Cards: Exposição Total, Riscos Críticos, Incidentes
- Matriz: Impacto × Probabilidade
- Barras: Riscos por Tipo

## Página 2 — Incidentes & Perdas

<img width="856" height="800" alt="pag2" src="https://github.com/user-attachments/assets/aecfb251-d077-4729-a089-9051da5e10b7" />

- Linha: Incidentes ao longo do tempo
- Barras: Perdas por Área
- Ranking: Top Processos com mais perdas

## Página 3 — Mitigação & Compliance

<img width="641" height="799" alt="pag3" src="https://github.com/user-attachments/assets/6047d1f4-5e12-4298-bfb9-9ab773111c86" />

- Barras: Status das Ações
- Colunas: % Mitigação por Área
- Tabela: Riscos sem plano de ação

## Página 4 — Análise Exploratória

<img width="1106" height="743" alt="pag4" src="https://github.com/user-attachments/assets/2b7e0b23-ed10-4fc5-8dee-5bd94db3b1bc" />

- Slicers avançados
- Drill-through por risco
- Tabela detalhada de riscos

📈 ANALISES.md

# Análises e Insights Esperados

- Riscos críticos representam pequena parcela do total
- Incidentes concentram-se em scores elevados
- Perdas financeiras seguem distribuição de cauda longa
- Nem todo risco crítico está mitigado
- Algumas áreas apresentam baixa maturidade de mitigação

Esses padrões refletem ambientes corporativos reais.

📐 MEDIDAS DAX — CONSOLIDADO FINAL

-- Total de Riscos
Total de Riscos =
COUNT ( Fato_Riscos[ID_Risco] )

-- Riscos Críticos
Riscos Críticos =
CALCULATE (
    COUNT ( Fato_Riscos[ID_Risco] ),
    Fato_Riscos[Score_Risco] >= 24
)

-- Exposição Total ao Risco
Exposição Total ao Risco =
SUM ( Fato_Riscos[Valor_Potencial_Perdido] )

-- Incidentes Ocorridos
Incidentes Ocorridos =
CALCULATE (
    COUNT ( Fato_Riscos[ID_Risco] ),
    Fato_Riscos[Incidente] = 1
)

-- Perda Financeira Total
Perda Financeira Total =
SUM ( Fato_Riscos[Valor_Perdido_Real] )

-- Perda Média por Incidente
Perda Média por Incidente =
DIVIDE (
    [Perda Financeira Total],
    [Incidentes Ocorridos]
)

-- % Riscos Mitigados
% Riscos Mitigados =
DIVIDE (
    CALCULATE (
        COUNT ( Fato_Riscos[ID_Risco] ),
        Dim_Status_Acao[Status_Acao] = "Mitigado"
    ),
    [Total de Riscos]
)

-- Score Médio de Risco (Evolução)
Score Médio de Risco =
AVERAGE ( Fato_Riscos[Score_Risco] )

👤 Autor

Projeto desenvolvido por Guilherme Alencar 
Especialista em Análise de Dados, Negócios e Visualização Executiva

📫 LinkedIn: https://www.linkedin.com/in/guilherme-alencar-327413213/ 
📊 Portfólio: https://github.com/GuilhermeAlencarSilva
