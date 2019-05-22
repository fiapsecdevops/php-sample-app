# Sistemas para Internet - NAC: Teste de Aplicação usando Docker + PHP

**Objetivo:** Executar o passo-a-passo abaixo configurando e entregando uma aplicação PHP encapsulada em Docker através da solução ["Docker Compose](https://docs.docker.com/compose/);

- Durante a execução dos testes observar o modelo de entrega e as diferenças em relação a uma entrega tradicional;

---

Esta app foi adaptada do exemplo contido [neste artigo](https://www.tutorialrepublic.com/php-tutorial/php-mysql-crud-application.php)

# Execução:

1. Fork do repositório:

    1.1 Usando sua conta do Github crie um fork do seguinte repositório: [https://github.com/fiapsecdevops/php-sample-app](https://github.com/fiapsecdevops/php-sample-app);

    1.2 Em seguida faça um clone para o Desktop local;

2. Criando a configuração de deploy da aplicação:

2.1 **No diretório raiz do projeto** crie um arquivo com o nome **docker-compose.yml** (É muito importante que este nome seja respeitado na criação do arquivo);

2.2 Preencha a configuração do arquivo com o seguinte conteúdo:

```sh
db:
  build: ./backend
  restart: always
  ports:
    - "${MYSQL_PORT}:3306"
  volumes:
    - /var/lib/mysql
  environment:
    - MYSQL_ROOT_PASSWORD=${DB_ROOT_PASSWORD}
    - MYSQL_USER=${DB_USERNAME}
    - MYSQL_PASSWORD=${DB_PASSWORD}
    - MYSQL_DATABASE=${DB_NAME}
  env_file: ./.env
php:
  build: ./frontend
  restart: always
  ports:
    - "${PHP_PORT}:80"
  volumes:
    - ./frontend:/var/www/html
  env_file: ./.env
  links:
    - db
```

2.3 Faça um commit desta alteração no seu repositório;

3. Acesso ao servidor de teste da Aplicação:

Para execução da atividade foi provisionado um Host Linux no provedor de núvem AWS para cada aluno entregar e testar a aplicação, o acesso a este host pode ser executado usando o seguinte endereço:

**nac-rm<seu_rm>.fiapdev.com**

3.1 Acesso o servidor usando o Putty:

    Usuário: ubuntu
    Senha:   (Uso da chave entregue no começo da atividade)

4. Deploy da aplicação:

4.1 Faça um clone do repositório criado no diretório /home/developer (sua pasta atual) no servidor acessado:

```sh
git clone  https://github.com/<SUA_CONTA_GIT>/php-sample-app
cd php-sample-app
```

4.2 Em seguida verifique se o Docker e o Docker Compose estão em execução:

```sh
docker ps
docker-compose --version
```

4.3 Com a configuração entregue anteriormente temos o script que será usado para iniciar a aplicação e conectar no banco MySQL, para isso execute:

```sh
docker-compose up -d
```

4.4 Verifique se a aplicação está em execução conforme esperado:

```sh
docker ps
```

Finalmente com a aplicação em execução faça o acesso no navegador pelo mesmo endereço usado para Login:
- **nac-rm<seu_rm>.fiapdev.com**

---

Ao finalizar o exercício de exemplo responda as questões propostas no Link abaixo:

[Questionário de entrega NAC](https://pt.surveymonkey.com/r/9DQ2GFC)

![QR_code](images/QR_code_9DQ2GFC.png)

---

Creditos do setup do compose: [@PatrickRNG](https://github.com/PatrickRNG)
