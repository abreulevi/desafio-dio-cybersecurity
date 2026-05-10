```markdown
# Reconhecimento com Netdiscover

## Objetivo

Realizar reconhecimento passivo da rede.

---

# Comando

```bash
sudo netdiscover -p -r 192.168.56.0/24
````

---

# Parâmetros

| Parâmetro | Função                 |
| --------- | ---------------------- |
| `-p`      | Modo passivo           |
| `-r`      | Define o range da rede |

---

# Estratégia

O modo passivo evita enviar pacotes ativos para descoberta.

A ferramenta apenas escuta o tráfego existente na rede.

````

---
