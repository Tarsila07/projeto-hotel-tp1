# Sistema de Gestão de Hotéis — TP1

Sistema de gerenciamento hoteleiro desenvolvido em **C++** com persistência em **SQLite**, como trabalho prático da disciplina de Técnicas de Programação 1 (UnB).

---

## Descrição

Aplicação de console que permite o cadastro e gerenciamento de hotéis, quartos, reservas e usuários (gerentes e hóspedes). O sistema adota uma arquitetura em camadas com separação clara entre apresentação, serviço e persistência, e faz uso extensivo de classes de domínio com validação embutida.

---

## Funcionalidades

- **Autenticação** — login e cadastro de gerentes e hóspedes com validação de senha
- **Gestão de Hotéis** — cadastro, consulta, atualização e remoção de hotéis
- **Gestão de Quartos** — cadastro e gerenciamento de quartos por hotel (capacidade, diária, ramal)
- **Gestão de Reservas** — criação e consulta de reservas com datas de chegada e partida e valor total
- **Gestão de Hóspedes** — cadastro de hóspedes com endereço e cartão de crédito
- **Gestão de Gerentes** — cadastro de gerentes com ramal e senha

---

## Arquitetura

O projeto segue uma arquitetura em camadas com interfaces abstratas para desacoplamento:

```
┌─────────────────────────────┐
│     Apresentação (UI)        │  Controladoras de menu e fluxo de telas
├─────────────────────────────┤
│       Serviço               │  Fábrica de serviços e lógica de negócio
├─────────────────────────────┤
│      Persistência            │  Acesso ao banco de dados SQLite
├─────────────────────────────┤
│  Entidades │ Domínios        │  Objetos de domínio com validação embutida
└─────────────────────────────┘
```

### Camadas

| Camada | Descrição |
|---|---|
| `apresentacao/` | Controladoras de Sistema, Autenticação, Gerente, Hóspede, Hotel, Quarto e Reserva |
| `servico/` | `FabricaServico` — instancia e injeta as dependências da camada de serviço |
| `persistencias/` | Implementações de acesso ao banco SQLite para cada entidade |
| `entidades/` | Classes `Hotel`, `Quarto`, `Reserva`, `Gerente`, `Hospede`, `Pessoa` |
| `dominios/` | Value objects com validação: `Nome`, `Email`, `Senha`, `Codigo`, `Data`, `Dinheiro`, `Cartao`, `Endereco`, `Telefone`, `Numero`, `Capacidade`, `Ramal` |
| `interfaces/` | Interfaces abstratas para desacoplar camadas |
| `testes/` | Testes unitários das entidades e domínios |

---

## Entidades

| Entidade | Atributos principais |
|---|---|
| `Hotel` | Nome, Endereço, Telefone, Código |
| `Quarto` | Número, Capacidade, Diária (R$), Ramal |
| `Reserva` | Chegada, Partida, Valor, Código, Hotel, Quarto, Hóspede |
| `Gerente` | Nome, Email, Ramal, Senha |
| `Hospede` | Nome, Email, Endereço, Cartão de crédito |

---

## Tecnologias

- **Linguagem:** C++17
- **Banco de dados:** SQLite 3 (biblioteca estática incluída em `sqlite_lib/`)
- **Build:** Code::Blocks (`.cbp`)
- **Documentação:** Doxygen (configuração em `Doxyfile`, saída em `doc/`)

---

## Como Compilar e Executar

### Pré-requisitos

- Compilador C++17 (GCC/MinGW recomendado)
- Code::Blocks (opcional, para abrir o projeto diretamente)

### Via Code::Blocks

1. Abra o arquivo `Trabalho TP1.cbp`
2. Selecione a configuração **Debug** ou **Release**
3. Compile e execute com `F9`

### Via linha de comando (GCC)

```bash
# Compilar (ajuste os caminhos conforme necessário)
g++ -std=c++17 -Iinclude -Isqlite_lib src/**/*.cpp src/main.cpp sqlite_lib/sqlite3.c -o hotel

# Executar
./hotel
```

O executável compilado é gerado em `bin/Debug/`.

---

## Documentação

A documentação gerada pelo Doxygen está disponível em:

- **HTML:** `doc/html/index.html`
- **LaTeX:** `latex/`

Para regenerar a documentação:

```bash
doxygen Doxyfile
```

---

## Estrutura de Diretórios

```
projeto-hotel-tp1/
├── include/           # Cabeçalhos (.hpp) organizados por camada
│   ├── apresentacao/  # Controladoras e interfaces de UI
│   ├── dominios/      # Value objects de domínio
│   ├── entidades/     # Entidades do sistema
│   ├── interfaces/    # Interfaces abstratas
│   ├── persistencias/ # Interfaces e implementações de persistência
│   ├── servico/       # Fábrica de serviços
│   └── testes/        # Testes unitários
├── src/               # Implementações (.cpp)
├── sqlite_lib/        # Biblioteca SQLite (código-fonte e header)
├── bin/               # Executável compilado
├── doc/               # Documentação gerada pelo Doxygen
├── hotel_database.db  # Banco de dados SQLite
└── Doxyfile           # Configuração do Doxygen
```

---

## Autores

- **João Pedro** 
- **Tarsila Marques**
---

*Trabalho Prático 1 — Técnicas de Programação 1 — Universidade de Brasília (UnB)*













