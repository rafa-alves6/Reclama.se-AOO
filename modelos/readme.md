# 📊 Diagramas UML do Sistema

## Visão Geral do Sistema

> Adicionar o diagrama de caso de uso que mostra a visão geral do sistema

```puml
@startuml

left to right direction


actor "Usuário" as Usuario
actor "Administrador" as Adm
actor "Usuário Comum" as Comum
actor Sistema as Sistema


Adm --|> Usuario
Comum --|> Usuario


rectangle "Sistema de Autenticação" {
  usecase "Realizar login" as UC1
}

rectangle "Configurações e Otimizações" {
  usecase "Realizar backup diário" as UCS1
}
usecase "Funçao 1" as UCEx1
usecase "Funçao 2" as UCEx2
usecase "Funçao 3" as UCEx3
usecase "Funçao 4" as UCEx4
usecase "Funçao 5" as UCEx5

Usuario --> UC1
Usuario --> UCEx1
Usuario --> UCEx2
Usuario --> UCEx4
Usuario --> UCEx5
Sistema -up-> UCS1
Sistema -up-> UCEx3
Sistema -up-> UCEx2
Sistema -up-> UCEx5

Adm -> UCS1
Adm -> UCEx5
@enduml

```

## Casos de Uso

>  Para cada item, apresentar: Nome, Atores, Fluxo principal, Fluxo alternativo, Pré-condições e Pós-condições, etc. 


| Nome                               | Descrição breve             | Observações |
| ---------------------------------- | --------------------------- | ----------- |
| [Realizar Login](./UC_01_login.md) | Permite o acesso ao sistema | -           |
| A2                                 | B2                          | C2          |
| A3                                 | B3                          | C3          |

## 🔹 Diagrama de Classes

### Módulo de Usuário

```plantuml
@startuml
title Reclã.me - Diagrama de Classes

class Usuario {
  - id: int
  - nome: String
  - email: String
  + autenticar()
}

class Cidadao extends Usuario {
  + enviarDenuncia()
  + enviarFeedback()
}

class Moderador extends Usuario {
  + avaliarDenuncia()
}

class Agente extends Usuario {
  + responderDenuncia()
}

Usuario -[hidden]-> Cidadao
Usuario -[hidden]-> Moderador
Usuario -[hidden]-> Agente

class Denuncia {
  - id: int
  - descricao: String
  - status: String <<enum>> # PENDENTE, AVALIADA, RESPONDIDA
  - dataCriacao: Date
  + validarAnexos(): boolean
  + publicar()
}

class Feedback {
  - id: int
  - mensagem: String
  - data: Date
  + enviar()
}

class Arquivo {
  - nome: String
  - tipo: String
  - tamanho: int
  + ehCompativel(): boolean
}

Denuncia --o Arquivo : contém

class Avaliacao {
  - id: int
  - data: Date
  - valida: boolean
  + avaliar()
}

class Resposta {
  - id: int
  - texto: String
  - data: Date
  + emitir()
}

class Orgao {
  - id: int
  - nome: String
  - responsavel: String
  + emitirResposta()
}


Denuncia --o Avaliacao : avaliada_por
Avaliacao --> Moderador : feita_por

Denuncia --o Resposta : tem
Resposta --> Orgao : emitida_por
Resposta --> Agente : respondida_por

Orgao "1" o-- "*" Agente : possui


Cidadao --o Denuncia : faz
Cidadao --o Feedback : envia
@enduml
```


## 🔹 Diagrama de Estados

> Mostra os estados possíveis de cada entidade [ex: login] e as transições entre eles.

| Nome                            | Finalidade / Obs  |
| ------------------------------- | ----------------- |
| [Status Usuário](./DE_login.md) | Status do usuário |
| A2                              | B2                |
| A3                              | B3                |

