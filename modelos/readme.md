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
  - status: String <<enum>> # ATIVO, INATIVO, BLOQUEADO
  + autenticar()
}

class Cidadao extends Usuario {
  + enviarDenuncia()
  + enviarFeedback()
}

class Moderador extends Usuario {
  + avaliarDenuncia()
}

Usuario -[hidden]-> Cidadao
Usuario -[hidden]-> Moderador

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
  - status: String <<enum>> # ENVIADO, VISUALIZADO, ENCERRADO
  + enviar()
}


class Arquivo {
  - nome: String
  - tipo: String
  - tamanho: int
  - status: String <<enum>> # ADICIONADO, VALIDANDO, ACEITO, RECUSADO
  + Compativel(): boolean
}


Denuncia --o Arquivo : contém

class Avaliacao {
  - id: int
  - data: Date
  - status: String <<enum>> # PENDENTE, VALIDADA, INVALIDA
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

Cidadao --o Denuncia : faz
Cidadao --o Feedback : envia
@enduml

```


## 🔹 Diagrama de Estados

> Mostra os estados possíveis de cada entidade [ex: login] e as transições entre eles.

| Nome                                       | Finalidade / Obs                            |
| ------------------------------------------ | ------------------------------------------- |
| [Status da Denúncia](./DE_denuncia.md)    | Criada → Avaliada → Respondida → Finalizada |
| [Status do Feedback](./DE_feedback.md)    | Enviado → Visualizado → Encerrado           |
| [Status do Usuário](./DE_usuario.md)      | Ativo, Inativo, Bloqueado                   |
| [Status da Avaliação](./DE_avaliacao.md)  | Pendente → Avaliada                         |
| [Status do Arquivo](./DE_arquivo.md)      | Adicionado → Validando → Aceito ou Recusado |

