---
title: "Wordpress com alta disponiblidade na AWS - Parte 1"
date: 2021-06-14T19:14:26-03:00
draft: false
---

Esse post faz parte de uma série de posts sobre como implementar uma aplicação monolítica na AWS com alta disponibilidade, elasticidade e resiliência. Iremos utilizar o Wordpress em nosso exemplo, um sistema de gerenciamento de conteúdo (CMS) de código aberto, baseado em PHP e MySQL muito versátil e bastante utilizado no mundo para criar sites, blogs, fóruns e e-commerce. Não é atoa que segundo a w3ctechs em 2021, [40% da web](https://w3techs.com/blog/entry/40_percent_of_the_web_uses_wordpress) no mundo utiliza o wordpress. Contudo, a arquitetura que iremos desenvolver na nuvem da AWS não se limita apenas ao wordpress, mas, se aplica também para a grande maioria das aplicações monolíticas, como o Magento, Moodle entre outras tantas.

Qualquer site WordPress fornece conteúdo estático e dinâmico. O conteúdo dinâmico é gerado no lado do servidor usando o PHP e esse processo ocorre a cada requisição que o servidor recebe. Já o conteúdo estático que inclui imagens, arquivos JavaScript e folhas de estilo é entregue de forma mais rápida, pois como o próprio nome diz, ele é estático e não muda e já está lá pronto para ser entregue. Acelerar a entrega de conteúdo melhora significativamente a experiência final do usuário. E isso pode ser obtido com a utilização de cache tanto para o conteúdo estático como para o dinâmico.
 
A solução proposta mostra como executar o WordPress sem servidor utilizando o Amazon ECS no AWS Fargate. Criaremos um VPC com duas sub-redes públicas e privadas em duas Zonas de disponibilidade (AZ A e B) e um NAT Gateway em cada AZ. Criaremos também um cluster ECS para os containers do WordPress. Uma instância RDS MySQL para o banco de dados. ElastiCache (memcached) para o cache do banco de dados. Um sistema de arquivos EFS onde o WordPress manterá seus dados compartilhados. E o Amazon CloudFront (CDN) para aproximar o conteúdo estático do cliente diminuindo a latência da rede.


![Wordpress.png](/Wordpress_ECS_FARGATE_3D.png)

Essa primeira parte é teórica, e tem como objetivo apresentar a solução. Da segunda parte em diante, vamos começar a  aplicar o que foi visto aqui. Enfim, chega de papo e vamos para a prática!