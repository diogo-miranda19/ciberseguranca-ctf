
# Cibersegurança - Relatório Técnico CTF

> Projeto académico desenvolvido em **grupo de 4 elementos** no âmbito da unidade curricular de **Cibersegurança** da Licenciatura em Engenharia Informática no **UPB (Universidade Politécnica de Bragança)**

---

## Sobre o Projeto
Este repositório contém o relatório técnico completo ([`CTF.pdf`](CTF.pdf)) com a documentação e resolução prática de um **Capture The Flag (CTF)**. O trabalho abrangeu 6 categorias distintas de segurança informática: **Boot2Root**, **OSINT**, **Web Hacking**, **Forensic Analysis**, **Cryptography** e **Linux Privilege Escalation**.

---

## A Minha Contribuição no Grupo
Embora todos os elementos do grupo tenham noções das categorias do CTF , dentro da divisão de tarefas da equipa de 4 elementos, fui o principal responsável pela exploração, resolução e documentação das seguintes áreas e desafios:

### 1. Boot2Root — `CTF 03 (User & Root)`
- **Reconhecimento e Enumeração Web:** Identificação de *cookie handler* codificado em Base64 e descoberta de diretório `/backup` exposto (`bak.zip`) através de *directory brute-forcing* (`gobuster`).
- **PHP Object Injection & RCE:** Análise do código-fonte PHP (`index.php`, `user.class.php`, `log.class.php`), manipulação de objetos serializados nos *cookies* para explorar *Local/Remote File Inclusion* (`include()`), obtenção de **Remote Code Execution (RCE)** e estabelecimento de *reverse shell* com `netcat`.
- **Privilege Escalation:** Descoberta de credenciais em ficheiros de *backup* (`credentials.txt.bak`) para movimento lateral e escalada para `root` através da exploração de permissões `sudo` sem *password* no editor `vim` (`NOPASSWD: /usr/bin/vim`).

### 2. OSINT — `OSINT 01` a `OSINT 05`
- **OSINT 01 (Metadados & Geolocalização):** Extração de pistas escondidas em metadados **EXIF** de imagens e identificação geográfica recorrendo a *Google Lens* e *Google Maps*.
- **OSINT 02 (Web Footprinting):** Análise de `robots.txt` e descoberta de diretórios não indexados (`/drafts/`) com notas codificadas em Base64.
- **OSINT 03 (Git Forensics & Leaks):** Auditoria de histórico de *commits* e *branches* secundárias (`dev`) num servidor **Gitea**, recuperando variáveis sensíveis de ficheiros `.env` apagados e cruzando identidades no *PasteBox*.
- **OSINT 04 (DNS Enumeration & Cifras):** Consulta de registos **DNS TXT** e enumeração automatizada de subdomínios ocultos com `dig` e `host`, combinada com decifração **ROT13**.
- **OSINT 05 (Email Forensics & Threat Intel):** Análise forense de cabeçalhos de *email* (*SPF/DKIM/DMARC*, cadeia `Received`, `X-Headers`), descodificação Base64/Hex e consulta a ferramentas internas de **WHOIS**.

---

## Estrutura Global do Relatório
Para além das secções acima, o relatório completo do grupo inclui ainda a resolução das restantes categorias:
- **Boot2Root (`CTF 01`, `02`, `04`):** Exploração WordPress (`wpscan`, *Theme Editor*), *LFI*, *brute-force* SSH (`hydra`), *pivoting* em rede interna Docker e *Docker Escape* via `docker.sock`.
- **Web Hacking (`01` a `05`):** *Fuzzing* de cabeçalhos HTTP (`X-Debug`), *IDOR*, *OS Command Injection*, falsificação de *tokens* JWT (`alg: none`) e *SSRF* (`file://`).
- **Forensic Analysis (`01` a `05`):** Análise de tráfego de rede no **Wireshark**, análise de *logs* Apache, *file carving* com `photorec`.
- **Cryptography (`01`, `02`, `04`, `05`):** Quebra de ROT47, reutilização de *keystream* XOR, força bruta em Cifra Afim ($\bmod 64$) e Fatoração de Fermat em chaves RSA.
- **Linux Privilege Escalation (`01` a `05`):** Abuso de binários SUID, *PATH Hijacking*, `sudo` sem *password* (*GTFOBins*) e *Wildcard Injection* em *cron jobs* com `tar`.

---

## Ferramentas Utilizadas
- **Ambiente & Rede:** Kali Linux, Nmap, Netcat (`nc`), cURL, Dig / Host
- **Enumeração & Web:** Gobuster, Dirb, FFUF, WPScan, Browser DevTools
- **Força Bruta & Análise:** Hydra, Python 3, Base64, `xxd`, Wireshark, PhotoRec
