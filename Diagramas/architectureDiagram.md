```mermaid
graph TD
    subgraph "Atores e Interfaces (Frontend)"
        A["Cidadão"] -- "Usa" --> AppCidadao["App do Cidadão (React Native)"]
        B["Moderador"] -- "Usa" --> PainelAdmin["Painel Administrativo (Web) <br> Acesso por Papel"]
        D["Entidade / Órgão"] -- "Usa" --> PainelAdmin
    end

    subgraph "Backend (Servidor)"
        API["API REST (Java / Spring Boot)"]
        
        subgraph "Modulos de Servico"
            S1["Gestão de Denúncias e Fluxo"]
            S2["Gestão de Usuários e Permissões <br> (Cidadão, Moderador, Entidade)"]
            S3["Servico de Notificações"]
            S4["Integração com Armazenamento"]
        end
    end

    subgraph "Persistência e Serviços Ext."
        DB[("Banco de Dados <br> (PostgreSQL)")]
        S3Bucket[("AWS S3 <br> Armazenamento de Anexos")]
        PushService[("Servico de Notificacoes Push <br> (Firebase)")]
    end

    %% Conexoes
    AppCidadao -- "Requisições HTTP" --> API
    PainelAdmin -- "Requisições HTTP" --> API

    API --> S1 & S2 & S3 & S4

    S1 -- "Salva/Lê dados das denúncias" ---> DB
    S2 -- "Salva/Lê dados de usuários e papeis" ---> DB
    
    S4 -- "Upload/Download de anexos" ---> S3Bucket
    
    S3 -- "Envia gatilho de notificação" ---> PushService

    PushService -- "Envia notificação para o dispositivo" --> AppCidadao
```
