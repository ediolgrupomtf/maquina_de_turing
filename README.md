# Máquina de Turing – Regra 30  
## Projeto Final – Linguagens Formais e Autômatos  
### Instituto Federal Goiano – Campus Trindade  

![Status](https://img.shields.io/badge/status-concluído-brightgreen)
![Python](https://img.shields.io/badge/python-3.10+-blue)
![MT](https://img.shields.io/badge/Máquina%20de%20Turing-Regra%2030-orange)
---

## 📌 Descrição do Projeto

Este projeto implementa uma **Máquina de Turing** capaz de gerar a **próxima linha** de um autômato celular unidimensional seguindo a **Regra 30**, proposta por Stephen Wolfram.

A entrada é uma linha de bits `0` e `1`, delimitada por `#`.  
A saída é escrita após um separador `|` na própria fita.

**Exemplo de fita de entrada:**

```
#000100#|
```

A máquina deve aplicar a Regra 30 em cada célula e gerar uma nova linha como saída.

---

## 📘 O que é a Regra 30?

A Regra 30 é um autômato celular unidimensional onde cada célula depende da sua **vizinhança local**:  
- valor da célula à esquerda  
- valor da célula atual  
- valor da célula à direita  

A regra pode ser representada pela seguinte tabela:

| Vizinhança | Novo valor |
|-----------|------------|
| 111       | 0          |
| 110       | 0          |
| 101       | 0          |
| 100       | 1          |
| 011       | 1          |
| 010       | 1          |
| 001       | 1          |
| 000       | 0          |

Mesmo uma configuração simples gera padrões **caóticos e irregulares**, o que torna a Regra 30 famosa em estudos de complexidade e sistemas dinâmicos.

---

## 🧠 Descrição Formal da Máquina de Turing

A Máquina de Turing projetada tem como objetivo ler a linha inicial e produzir a próxima linha aplicando a Regra 30.  
A nova linha é escrita na fita à direita do separador `|`.

### **Conjunto de estados**

```
Q = { q0, q_scan, q_left, q_right, q_compute, q_write, q_return, q_accept }
```

### **Alfabeto de entrada**

```
Σ = { 0, 1 }
```

### **Alfabeto da fita**

```
Γ = { 0, 1, #, |, B }
```

- `#` marca início e fim da linha de entrada  
- `|` separa área de entrada e saída  
- `B` representa branco  

### **Estado inicial**

```
q0
```

### **Estado de aceitação**

```
q_accept
```

---

## 🔧 Objetivo da Máquina

Para cada posição da fita:

1. ler a vizinhança (esquerda, centro, direita)  
2. aplicar a Regra 30  
3. escrever o novo bit na região de saída à direita de `|`  

---

## 🔄 Comportamento Geral da Máquina

- **q0**: move até o primeiro dígito após `#`  
- **q_scan**: lê cada célula da esquerda para a direita  
- **q_left / q_right**: obtêm a vizinhança  
- **q_compute**: aplica a Regra 30  
- **q_write**: escreve o novo bit  
- **q_return**: volta para continuar a varredura  
- **q_accept**: encerra ao encontrar o `#` final  

---

## 🔣 Função de Transição (descrição textual)

### **1️⃣ Movimento inicial**
```
(q0, #) → (q_scan, #, R)
```

### **2️⃣ Leitura da entrada**
```
(q_scan, 0) → ir calcular vizinhança
(q_scan, 1) → ir calcular vizinhança
(q_scan, #) → (q_accept, #, S)
```

### **3️⃣ Obtenção da vizinhança**
```
(q_left, símbolo)  → move L e lê esquerda
(q_right, símbolo) → move R e lê direita
```

---

## 🔀 Diagrama da Máquina de Turing (ASCII)

> **Obs.:** Utilize fonte monoespaçada ao visualizar.
⠀⠀⠀<img width="556" height="633" alt="image" src="https://github.com/user-attachments/assets/231ffb8b-e72b-46cc-91d5-432e58b78ffa" />




```

---

## 🖥️ Execução

Para executar a simulação:

```
python3 mt_regra30.py
```

Ou, no Windows:

```
python mt_regra30.py
```

---

## 📁 Estrutura do Repositório

```
/
├── README.md
└── mt_regra30.py
```

---

## ✔️ Arquivo Principal: mt_regra30.py

O arquivo contém uma simulação da Máquina de Turing.  
Ele percorre a fita, lê vizinhanças, aplica a Regra 30 e escreve a nova linha após `|`.

---

## 🚀 Exemplo de Uso

Entrada:
```
#000100#|
```

Saída produzida:
```
001110
```

---

## ✨ Conclusão

O projeto demonstra a capacidade da Máquina de Turing de simular um autômato celular, reforçando que mesmo regras simples como a Regra 30 podem gerar comportamentos complexos.
