Chat com a biblioteca socket.io rodando com Node

1- instalar o framework express com o seguinte comando:

npm install -g express-generator

2- após a instalação do framework express vamos criar um novo projeto

express -e chatdemo
O -e indica que vamos usar a view-engine EJS que usa HTML+JS 

3- Também vamos instalar o nodemon para aplicar nossas atualizações automaticamente sem precisar
fiar reiniciando nosso servidor 

npm install nodemon --save

no package.json devemos deixar a linha start dessa forma:
     "start": "nodemon ./bin/www"

e com o comando npm start o nodemon automaticamente sera carregado

4- logo em seguida devemos instalar o socket.io

npm install socket.io --save

5-

