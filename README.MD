# Manipulação e Formatação de Strings em Python

Manipular e formatar **strings** em Python é essencial, pois textos são frequentemente usados para comunicação entre usuários e sistemas, e também no processamento de dados. Operações comuns incluem:

* Remover espaços e caracteres desnecessários
* Alterar maiúsculas/minúsculas
* Substituir ou contar palavras
* Dividir e unir textos
* Formatar variáveis, números e datas

---

## 1. Método `strip()`

Remove **espaços em branco** e caracteres de nova linha (`\n`, `\r`) do **início e do fim** de uma string.

```python
linha = "   Olá mundo!   \n"
linha_limpa = linha.strip()
print(repr(linha_limpa))  # 'Olá mundo!'
```

**Uso comum:** contar linhas com conteúdo em arquivos:

```python
contador = 0
with open("dados.txt", "r") as arquivo:
    for linha in arquivo:
        if linha.strip():  # só conta se houver conteúdo
            contador += 1
print(contador)
```

---

## 2. Método `count()`

Conta **quantas vezes uma substring aparece** em uma string.

```python
frase = "Eu amo comer amoras no café da manhã"
print(frase.count("amo"))  # 2
```

⚠️ `count` conta substrings dentro de outras palavras. Para contar apenas palavras exatas, combine com `split()`.

---

## 3. Método `split()`

Divide uma string em **uma lista de palavras ou trechos**, usando um separador (por padrão, espaços).

```python
frase = "Eu amo comer amoras"
palavras = frase.split()
print(palavras)  # ['Eu', 'amo', 'comer', 'amoras']

texto = "Carro,moto,avião"
lista = texto.split(",")
print(lista)  # ['Carro', 'moto', 'avião']
```

**Contando palavras exatas:**

```python
frase = "Eu amo comer amoras"
contador = 0
for termo in frase.split():
    if termo == "amo":
        contador += 1
print(contador)  # 1
```

---

## 4. Método `join()`

Une elementos de uma lista em **uma única string**, usando um separador (`conector`).

```python
minha_lista = ["Python", "é", "legal"]

# Conector vírgula
texto1 = ", ".join(minha_lista)
print(texto1)  # 'Python, é, legal'

# Conector nova linha
texto2 = "\n".join(minha_lista)
print(texto2)
# Python
# é
# legal
```

---

## 5. Formatação de Strings (f-strings)

Permite incluir **variáveis e expressões** diretamente dentro de strings de forma clara e legível.

```python
nome = "Matheus"
idade = 19
print(f"Meu nome é {nome} e tenho {idade} anos")
```

**Funcionalidades avançadas:**

* Chamadas de funções: `{nome.upper()}`
* Operações matemáticas: `{10 + 5}`
* Comparações booleanas: `{idade > 18}`
* Verificação de elementos em listas: `{3 in [1,2,3]}`

**Formatação de largura e alinhamento:**

```python
frutas = ["maçã", "banana", "laranja"]
for fruta in frutas:
    print(f"{fruta:12} -> {len(fruta):3} letras")
```

**Formatação de floats:**

```python
pi = 3.14159
print(f"{pi:.1f}")   # 3.1
print(f"{pi:6.1f}")  # 3.1 com largura 6
print(f"{pi:.4f}")   # 3.1416
```

**Formatação de datas:**

```python
from datetime import datetime

data = datetime.now()
print(f"{data}")         # padrão
print(f"{data:%d/%m/%Y}")  # 13/08/2020
```

---

## Resumo rápido

| Método / Recurso | Função                                      | Exemplo                           |
| ---------------- | ------------------------------------------- | --------------------------------- |
| `strip`          | Remove espaços e \n do início/fim da string | `" abc\n".strip() → "abc"`        |
| `count`          | Conta ocorrências de uma substring          | `"amo amo".count("amo") → 2`      |
| `split`          | Divide a string em lista                    | `"a b c".split() → ["a","b","c"]` |
| `join`           | Une elementos de lista em string            | `", ".join(["a","b"]) → "a, b"`   |
| f-strings        | Insere variáveis e expressões em strings    | `f"Nome: {nome}, Idade: {idade}"` |

# 🔐 Codificação de Mensagens com Python — Cifra ZENIT POLAR

Este projeto demonstra como realizar a **codificação de mensagens** usando a cifra de substituição **ZENIT POLAR** em Python.  
Além disso, apresenta conceitos de manipulação de strings como `replace`, `split`, `join` e `title`.

---

## 📖 O que é a cifra ZENIT POLAR?

A cifra **ZENIT POLAR** é uma substituição simples de letras:  

- **Z ↔ P**  
- **E ↔ O**  
- **N ↔ L**  
- **I ↔ A**  
- **T ↔ R**

Isso significa que cada letra de um grupo é trocada pela correspondente do outro grupo.  

Exemplo:  
- `"ZENIT"` → `"POLAR"`  
- `"POLAR"` → `"ZENIT"`

> Essa técnica é **bidirecional**: o mesmo processo serve para codificar e decodificar.

---

## 🧑‍💻 Código em Python

```python
def zenit_polar_replace(text):
    # Aplicar a codificação ZENIT POLAR utilizando o método replace
    replacements = [
        ('z', 'p'), ('e', 'o'), ('n', 'l'), ('i', 'a'), ('t', 'r'),
        ('Z', 'P'), ('E', 'O'), ('N', 'L'), ('I', 'A'), ('T', 'R')
    ]
    for old, new in replacements:
        text = text.replace(old, new)
    return text
 
def main():
    # Frase de exemplo
    phrase = "The quick brown fox jumps over the lazy dog".title()
    
    # Divisão da frase em palavras
    words = phrase.split()
    
    # Codificação de cada palavra
    coded_words = [zenit_polar_replace(word) for word in words]
    
    # Reunião das palavras em uma frase
    coded_phrase = " ".join(coded_words)

    print("Original:", phrase)
    print("Coded:", coded_phrase)

if __name__ == "__main__":
    main()
```

---

## ⚙️ Saída esperada

```
Original: The Quick Brown Fox Jumps Over The Lazy Dog
Coded: Rho Qaack Brawl Fax Jamrs Ovor Rho Lziy Dag
```

---

## 📌 Conceitos utilizados

- **Funções** → organização do código em blocos reutilizáveis.  
- **replace()** → substituição de caracteres.  
- **split()** → separação de string em palavras.  
- **join()** → reconstrução de string a partir de lista.  
- **title()** → capitalização da primeira letra de cada palavra.  
- **List Comprehension** → aplicação rápida da função a cada item de uma lista.  

---

## 🎯 Objetivo educacional

Este projeto mostra como é possível:  
- Criar uma cifra de substituição básica.  
- Manipular strings em Python.  
- Introduzir conceitos de criptografia de forma simples e prática.  

> ⚠️ Importante: a cifra ZENIT POLAR não é segura para uso real em segurança da informação.  
É apenas um exemplo didático e divertido para aprender manipulação de texto.

