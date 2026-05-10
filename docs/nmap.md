
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


# Scan de versão

```bash
sudo nmap -sS -Pn -n -sV -T1 -f --mtu 24 192.168.56.105 -p 22
```

## Parâmetros adicionais

| Parâmetro | Função                     |
| --------- | -------------------------- |
| `-Pn`     | Ignora descoberta por ping |
| `-n`      | Não resolve DNS            |
| `-sV`     | Detecta versão do serviço  |
| `-p 22`   | Escaneia apenas SSH        |

````
---
