## CHAPTER 1

> **Functional Requirements**
> 
> Functional requirements describe the system’s behavior: what it does,
> the user interactions, and the business logic.
> 
> Define the problem, why solving it is relevant, and any vital context.
> Make a list of questions about the business rules you want answered.
> 
> If you have a long list of functional requirements, split them by
> context (e.g., consumer/logistics or deployment/scaling). Solutions
> will usually follow these splits, so you may delegate the
> implementation of context’s features to different teams or just place
> them in different services.

**1. Função principal - Descoberta de arquivos e diretórios**

-   A aplicação precisa pegar uma URL fornecida e testar possíveis arquivos e diretórios nela.
-   Se encontrar uma página do tipo “Index Of”, em que já esteja listado os arquivos e diretórios, não é necessário continuar com as tentativas (a maioria das ferramentas não tem essa opção e eu senti falta disso, é útil para laboratórios). Eu gostaria que isso fosse até um padrão, mas com opção de poder desligar caso se encontre falsos positivos.
-   Ao encontrar um diretório, gostaria de ter a opção da aplicação começar a testar o brute force nele também, para encontrar subdiretórios e arquivos.

**2. Sobre output, interface e controles do usuário**

-   A cada arquivo ou diretório que encontrar, exibir na saída o status, tamanho, link completo pra visualização ou que fique prático pra copiar e colar em um navegador
-   Seria interessante ter uma opção pra passar as requisições por um proxy
-   Eu deveria adicionar a possibilidade de autenticação da página se estiver tentando brutar uma área restrita

**3. Sobre resiliência**

-   Seria muito bom que a ferramenta seja resiliente a erros com a internet. Na minha prova a VPN caía com frequência e lá se ia um monte de tentativas. Pensando no que poderia ser feito de diferente das outras, podia se criar uma lista temporária com as tentativas que falharam por causa de erros de conexão (timeout, network interface missing, etc) pra se tentar de novo no futuro quando voltasse a ficar estável (ou quando eu estivesse a fim)
-   Ainda na questão de "tentar de novo no futuro", seria interessante guardar uma sessão interrompida para continuar do mesmo ponto mais tarde.

**4. Adicionais - Sugestões automáticas**

-   Seria interessante uma sugestão de extensões baseadas no site alvo. Se for detectado um servidor X com tecnologia Y, sugerir algumas extensões típicas desse serviço (ex: WordPress → .php, .php7 / IIS → .asp, .aspx, etc)
-   Pensando um pouco além dá até pra sugerir wordlists específicas também baseadas nos serviços

> **Non-Functional Requirements**
> 
> Nonfunctional requirements, however, explain how the system performs: scalability, resilience, security, and maintainability.
> 
> List the essential quality categories you may care about: performance, resilience (which contains scalability and availability), observability, security, and maintainability (which includes extensibility).
> 
> Under each category, detail what the solution should accomplish, such as keeping the latency at the 90th percentile under 100ms.

-   Corzinhas pra chamar atenção e organizar visualmente a saída seria ótimo
-   Possibilidade de aumentar e diminuir em tempo real a verbosidade da saída
-   Seria interessante ter um controle manual da velocidade das requisições/threads utilizadas mesmo depois do início sem interromper a execução e recomeçar (isso é possível?)
-   Deve realizar requisições em um tempo rápido o suficiente pra não me gerar frustações
-   Deve ser capaz de lidar com quedas de conexão sem perder progresso
-   Deve suportar múltiplas tentativas de execução para completar uma sessão após falhas temporárias.