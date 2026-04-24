# Desafio DevSecOps — Gerenciador de Tarefas

Este repositório faz parte do desafio prático do módulo de DevSecOps da ADA Tech. O desafio aqui proposto me permitiu aplicar, na prática, os conhecimentos adquiridos ao longo do curso ministrado pelo instrutor Matheus, a quem agradeço pela dedicação e atenção durante toda essa jornada de aprendizado.


# Funcionamento da Pipeline

A pipeline de segurança é composta por diferentes etapas (steps), cada uma com um papel específico na detecção e prevenção de vulnerabilidades. O objetivo é garantir que o código seja analisado, validado e implantado de forma segura.

1. Secrets Scanning com Gitleaks
O que faz: Analisa o repositório em busca de credenciais expostas, como chaves de API, tokens, senhas ou certificados.

Por que é importante: Vazamento de segredos é uma das falhas mais críticas em segurança, pois pode permitir acesso indevido a sistemas e dados sensíveis. Essa etapa garante que informações confidenciais não sejam versionadas no código.

2. SAST (Static Application Security Testing) com Semgrep
O que faz: Examina o código-fonte em busca de padrões inseguros, más práticas de programação e vulnerabilidades conhecidas (como SQL Injection, XSS, uso inseguro de funções).

Por que é importante: Detecta problemas antes mesmo da execução da aplicação, permitindo que sejam corrigidos na fase de desenvolvimento. Isso reduz custos e riscos de segurança em produção.

3. SCA (Software Composition Analysis) com Grype
O que faz: Analisa dependências e bibliotecas utilizadas no projeto, verificando se possuem vulnerabilidades conhecidas em bancos de dados de segurança (como CVEs).

Por que é importante: Grande parte das aplicações modernas depende de pacotes externos. Se uma biblioteca vulnerável for usada, toda a aplicação pode ser comprometida. O SCA garante que apenas versões seguras sejam utilizadas.

4. Deploy com GitHub Pages
O que faz: Publica a aplicação em um ambiente acessível via GitHub Pages.

Por que é importante: Além de disponibilizar o projeto, essa etapa só deve ser executada se todas as anteriores forem aprovadas. Isso garante que apenas código seguro e validado chegue ao ambiente de produção.

# Fluxo da Pipeline

Commit/Pull Request → dispara a pipeline.

Gitleaks → bloqueia caso segredos sejam encontrados.

Semgrep → interrompe se houver falhas de segurança no código.

Grype → falha se dependências vulneráveis forem detectadas.

Deploy GitHub Pages → só acontece se todos os steps anteriores passarem com sucesso.

👉 Assim, a pipeline funciona como uma barreira de proteção em camadas: primeiro evita vazamento de segredos, depois garante código seguro, em seguida valida dependências externas, e por fim libera o deploy apenas se tudo estiver conforme os padrões de segurança.

