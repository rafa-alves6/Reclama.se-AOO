@startuml
title Estado da Denúncia

[*] --> Criada
Criada --> Avaliada : Moderador avalia
Avaliada --> Respondida : Órgão responde
Respondida --> Finalizada : Usuário confirma recebimento ou sistema encerra
Finalizada --> [*]

@enduml
