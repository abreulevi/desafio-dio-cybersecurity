# CVE-2008-0166

## Descrição

A CVE-2008-0166 afetou versões do OpenSSL em sistemas Debian e Ubuntu.

Um erro introduzido no código reduziu drasticamente a entropia na geração de chaves criptográficas.

Como consequência:

- chaves SSH previsíveis eram geradas;
- ataques com bancos de chaves pré-calculadas tornaram-se possíveis.

---

# Impacto

- Comprometimento de autenticação SSH;
- Quebra de confidencialidade;
- Acesso não autorizado.

---

# Referências

- https://nvd.nist.gov/vuln/detail/CVE-2008-0166
- https://www.cvedetails.com/cve/CVE-2008-0166/
````
