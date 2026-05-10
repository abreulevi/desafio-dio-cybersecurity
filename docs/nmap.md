# docs/nmap.md

```markdown
# Enumeração com Nmap

## Scan inicial

```bash
sudo nmap -sS -T2 -f --mtu 24 192.168.56.101-105
````

---

# Explicação dos parâmetros

| Parâmetro  | Função                                         |
| ---------- | ---------------------------------------------- |
| `-sS`      | SYN Scan                                       |
| `-T2`      | Timing lento para evitar detecção              |
| `-f`       | Fragmenta os pacotes                           |
| `--mtu 24` | Define fragmentação MTU customizado            |

---
