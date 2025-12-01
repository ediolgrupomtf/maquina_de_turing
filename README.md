# Máquina de Turing – Regra 30  
Projeto Final – Linguagens Formais e Autômatos  
Instituto Federal Goiano – Campus Trindade


![Status](https://img.shields.io/badge/status-concluído-brightgreen)
![Python](https://img.shields.io/badge/python-3.10+-blue)
![MT](https://img.shields.io/badge/Máquina%20de%20Turing-Regra%2030-orange)

## 📌 Descrição do Projeto
Este trabalho implementa uma **Máquina de Turing** capaz de gerar a **próxima linha** de um autômato celular unidimensional segundo a **Regra 30**, proposta por Stephen Wolfram.

A entrada é uma linha de bits `0` e `1`, limitada por `#`, e a saída é escrita após um separador `|` na própria fita.

Exemplo de fita de entrada:

#000100#|

---

## 📘 O que é a Regra 30?
A Regra 30 é um autômato celular de uma dimensão onde cada célula depende de:

- O valor da célula à esquerda  
- O valor da célula atual  
- O valor da célula à direita  

A tabela da regra é:

| Vizinhança | Novo Valor |
|------------|------------|
| 111 | 0 |
| 110 | 0 |
| 101 | 0 |
| 100 | 1 |
| 011 | 1 |
| 010 | 1 |
| 001 | 1 |
| 000 | 0 |

O padrão gerado costuma ser **caótico**, mesmo partindo de uma única célula preta.

Um exemplo visual clássico gerado por várias iterações:

                           1
                          111
                         11001
                        1011110
                       100100110
                     ... (caótico)


---

## 🧠 Descrição Formal da Máquina de Turing

A Máquina de Turing projetada tem como objetivo ler uma linha de células (0 e 1) na fita e produzir a próxima linha segundo a Regra 30, escrevendo o resultado após o símbolo separador |.

Elementos formais
• Conjunto de estados
𝑄 = {𝑞0,𝑞scan,𝑞left,𝑞right,𝑞compute,𝑞write,𝑞return,𝑞accept}
• Alfabeto de entrada
Σ={0,1}
• Alfabeto da fita
\Gamma = \{ 0,\ 1,\ #,\ |,\ B \}

# marca o início e fim da linha de entrada

| separa área de entrada e área de saída

B representa célula em branco

• Estado inicial
      𝑞0
      ​
• Conjunto de estados de aceitação
𝐹 ={𝑞accept}

A Máquina de Turing proposta é definida por:

- **Estados:**  
  `Q = { q0, q_scan, q_compute, q_write, q_return, q_accept }`

- **Alfabeto de entrada:**  
  `Σ = { 0, 1 }`

- **Alfabeto da fita:**  
  `Γ = { 0, 1, #, |, B }`

- **Estado inicial:**  
  `q0`

- **Estado de aceitação:**  
  `q_accept`

- **Objetivo:**  
  Para cada célula da entrada, ler sua vizinhança `(esq, atual, dir)` e usar a Regra 30 para calcular a próxima linha, escrevendo na região de saída à direita do caractere `|`.

---

Comportamento geral da máquina

A Máquina de Turing segue este processo:

q0: Move para a direita até encontrar o início dos dados (primeiro após #).

qscan: Varrendo a entrada da esquerda para a direita, para cada célula chama a rotina de cálculo da vizinhança.

qleft / qright: Movimenta-se para obter o valor da célula da esquerda e da direita.

qcompute: A partir dos três valores (esq, centro, dir), aplica a Regra 30, determinando o próximo bit.

qwrite: Move para o lado direito do separador | e escreve o novo bit.

qreturn: Retorna para a próxima célula da entrada, seguindo a leitura sequencial.

Quando encontra o # final (fim da linha), termina em qaccept.

Função de transição (descrição textual)

A função δ não será escrita símbolo a símbolo (seria enorme e impraticável), mas segue estas regras:

1️⃣ Movimento inicial

(q0, #) → (qscan, #, R)

2️⃣ Leitura de cada célula da entrada

(qscan, 0) → ir calcular vizinhança

(qscan, 1) → ir calcular vizinhança

(qscan, #) → (qaccept, #, S) ← fim da entrada

3️⃣ Obtenção da vizinhança

(qleft, símbolo) → move L até capturar left

(qright, símbolo) → move R até capturar right


## 🔀 Diagrama da Máquina de Turing (ASCII)

Representação simplificada do comportamento geral:
                   ┌───────────────┐
                   │               │
             ┌───> │   q_scan      │ ────┐
             │     │ (lê entrada)  │     │
             │     └───────────────┘     │
             │                            │
        ┌────┴───┐                   ┌────▼──────┐
        │  q0    │                   │ q_compute │
        │inicial │                   │aplica R30 │
        └────┬───┘                   └────┬──────┘
             │                            │
             │                            │
             │                       ┌────▼───────┐
             │                       │  q_write   │
             │                       │escreve bit │
             │                       └────┬──────┘
             │                            │
             │                       ┌────▼──────┐
             └───────────────────────┤ q_return  │
                                     │volta p/scan│
                                     └────┬──────┘
                                          │
                                     ┌────▼─────┐
                                     │ q_accept │
                                     │ (fim)    │
                                     └──────────┘

---

**Execução**:

python3 mt_regra30.py

**Estrutura do Repositório**

/
├── README.md
└── mt_regra30.py




