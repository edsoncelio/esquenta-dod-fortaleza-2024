---
theme: apple-basic
author: edsoncelio
title: 'Observabilidade com Ferramentas OpenSource'
mdc: true
transition: slide-left
hideInToc: true
layout: intro
---

# Observabilidade com Ferramentas OpenSource

Stack LGTM+ e Mais Um Pouco

<div class="absolute bottom-10">
  <span class="font-700">
    Esquenta DoD Fortaleza - 10.08.2024 
  </span>
</div>


<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/edsoncelio/esquenta-dod-fortaleza-2024" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>


---
transition: slide-left
hideInToc: true
level: 3
---

# Sobre Mim

* SRE
* Grafana Champion, AWS Community Builder e CNCF Ambassador
* Mantenedor/contribuidor da documentação dos projetos abaixo (em Português do Brasil): 
  * Kubernetes
  * OpenTelemetry
  * Glossário Cloud Native da CNCF

<div class="absolute bottom-10">
  <span class="font-400">
    Contatos: /in/edsoncelio, github.com/edsoncelio, edsoncelio.dev
  </span>
</div>


---
transition: slide-left
hideInToc: true
---

# Agenda

<Toc minDepth="1" maxDepth="2"></Toc>

---
transition: slide-left
layout: section
level: 1
---

# O que é Observabilidade?

---
transition: slide-left
layout: quote
level: 1
hideInToc: true
---

Observabilidade é a capacidade de medir os estados internos de um sistema examinando os sinais emitidos.

A observabilidade nos permite compreender um sistema a partir do exterior, permitindo fazer perguntas sobre esse sistema sem conhecer o seu funcionamento interno. 
Além disso, permite solucionar facilmente e lidar com novos problemas e ajuda a responder à pergunta: “Por que isso está acontecendo?

---
transition: slide-left
layout: section
level: 2
---

# Dados de Telemetria Importantes de Conhecer

---
transition: slide-left
hideInToc: true
level: 3
---

# Logs

Um log é um registro de texto com marcação de data/hora, estruturado (recomendado) ou não estruturado, com metadados.
A maioria das linguagens de programação possuem bibliotecas de logging de forma nativa.

<br>

```bash
I, [2021-02-23T13:26:23.505892 #22473]  INFO -- : [6459ffe1-ea53-4044-aaa3-bf902868f730] Started GET "/" for ::1 at 2021-02-23 13:26:23 -0800
```

---
transition: slide-left
level: 3
---

# Métricas

Métricas são uma representação numérica de dados medidos em intervalos de tempo.

As métricas economizam tempo porque podem ser facilmente correlacionadas entre os componentes da aplicação/infraestrutura para fornecer uma visão abrangente da integridade e do desempenho do sistema. Também permitem uma pesquisa mais fácil e uma retenção estendida de dados.

<br>

```bash
avg(rate(node_cpu{job="default/node-exporter",mode="idle"}[1m]))
```

Outros exemplos:

- Taxa de Erros
- Uso de Memória
- Uso de Espaço em Disco


---
transition: slide-left
level: 3
---

# Rastros (Traces)
Os rastros nos dão uma visão geral do que acontece quando é feita uma requisição em uma aplicação.
Independente da arquitetura da sua aplicação, os rastros são essenciais para entender o caminho completo
das requisições na aplicação.

## Trechos (Spans) 
Um trecho representa uma unidade de trabalho (ou operação).   
Trechos são os blocos que compõem os rastros.

<style>
  img {
  display: block;
  margin: auto;

}
</style>

![otel logo](/trace.png){width=39%}

---
transition: slide-left
level: 3
---

Existem outros dados de telemetria importantes que valem a pena serem citados:

- Eventos (similar a um histórico)
- Perfils (análise de performance em tempo de execução)
- Erros

---
transition: slide-left
layout: section
level: 1
---


# O Que Levar em Conta ao Montar sua Plataforma de Observabilidade

---
transition: slide-left
layout: bullets
level: 2
---

* Conhecimento interno do time
* Customização e flexibilidade das ferramentas
* Suporte
* Vendor Lock-In
* Volume de Dados


---
transition: slide-left
layout: section
level: 1
---

# Ferramentas e Frameworks OpenSource

---
transition: slide-left
layout: section
level: 2
---

# OpenTelemetry (OTel)

<style>
  img {
  display: block;
  margin: auto;

}
</style>

![otel logo](/otel-logo.png){width=22%}

---
transition: slide-left
level: 2
---

O OpenTelemetry, também conhecido como Otel é um **framework de Observabilidade** projetado para **criar e gerenciar dados de telemetria**, como rastros, métricas e logs. Por design, o OpenTelemetry é **agnóstico a fornecedor e ferramenta**, o que significa que pode ser usado com grande variedade de backends de Observabilidade.

O OpenTelemetry atende a necessidade de observabilidade ao mesmo tempo que segue dois princípios fundamentais:

- Os dados que você gera são seus. Não há dependência de fornecedor (o famoso vendor lock-in).
- Você **só** precisa aprender um único conjunto de APIs e convenções.

<br>

Atualmente, o Otel tem compatibilidade com [mais de 40 fornecedores](https://opentelemetry.io/ecosystem/vendors/) de plataformas de Observabilidade
integrado com muitas bibliotecas e serviços e com um grande número de usuários.

<br>
<br>

<footer>

[https://opentelemetry.io/](https://opentelemetry.io/docs/)

</footer>

---
transition: slide-left
hideInToc: true
level: 3
---

## Componentes

<br>

- Especificação para todos os componentes (API, SDK e Dados)
- Collector (receber, processar e exportar dados de telemetria)
- Implementações de API e SDK específicas para cada linguagem (.NET, Java, Javascript, PHP, Python...)

---
transition: slide-left
level: 3
---

## Arquitetura

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![otel](/otel.png){width=65%}


<footer>

[https://opentelemetry.io/](https://opentelemetry.io/docs/)

</footer>

---
transition: slide-left
level: 3
---

## Instalação/Configuração

* Para instrumentação das aplicações, você pode consultar a [documentação específica de cada linguagem](https://opentelemetry.io/docs/languages/).
* Para autoinstrumentação, você pode consultar a [documentação para cada linguagem](https://opentelemetry.io/docs/zero-code/).
* Para configuração do Collector em Kubernetes, pode usar algum dos Helm Charts disponíveis:
  * [opentelemetry-kube-stack](https://github.com/open-telemetry/opentelemetry-helm-charts/tree/main/charts/opentelemetry-kube-stack)
  * [opentelemetry-operator](https://github.com/open-telemetry/opentelemetry-helm-charts/tree/main/charts/opentelemetry-operator)
  * [opentelemetry-collector](https://github.com/open-telemetry/opentelemetry-helm-charts/tree/main/charts/opentelemetry-collector)
* O Collector também suporta outros orquestradores/sistemas, como Nomad, Linux e Windows.

---
transition: slide-left
layout: section
level: 2
---

# Stack da Grafana Labs (LGTM+)

<style>
  img {
    display: block;
    margin: auto;
  }
</style>

![grafana grot](/grafana-grot.svg){width=20%}

---
transition: slide-left
hideInToc: true
level: 3
---

# Loki
O Loki é um agregador de logs com alta disponibilidade, multi-tenant e escalável, inspirado no Prometheus.
Foi projetado para ser econômico e fácil de manter.

Diferente de outras ferramentas, o Loki indexa apenas os metadados dos logs (labels).


<style>
  img {
  display: block;
  margin: auto;
}
</style>

![loki](/loki.png){width=76%}

<br>
<footer>

[https://grafana.com/docs/loki/](https://grafana.com/docs/loki/latest/)

</footer>

---
transition: slide-left
level: 3
---

# Grafana

Grafana é uma ferramenta de visualização que permite que você faça consultas, visualize, crie alertas e explore suas métricas, rastros e logs 
onde quer que estejam armazenados.

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![grafana](/grafana-dashboard.png){width=65%}

[https://github.com/grafana/grafana](https://github.com/grafana/grafana)


---
transition: slide-left
level: 3
---

# Tempo
Backend para rastreamento distribuído, otimizado para custos e tem como pre-requisito apenas um armazenamento de objetos para funcionar.

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![tempo](/tempo.png){width=76%}

<footer>

[https://github.com/grafana/tempo](https://github.com/grafana/tempo)

</footer>

---
transition: slide-left
level: 3
---

# Mimir
Solução para armazenamento escalável e de longo prazo para métricas.

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![tempo](/mimir.svg){width=76%}

<br>

<footer>

[https://github.com/grafana/mimir](https://github.com/grafana/mimir)

</footer>

---
transition: slide-left
layout: section
level: 3
---

# Outras Ferramentas da Grafana Labs

---
transition: slide-left
level: 3
---

# Beyla
Ferramenta para auto instrumentação baseada em eBPF, com suporte para muitas linguagens, como Go, C/C++, Rust, Python, Ruby, Java.
Todos os dados capturados sem nenhuma alteração no código da aplicação ou outra configuração.

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![beyla](/beyla.png){width=64%}

<footer>

[https://github.com/grafana/beyla](https://github.com/grafana/beyla)

</footer>

---
transition: slide-left
level: 3
---

# Faro
Um projeto para observabilidade de frontend, inclui um SDK para monitoramento de usuários em tempo real (RUM).

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![faro](/grafana-faro.png){width=58%}

<footer>

[https://github.com/grafana/faro-web-sdk](https://github.com/grafana/faro-web-sdk/)

</footer>

---
transition: slide-left
level: 3
---

# Alloy
Alloy é uma distribuição do (OTel) Collector mantida pela Grafana Labs. É totalmente compatível com os padrões de observabilidade de código aberto mais populares, como OpenTelemetry (OTel) e Prometheus.

<style>
  img { 
  display: block;
  margin: auto;
}
</style>

![faro](/grafana-allow.png){width=80%}

<footer>

[https://github.com/grafana/alloy](https://github.com/grafana/alloy)

</footer>

---
transition: slide-left
level: 3
---

## Instalação/Configuração

* Para instalação em Kubernetes, você pode usar os [Helm Charts disponíveis](https://github.com/grafana/helm-charts/tree/main/charts).
* Cada projeto tem suas configurações específicas


---
transition: slide-left
layout: section
level: 2
---

# Prometheus

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![prometheus](/prometheus.png){width=8%}

---
transition: slide-left
hideInToc: true
layout: quote
level: 3
---

<br>

O Prometheus é um conjunto de ferramentas de monitoramento e alerta de código aberto que cresceu em popularidade junto com o crescimento do Kubernetes.

<br>

Funcionalidades:

- Modelo de dados multi dimensional com dados de série temporal (time serie) identificados pelo nome da métrica e pares de chave/valor
- Uma linguagem para consulta das métricas: PromQL
- A coleta dos dados acontece por meio de um modelo pull via HTTP (para coleta via push é feito via um Gateway intermediário)

<br>
<br>

<footer>

[https://prometheus.io/docs/introduction/overview/](https://prometheus.io/docs/introduction/overview/)

</footer>

---
transition: slide-left
hideInToc: true
level: 3
---

# Componentes

Componentes (sendo que alguns são opcionais):

- Servidor Principal, responsável por fazer scrape e armazenar os dados time series
- Bibliotecas clientes, para instrumentar as aplicações
- Push Gateway, para jobs efêmeros (e batchs) expor métricas
- Exporters, para ajudar a exportar métricas de serviços terceiros para o Prometheus
- Alert Manager, para gerenciamento de alertas a partir do Prometheus

<br>
<br>

<footer>

[https://prometheus.io/docs/introduction/overview/](https://prometheus.io/docs/introduction/overview/)

</footer>


---
transition: slide-left
level: 3
---

## Instalação/Configuração

* Para instalação em Kubernetes, pode usar os [Charts (Helm)](https://github.com/prometheus-community/helm-charts/tree/main/charts) do projeto.
* Existem alguns Charts customizados, por exemplo:
  * [kube-prometheus-stack](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack)


---
transition: slide-left
level: 1
---

# Considerações Finais

- Observabilidade é diferente de monitoramento
- Entenda bem suas aplicações e o que precisa de telemetria antes de implementar uma ferramenta (ou stack)
- Observabilidade pode ser cara/custosa
- Observabilidade é uma jornada, vai muito além de logs, rastros e métricas

---
layout: statement
hideInToc: true
---

# Dúvidas?

<br>

[edsoncelio.dev/esquenta-dod-fortaleza-2024](https://edsoncelio.dev/esquenta-dod-fortaleza-2024)
