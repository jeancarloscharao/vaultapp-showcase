# 🧠 Arquitetura — Vault App

## 📌 Visão geral

O Vault App é uma aplicação web voltada ao armazenamento seguro de credenciais, projetada com foco em criptografia, isolamento de dados e proteção contra acesso indevido.

A arquitetura implementa múltiplas camadas de segurança para garantir que informações sensíveis nunca sejam armazenadas em formato legível. 

---

## 🎯 Objetivos arquiteturais

* proteger dados sensíveis em repouso
* garantir isolamento por usuário
* impedir acesso indevido a credenciais
* permitir revelação controlada de dados
* manter alto nível de segurança sem comprometer usabilidade

---

## 🧩 Arquitetura do sistema

### 🌐 Frontend

* landing page pública
* interface simples de acesso ao sistema
* suporte a dark/light mode

---

### 🛠️ Backend (Filament)

* painel administrativo autenticado
* gerenciamento de credenciais
* dashboard com indicadores
* controle de acesso por usuário

---

## 🏗️ Arquitetura em camadas

### Camada de apresentação

* landing page
* painel administrativo

---

### Camada de aplicação

* gerenciamento de credenciais
* validação de acesso
* fluxo de revelação de senha

---

### Camada de domínio

* entidade VaultItem (credenciais)
* regras de segurança
* controle de sessão de revelação

---

### Camada de dados

* armazenamento criptografado
* campos protegidos
* dados isolados por usuário

---

## 🔐 Modelo de segurança

O sistema implementa um modelo híbrido de criptografia.

### 1. Criptografia padrão Laravel

* campos criptografados com APP_KEY
* proteção básica para dados sensíveis

---

### 2. Criptografia em envelope

* geração de chave de dados (Data Encryption Key - DEK)
* criptografia do segredo com DEK
* armazenamento do segredo cifrado

---

### 3. Proteção da chave (Key Wrapping)

* DEK protegida por chave derivada
* chave derivada baseada em:

  * senha do usuário
  * chave do servidor

---

### 4. Derivação de chave (Argon2id)

* uso de algoritmo Argon2id
* salt único por usuário
* proteção contra ataques de força bruta

---

### 5. Algoritmo de criptografia

* AES-256-GCM
* autenticação e integridade dos dados

---

## 🔄 Fluxo de criptografia

1. usuário define senha
2. sistema deriva chave segura
3. gera chave de dados (DEK)
4. criptografa credencial com DEK
5. protege DEK com chave derivada
6. armazena tudo no banco

---

## 🔓 Revelação de senha

A revelação de dados sensíveis é controlada:

* exige senha do usuário
* valida identidade via hash
* libera acesso temporário (sessão)
* revoga acesso após tempo limite

---

## 📊 Segurança adicional

* validação de URLs inseguras (HTTP)
* recomendação de boas práticas no dashboard
* isolamento total por usuário

---

## 🐳 Infraestrutura

* Docker com Laravel Sail
* MySQL para persistência
* Redis para suporte a cache e filas
* Mailpit para e-mails em ambiente local

---

## 📈 Escalabilidade

A arquitetura permite evolução para:

* autenticação em dois fatores (2FA)
* integração com serviços de segurança
* auditoria de acessos
* multi-dispositivo seguro

---

## 💡 Decisões arquiteturais

* uso de criptografia em múltiplas camadas
* separação entre chave de dados e chave de proteção
* derivação de chave baseada no usuário
* controle de sessão para acesso sensível

---

## 🧾 Conclusão

O Vault App foi projetado com foco em segurança desde a base, implementando práticas modernas de criptografia e controle de acesso. A arquitetura garante que dados sensíveis permaneçam protegidos, mesmo em cenários de comprometimento parcial do sistema.
