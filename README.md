# Clothes4Happiness - POC de CI/CD com Docker e GitHub Actions

Este repositório é a prova de conceito (POC) da atividade avaliativa de Computação em Nuvem e DevOps. A proposta era mostrar, na prática, como funciona a atualização automatizada de um sistema usando Docker, GitHub Actions e os conceitos de CI/CD que estudamos.

## Sobre o projeto

A empresa fictícia da atividade é a Clothes4Happiness. Para representar o sistema dela, criei uma página simples em HTML e CSS que funciona como um painel mostrando o status da transformação digital da empresa: nuvem, Docker, pipeline de CI/CD, segurança, sistemas que ainda estão em planejamento (como ERP e CRM) e a cultura DevOps.

Essa página fica dentro de um container Docker, simulando o "servidor" da empresa.

## Como funciona a automação

A ideia é que toda vez que eu altero o código e envio pro GitHub, o processo de atualização aconteça sozinho, sem eu precisar fazer nada manualmente na parte de build da imagem. O caminho é mais ou menos assim: eu mudo algo no código, dou push no GitHub, isso dispara o GitHub Actions, que constrói uma nova imagem Docker e publica ela no Docker Hub. Depois disso, o container que representa o servidor é atualizado com essa imagem nova.

O arquivo que configura essa automação é o `.github/workflows/deploy.yml`. Ele diz pro GitHub Actions: sempre que houver um push na branch main, faça o login no Docker Hub usando as credenciais guardadas em segredo (secrets), construa a imagem a partir do Dockerfile e publique ela.

## O papel de cada ferramenta

O GitHub guarda o código e todo o histórico de alterações do projeto. O GitHub Actions é quem automatiza a parte de build e publicação da imagem, sem precisar que eu faça isso manualmente. O Docker empacota a aplicação de um jeito que ela roda igual em qualquer lugar, sem depender de configurações específicas da máquina. O Docker Hub é onde a imagem gerada fica guardada, pronta para ser usada pelo servidor. E o CI/CD é justamente esse processo todo: a parte de integração contínua garante que toda mudança seja testada e construída automaticamente, e a de entrega contínua garante que essa mudança fique disponível para uso.

## Estrutura do repositório

O projeto tem o arquivo `index.html`, que é a aplicação em si, o `Dockerfile`, que tem as instruções para montar o container, e a pasta `.github/workflows`, que guarda o arquivo `deploy.yml` com a configuração da automação.

## Como rodar localmente

Para testar o projeto na sua própria máquina, depois de clonar o repositório, é só rodar estes dois comandos no terminal:

Depois é só acessar `http://localhost:8080` no navegador.

## Testando a atualização automática

Para comprovar que a automação funciona, fiz o seguinte teste: mudei o número da versão que aparece no cabeçalho da página, de v1.0 para v1.1, e dei push no GitHub. O GitHub Actions rodou sozinho e publicou a nova imagem no Docker Hub. Depois disso, atualizei o container local puxando essa imagem nova, e o site passou a mostrar v1.1, confirmando que o ciclo completo estava funcionando.

## Autoria Taiane Silva de Oliveira - José Augusto da Silva Bertolino Falcão

Atividade avaliativa de Computação em Nuvem e DevOps, empresa fictícia Clothes4Happiness.