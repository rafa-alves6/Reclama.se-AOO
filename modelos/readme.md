# 📊 Diagramas UML do Sistema

## Visão Geral do Sistema

```puml
@startuml

skinparam actorStyle awesome

actor "Usuário" as U
actor "Órgão Responsável" as O
actor "Sistema" as S
actor "Moderador" as M
actor "Cidadão" as C

U --> C
U --> M

C --> (Cadastrar Usuário)
C --> (Autenticar Usuário)
C --> (Registrar Denúncia)
C --> (Assinar Denúncia)
C --> (Pesquisar Denúncia)
C --> (Editar/Excluir Publicação)

M --> (Pesquisar Denúncia)
M --> (Editar/Excluir Publicação)
M --> (Analisar Denúncia)

S -up-> (Notificar Atualizações)
S -up-> (Gerar Relatório)


O --> (Responder Denúncia)
O --> (Responder Feedback)

(Registrar Denúncia) .down.> (Gerar Relatório) : gera
(Registrar Denúncia) .down.> (Notificar Atualizações) : notifica

@enduml
```

## Casos de Uso

>  Para cada item, apresentar: Nome, Atores, Fluxo principal, Fluxo alternativo, Pré-condições e Pós-condições, etc. 


| Nome                                   | Descrição breve                                               | Observações                        |
| -------------------------------------- | ------------------------------------------------------------- | ---------------------------------- |
| [Registrar Denúncia](./UC_Denuncia.md) | Permite ao usuário realizar uma denúncia pública              | Realizado por um usuário cidadão  |
| [Cadastrar Usuário](./UC_Denuncia.md)  | Permite ao usuário se cadastrar ao sistema                    | Realizado pelo usuário, permitido pelo sistema |
| [Autenticar Usuário](./UC_Denuncia.md) | Permite ao usuário realizar a autenticação                    | Autenticação realizada pelo usuário com o gov.br |
| [Assinar Denúncia](./UC_Denuncia.md)   | Permite ao cidadão assinar/creditar uma denúncia existente    | Realizado por qualquer cidadão |
| [Pesquisar Denúncia](./UC_Denuncia.md) | Permite a pesquisa de denúncias já registradas                | Disponível para Cidadão, Moderador |
| [Editar/Excluir Publicação](./UC_Denuncia.md) | Permite ao usuário editar ou excluir uma denúncia ou publicação | Realizado por Moderador ou Cidadão (conforme permissões) |
| [Analisar Denúncia](./UC_Denuncia.md)  | Permite ao Moderador analisar uma denúncia registrada         | Realizado por Moderador |
| [Responder Denúncia](./UC_Denuncia.md) | Permite ao órgão responsável responder a uma denúncia         | Realizado pelo Órgão Responsável |
| [Responder Feedback](./UC_Denuncia.md) | Permite ao órgão responsável responder ao feedback da denúncia | Realizado pelo Órgão Responsável |
| [Notificar Atualizações](./UC_Denuncia.md) | Notifica o usuário sobre atualizações em denúncias         | Realizado pelo Sistema |
| [Gerar Relatório](./UC_Denuncia.md)    | Permite ao sistema gerar relatórios sobre o estado das denúncias | Realizado pelo Sistema |


## 🔹 Diagrama de Classes

### Módulo de Usuário

```plantuml
@startuml
abstract class User {
  - id: Integer <<PK>>
  - nome: String
  - cpf: String
  - email: String
  - telefone: String 
  - dataNascimento: DateTime
}

class UserCidadao {
  - denunciasEnviadas: List<Denuncia> 
  - feedbacksEnviados: List<Feedback>
  - denunciasCreditadas: List<Denuncia>
  + registrarDenuncia(): Mensagem
  + registrarFeedback(): Mensagem
  + creditarDenuncia(): void
}

class Moderador {
  - dataAdmissao: DateTime
  - dataDemissao: DateTime
  - ativo: boolean
}

UserCidadao -up-|> User
Moderador -up-|> User

class Entidade {
  - id: Integer <<PK>>
  - nome: String
  - email: String
  - telefone: String
  - statusAtivo: boolean 
  - siteURL: String 
  - dataFundado: DateTime
  - denunciasRecebidas: List<Denuncia>
  + responderDenuncia(): Denuncia
  + responderFeedback(): Feedback
}


class EntidadePublica {
} 

class EntidadePrivada {
  - cnpj: String
}

EntidadePublica -up-|> Entidade
EntidadePrivada -up-|> Entidade

class Mensagem {
  - id: Integer <<PK>>
  - titulo: String
  - descricao: String
  - denuncianteId: Integer
  - tipo: String 
  - data: DateTime
}

class Denuncia {
  - denuncianteId: Integer
  + gerarRelatorio(): void
}

class Feedback {
  - denunciaId: Integer
  - denuncianteId: Integer
  - entidadeId: Integer
}

Denuncia -up-|> Mensagem
Feedback -up-|> Mensagem 

enum StatusDenuncia {
  EM_ANALISE
  REGISTRADA
  SEM_RESPOSTA
  EM_SOLUCAO
  SOLUCIONADA
}

Denuncia --> StatusDenuncia : 1..1
UserCidadao "1..*" --> "1..*" Denuncia : envia
UserCidadao "1..*" --> "1..*" Feedback : envia
Entidade "1..*" --> "1..*" Denuncia : recebe
Entidade "1..*" --> "1..*" Feedback : responde
Denuncia "1..*" --> "1..*" Feedback : gera

@enduml
```


## 🔹 Diagrama de Estados

| Nome                            | Finalidade / Obs  |
| ------------------------------- | ----------------- |
| [Status Usuário](./DE_login.md) | Status do usuário |
| A2                              | B2                |
| A3                              | B3                |

