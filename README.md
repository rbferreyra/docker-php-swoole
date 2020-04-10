# Docker Swoole

## Arquivo Dockerfile

### Para executar a aplicação a partir do arquivo Dockerfile, execute os comandos abaixo

Montar a aplicação a partir do arquivo Dockerfile:

```bash
docker build -t php-swoole .
```

* Comando `build` monta a imagem
* A flag `-t` é o nome / tag da imagem, e.g. `php-swoole`
* O ponto `.` significa executar a partir do arquivo Dockerfile, apontando para o caminho atual

Rodar a aplicação:

```bash
docker run -d --name=swoole -p 9501:9501 php-swoole
```

* Comando `run` significa rodar o container
* A flag `-d`  aponta pra rodar o container em segundo plano, não interrompendo o processo
* A flag `--name` é o nome do container, e.g. `swoole`
* A flag `-p` define a porta, e.g. `9501:9501`
* O último argumento é o nome da imagem, e.g. `php-swoole`

Acessa a aplicação pelo url:

[http://localhost:9501](http://localhost:9501)

## Subir imagem para o repositório

Montar a imagem:

```bash
docker build -t rbferreyra/php-swoole:latest .
```

Subir imagem:

```bash
docker push -t rbferreyra/php-swoole:latest
```

## Baixar Imagem do repositório

### Para rodar a aplicação a partir de uma imagem, basta rodar os comandos abaixo

Repositório da imagem

[https://hub.docker.com/r/rbferreyra/php-swoole](https://hub.docker.com/r/rbferreyra/php-swoole)

Baixar a imagem da aplicação:

```bash
docker pull rbferreyra/php-swoole
```

Rodar a aplicação:

```bash
docker run -d --name=swoole -p 9501:9501 rbferreyra/php-swoole:latest
```

Acessa a aplicação pelo url:

[http://localhost:9501](http://localhost:9501)

## Dockerfile

```bash
FROM php:7.3-cli
```

Define a imagem a ser executado

Biblioteca de imagens disponíveis no [https://hub.docker.com](https://hub.docker.com)

* * *

```bash
RUN pecl install swoole \
    &&  docker-php-ext-enable swoole
```

Executar comandos na imagem. Nesse solicita instalar o swoole e habilitar a extensão do Swoole no PHP

* * *

```bash
COPY index.php /var/www
```

Copia o arquivo index.php para o diretório da imagem

* * *

```bash
EXPOSE 9501
```

Expõe porta a porta, para acessar a aplicação fora da imagem

* * *

```bash
ENTRYPOINT ["php","/var/www/index.php","start"]
```

Ao rodar o container, o mesmo não persiste a execução, sendo interrompido. Nesse caso, aplica um comando para rodar a aplicação, persistindo o processo do container
