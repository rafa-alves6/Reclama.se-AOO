@startuml
title Estado do Arquivo Anexado

[*] --> Adicionado
Adicionado --> Validando : Sistema verifica compatibilidade
Validando --> Aceito : Arquivo é compatível
Validando --> Recusado : Arquivo é incompatível
Aceito --> [*]
Recusado --> [*]

@enduml
