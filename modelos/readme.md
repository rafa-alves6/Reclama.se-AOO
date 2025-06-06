# 📊 Diagramas UML do Sistema

## Visão Geral do Sistema

> Adicionar o diagrama de caso de uso que mostra a visão geral do sistema

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


| Nome                                   | Descrição breve                                               | Observações                     |
| -------------------------------------- | ------------------------------------------------------------- | ------------------------------- |
| [Registrar Denúncia](./UC_Denuncia.md) | Permite ao usuário realizar uma denúncia pública              |                                 |
| A2                                     | B2                                                            | C2                              |
| A3                                     | B3                                                            | C3                              |

## 🔹 Diagrama de Classes

### Módulo de Usuário

```plantuml
@startuml
skinparam groupInheritance 2
abstract class Usuario {
  + id: Integer <<PK>>
  + nome: String
  + email: String
  + senhaHash: String
  + dataCadastro: DateTime
  + ultimoAcesso: DateTime
  --
  + autenticar(): Boolean
  + solicitarTrocaSenha(): void
}

class Administrador {
  + nivelAcesso: Integer
  + desbloquearUsuario(): void
  + excluirUsuario(): void
}

class UsuarioComum {
  + preferencias: String
}

class StatusLogin{
  + id: Integer <<PK>>
  + tipo: Status
  + dataAlteracao: DateTime
  + motivo: String
  --
  + atualizarStatus(novoStatus: Status): void
}

class TentativaLogin {
  + id: Integer <<PK>>
  + dataHora: DateTime
  + ip: String
  + sucesso: Boolean
}

Usuario "1" *-- "1" StatusLogin
Usuario "1" *-- "0..*" TentativaLogin

Administrador --|> Usuario
UsuarioComum --|> Usuario

enum Status {
  AGUARDANDO_CONFIRMACAO
  ATIVO
  BLOQUEADO
  CANCELADO
  EXCLUIDO
}

Usuario "1" --> "1..*" Status

@enduml
```


## 🔹 Diagrama de Estados

> Mostra os estados possíveis de cada entidade [ex: login] e as transições entre eles.

| Nome                            | Finalidade / Obs  |
| ------------------------------- | ----------------- |
| [Status Usuário](./DE_login.md) | Status do usuário |
| A2                              | B2                |
| A3                              | B3                |

