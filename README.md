# Software Educacional de Álgebra — Resolução de Equações por Propriedades Formais

## Descrição Resumida

Software educacional que permite ao aluno resolver equações do primeiro grau
aplicando **exclusivamente as propriedades algébricas** dos conjuntos ℕ, ℤ e ℚ
e as propriedades da igualdade. O diferencial é **evidenciar formalmente** cada
propriedade utilizada em cada transformação, eliminando terminologias informais
como "passa para o outro lado" ou "corta os termos".

O sistema **não resolve a equação pelo aluno** — ele valida e registra as
transformações que o aluno aplica, justificando cada passo pela propriedade
matemática correspondente. O conjunto universo (ℕ/ℤ/ℚ) delimita as operações
válidas e a validade da solução.

### Objetivo Pedagógico
Tornar visíveis as propriedades matemáticas que a terminologia prática esconde,
promovendo compreensão algébrica formal em vez de memorização de atalhos.

### Stakeholders
- **Participante (aluno):** resolve equações usando apenas propriedades algébricas.
- **Equipe de TI:** desenvolve o software.
- **Stakeholder pedagógico:** valida casos e justificativas (a confirmar — D12).

---

## Diagramas Produzidos

### Diagrama de Componentes (PlantUML — nível estrutural)

Representa o **núcleo de resolução** com os papéis do padrão Strategy separados:

| Elemento | Papel |
|---|---|
| `ResolvedorDeEquacao` | Context — orquestra, não conhece regras |
| `PropriedadeAlgebrica` | Strategy (contrato) — propriedades da igualdade e operacionais |
| `RegraDeUniverso` | Strategy (contrato) — regras de ℕ, ℤ, ℚ |
| `SeletorDePropriedade` | Selector — seleção determinística por ID |
| `EstadoDaEquacao` | State — canônico, imutável, versionado |
| `RegistroDePassos` | Histórico — registra ID, estado anterior e posterior |
| Catálogo de Propriedades | ConcreteStrategies extensíveis |
| Catálogo de Universos | ConcreteStrategies (ℕ, ℤ, ℚ) |

**Fronteira explícita:** o núcleo **não depende** de UI, persistência,
exportação ou integrações externas. Elementos limítrofes aparecem marcados
como `<<external>>`, sem detalhes.

**Localização:** ver código PlantUML no artefato de diagrama (`@startuml`/`@enduml`).

**Lacunas anotadas no diagrama:** L1 (2º grau), L2 (validar vs. sugerir),
L4 (plataforma/persistência), L11 (stack/legado), L6 (histórico interno),
L7 (universo como componente).

---

## Evolução do Projeto

### Etapa 1 — Elicitação e Organização de Necessidades
- Identificação de requisitos funcionais (RF01–RF13), não funcionais (RNF01–RNF11)
  e regras de negócio (RN01–RN09).
- Registro de ambiguidades e lacunas (D01–D12).
- Necessidades de design organizadas (N1–N15), com formas de validação e
  condições/restrições (C1–C12).
- **Artefatos:** `requisitos-funcionais.md`, `requisitos-nao-funcionais.md`,
  `regras-de-negocio.md`, `duvidas-e-lacunas.md`.

### Etapa 2 — Análise de Candidatos
- Levantamento de candidatos de padrão e motivos de descarte (preservados no ADR).
- **Lacuna de registro:** resumo literal dos candidatos descartados (L-ADR1)
  ainda pendente de colagem no ADR-001.

### Etapa 3 — Escolha Condicionada do Padrão
- **Hipótese adotada:** Strategy para (a) propriedades algébricas e
  (b) regras de universo, com seleção determinística e rastreável por ID.
- **Premissa de priorização:** N1, N2, N4, N7, N9 (sujeita a confirmação).
- **Trade-offs aceitos:** T1 (indireção vs. simplicidade), T2 (granularidade vs.
  explosão de estratégias), T3 (contrato de estado vs. flexibilidade).
- **Riscos reconhecidos:** R1 (lógica duplicada), R2 (seleção não determinística),
  R3 (regra de universo vazando para propriedade).

### Etapa 4 — Pseudocódigo e Checklist
- Pseudocódigo mínimo agnóstico de linguagem/framework, com papéis do padrão
  e fronteiras explícitas.
- Checklist de 10 itens para code review, cobrindo encapsulamento, acoplamento,
  testabilidade, ausência de vazamento de infraestrutura, papéis separados e
  condições de uso/não uso.

### Etapa 5 — Mini-ADR (Verificação e Registro)
- **ADR-001 — Status: Proposto.**
- Plano de verificação com 8 itens (testes, inspeção, métricas — sem números
  inventados; alvos definidos por stakeholder).
- Sinais de alerta (S1–S7) e condições monitoradas (uso/não uso/gatilhos de revisão).
- Lacunas de registro: L-ADR1 (candidatos descartados), L-ADR2 (alvos numéricos),
  L-ADR3 (critérios de aceitação), L-ADR4 (confirmação de L1/L2/L4/L11).

### Etapa 6 — Pré-Diagramação
- Identificação de 10 lacunas específicas do diagrama (L1–L10) e 8 perguntas
  de esclarecimento.
- Roteiro revisado em tabela (Escopo, Nível, Limites, Integrações, Restrições,
  Lacunas) com hipóteses de revisão declaradas.

### Etapa 7 — Diagrama de Componentes
- Diagrama PlantUML em nível de componentes, com suposições explícitas (S1–S6)
  e lacunas anotadas.
- Checklist de revisão de 12 itens focado em estrutura e dependências.

### Etapa 8 — Comparação com Análise Arquitetural Inicial (PDF)
- **Convergências:** objetivo pedagógico, relevância do conjunto universo,
  RNFs de correção/rastreabilidade/extensibilidade/testabilidade, postura
  metodológica de não inventar decisões.
- **Divergência principal:** o PDF trata 2º grau como fato; o pipeline o trata
  como lacuna não resolvida (L1/D01) e o diagrama adotou S1 (apenas 1º grau).
- **Conclusão:** o PDF é uma foto anterior ao pipeline; as etapas avançaram
  sobre ele com decisão condicionada registrada (ADR-001).

---

## Documentos do Projeto

| Documento | Conteúdo |
|---|---|
| `README.md` | Este arquivo — visão geral, diagramas e evolução. |
| `requisitos-funcionais.md` | RF01–RF13 com prioridade e rastreabilidade. |
| `requisitos-nao-funcionais.md` | RNF-A a RNF-I com condição e critério verificável. |
| `regras-de-negocio.md` | RN01–RN09 + matriz de decisão operação × universo. |
| `duvidas-e-lacunas.md` | D01–D12 com stakeholder e impacto. |
| `necessidades-design.md` | N1–N15, validação, L1–L12, C1–C12. |
| `adr-001-strategy.md` | Mini-ADR completo (Status: Proposto). |
| `pseudocodigo-strategy.md` | Pseudocódigo + checklist de 10 itens. |
| `diagrama-componentes.puml` | Código PlantUML do diagrama estrutural. |
| `pre-diagramacao.md` | Lacunas, perguntas e roteiro revisado. |
| `comparacao-pdf.md` | Diferenças entre PDF inicial e pipeline. |

---

## Status Atual

**Fase:** decisão condicionada registrada (ADR-001 Proposto) + diagrama de
componentes gerado.

**Pendências críticas antes de consolidar como "Aceito":**
- L1/D01 — escopo 1º vs. 1º+2º grau.
- L2/D02 — validar vs. sugerir propriedades.
- L4/D05 — plataforma e persistência.
- L11 — stack/legado imposto.
- L-ADR1 — colar candidatos descartados da Etapa 2.
- L-ADR2/L-ADR3 — alvos numéricos e critérios de aceitação formais.

**Gatilhos de revisão do ADR-001:** detecção de S1/S2/S3; falha em qualquer item
do plano de verificação; mudança em L1/L2/L4/L11; acúmulo de S4/S5/S6.

---

## Como Usar Este Repositório

1. Leia este `README.md` para visão geral e evolução.
2. Consulte `adr-001-strategy.md` para a decisão registrada e seu plano de verificação.
3. Use o checklist de 10 itens (`pseudocodigo-strategy.md`) como gate de code review.
4. Use o checklist de 12 itens (`diagrama-componentes.puml`) como gate de revisão estrutural.
5. Antes de avançar para implementação, resolva as pendências críticas listadas acima.