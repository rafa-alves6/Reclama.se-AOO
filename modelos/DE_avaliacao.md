@startuml
title Estado da Avaliação da Denúncia

[*] --> Pendente
Pendente --> Avaliada : Moderador analisa conteúdo
Avaliada --> [*]

state Avaliada {
  [*] --> Válida
  [*] --> Inválida
}

@enduml
