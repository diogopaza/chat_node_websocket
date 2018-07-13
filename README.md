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

5-do lado servidor configurar o socket.io


var io = require('socket.io').listen(server);
io.on('connection', function(socket){
  console.log('a user connected')
})

repare que ele passe o server no metodo listen que é o objetdo express.
ou seja você deve configurar o socket.io no seu arquivo onde você levanta o servidor express,
logo após o metodo createServer

6- no cliente devemos apontar para o arquivo js do nosso socket

<script src='/socket.io/socket.io.js'></script>

let socket = io('http://localhost:3000')
e apos isso adicinaremos um eventos ao botao

meuForm =  document.querySelector('form')
meuForm.addEventListener('submit', function(e){
          //e.preventDefault()
         
          dados =  document.getElementById('m').value
        
          socket.emit('chat message', dados)
         return;
                  
        })

o socket.emit ira enviar as informações do input para o back-end

7-Até aqui temos uma comunicação unidirecional, ou seja o cliente 
envia informações e o servidor as exibe no console.
Para o cliente também receber dados do servidor
devemos alterar para esse código

socket.on('chat message', function(msg){
  
   io.emit('chat',msg)
 
  })

ou seja o sockete  está escutando o cliente através do chat message
logo após receber essas informações o back-end irá replicar para todos 
os que estiverem ouvindo o 'chat' atraves do io.emit('chat')
Também precisamos modificar nosso cliente para que
ele exiba as mensagens na tela

socket.on('chat', function(msg){
          minhasMensagens = document.getElementById('messages').innerHTML += '<li>' + msg + '<li>'
         
        })












