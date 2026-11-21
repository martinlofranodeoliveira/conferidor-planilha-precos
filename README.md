# Conferidor de Planilha de Preços

Compare subtotais declarados com quantidade vezes preço unitário e sinalize referências ultrapassadas.

## Como usar

Abra a [demonstração](https://martinlofranodeoliveira.github.io/conferidor-planilha-precos/). Para uso local, execute `python3 -m http.server 8000` no diretório e abra `http://localhost:8000`.

Preencha os itens com quantidade, preço unitário, total informado e referência. Clique em **Conferir preços** para ver diferenças de cálculo e itens acima da referência. O relatório está disponível em CSV.

## Contrato público

input é objeto com items array de até 100 objetos {id,quantity,unitCents,declaredCents,referenceUnitCents?}. id tem 1 a 32 caracteres ASCII alfanuméricos, hífen ou sublinhado, sem repetir. quantity é inteiro de 0 a 10000, unitCents e referenceUnitCents são inteiros de 0 a 10000000 e declaredCents é inteiro de 0 a 100000000000. referenceUnitCents ausente ou null significa sem referência. Entrada inválida retorna exatamente {error:"INVALID_INPUT"}.
Retorne {rows,summary}. rows segue a ordem de items e contém {id,computedCents,declaredCents,differenceCents,referenceCents,totalMismatch,aboveReference}. computedCents=quantity*unitCents, differenceCents=declaredCents-computedCents, referenceCents=referenceUnitCents ou null. totalMismatch marca diferença não zero; aboveReference é comparação estrita de unitCents à referência presente, mesmo que quantity=0. summary tem computedCents e declaredCents somados, totalMismatches e aboveReference (contagens).

## Escopo

Demonstração offline com exemplos fictícios. A equipe responsável avalia documentação, conformidade e habilitação. A interface processa os dados no navegador. O motor foi gerado com Gemini 4 Neon no Vertex AI.

## Testes

Execute `node scripts/test.mjs public.json`.

## Licença

MIT. Acorn preserva sua licença em scripts/vendor/LICENSE-Acorn.txt.
