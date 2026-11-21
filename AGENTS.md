# Gerador de orçamento (projeto de teste)

Projeto pequeno em Python para calcular e formatar orçamentos de freelance.
Objetivo real: testar o fluxo com vários agentes de IA, cada um na sua branch.

## Stack e comandos
- Python 3.11+, sem dependências externas (exceto pytest para testes).
- Verificação: `python -m pytest` (rodar na raiz do projeto).
- Nunca diga que os testes passaram sem ter rodado o comando e visto a saída.

## Arquivos e donos
| Arquivo | Dono | Observação |
|---|---|---|
| `orcamento.py` | Agente de código (Claude) | Funções abaixo, exatamente com estas assinaturas |
| `test_orcamento.py` | Agente de testes (Codex) | Testa só o que está especificado aqui |
| `README.md` | Agente de docs (Hermes) | Instruções de uso baseadas nesta especificação |

REGRA: altere somente o arquivo que é seu. Se achar que precisa mexer em outro,
pare e avise em vez de editar.

## Especificação (contrato — não mude assinaturas)

Um item é um dict: `{"descricao": str, "horas": float, "valor_hora": float}`.

### `calcular_total(itens: list[dict]) -> float`
- Soma `horas * valor_hora` de todos os itens, arredondado a 2 casas.
- Lista vazia retorna `0.0`.
- `horas` ou `valor_hora` negativos levantam `ValueError`.
- Exemplo: itens `[{"descricao": "Site", "horas": 10, "valor_hora": 50},
  {"descricao": "Ajustes", "horas": 2.5, "valor_hora": 40}]` retorna `600.0`.

### `aplicar_desconto(total: float, percentual: float) -> float`
- `percentual` entre 0 e 100 (inclusive). Retorna `round(total * (1 - percentual / 100), 2)`.
- `percentual` fora de 0–100 ou `total` negativo levantam `ValueError`.
- Exemplo: `aplicar_desconto(600.0, 10)` retorna `540.0`.

### `formatar_valor(valor: float) -> str`
- Formato brasileiro: `R$` + espaço, milhar com ponto, decimal com vírgula, 2 casas.
- Exemplos: `formatar_valor(1234.5)` retorna `"R$ 1.234,50"`;
  `formatar_valor(0)` retorna `"R$ 0,00"`.

## Regras gerais
- Não adicione dependências nem crie arquivos novos além dos listados.
- Commits pequenos, na sua própria branch (`agente/<nome>`). Nunca commite na `main`.
- Se a especificação estiver ambígua, pergunte; não invente comportamento.
