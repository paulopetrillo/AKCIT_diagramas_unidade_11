# Pré-Diagramação — Lacunas, Perguntas e Roteiro Revisado

## 1) Lacunas e ambiguidades
- L1 Nível (containers vs. componentes) não especificado.
- L2 Escopo do diagrama indefinido (núcleo vs. inclui UI/persistência/exportação).
- L3 Fronteira com infraestrutura não declarada explicitamente no template.
- L4 Dependências proibidas não preenchidas.
- L5 "O que não deve aparecer" não preenchido.
- L6 Histórico: componente interno ou separado?
- L7 Regra de universo: um componente ou estratégias individuais?
- L8 Troca de universo/undo: interfaces explícitas ou responsabilidades do Context?
- L9 Lacunas herdadas (L1/L2/L4/L11 do pipeline) afetam o diagrama.
- L10 Atores externos entram ou não em diagrama estrutural?

## 2) Perguntas de esclarecimento
1. Nível: containers ou componentes?
2. Escopo: só núcleo ou também UI/seleção/exportação?
3. Infraestrutura: fora do escopo (menção) ou componentes limítrofes?
4. Quais dependências devem ser proibidas no diagrama?
5. O diagrama deve omitir classes/métodos/atributos?
6. Histórico é componente interno ou separado?
7. Regra de universo: um componente ou estratégias individuais?
8. Lacunas L1/L2/L4/L11 já decididas? Quais respostas?

## 3) Roteiro revisado (tabela)
| Campo | O que explicar |
|---|---|
| Escopo | Entram: núcleo (Context, Strategy propriedade, Strategy universo, Selector, State, Histórico). Fora: UI, persistência, exportação, integrações. |
| Nível | Componentes (unidades internas do núcleo), não containers. |
| Limites | Núcleo não depende de UI/persistência/framework; limítrofes sem detalhes. |
| Integrações | Nenhuma confirmada; Symbolab/MathPapa/WolframAlpha são UX, não integração. |
| Restrições | Proibido: núcleo→UI/persistência/framework; propriedade→universo; seleção "a primeira que couber". Omitir classes/métodos/atributos. |
| Lacunas | L1 (2º grau), L2 (validar/sugerir), L4 (plataforma), L11 (stack), L6 (histórico), L7 (universo como componente) — anotar como pendências. |

Linhas adicionais do roteiro:
- Papéis do padrão separados (Context, Strategy×2, ConcreteStrategy, Selector, State, Histórico).
- Invariantes visíveis: seleção por ID, rastreabilidade, ortogonalidade, estado imutável.
- Fora do diagrama: formato de entrada, nível de assistência, persistência, exportação.
- Convenção: setas = dependência de contrato; limítrofes sem detalhes.
- Critério de aceite: checklist de 10 itens da Etapa 4 aplicável só pelo diagrama.