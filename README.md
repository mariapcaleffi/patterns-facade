# Design Pattern - FACADE 🏡

A estrutura Facade é um padrão de design estrutural da programação orientada a objetos. Ele serve para simplificar a interação com sistemas complexos, fornecendo uma interface unificada que oculta a complexidade do sistema subjacente.   

### Quando utilizar o método Facade ❓

- para simplificar o uso de um sistema complexo.
- para criar uma interface de alto nível que delega tarefas para subsistemas mais detalhados.
- para ajudar na organização do código, separando as camadas de lógica.
<br>

### Como funciona? 🖥

O Facade define uma interface simplificada para um subsistema de objetos, mas ele não introduz qualquer nova funcionalidade. O próprio subsistema não está ciente da fachada. Objetos dentro do subsistema podem se comunicar diretamente. O Mediator centraliza a comunicação entre componentes do sistema.

```
// clientes
class Cliente {
    constructor(nome) {
        this.nome = nome;
    }
}

// pedidos
class Pedido {
    constructor(cliente, produto) {
        this.cliente = cliente;
        this.produto = produto;
    }
}


class SistemaFacade {
    constructor() {
        this.clientes = [];
        this.pedidos = [];
    }

    adicionarCliente(nome) {
        const cliente = new Cliente(nome);
        this.clientes.push(cliente);
        console.log(`Cliente adicionado: ${cliente.nome}`);
    }

    criarPedido(nomeCliente, produto) {
        const cliente = this.clientes.find(c => c.nome === nomeCliente);
        if (cliente) {
            const pedido = new Pedido(cliente, produto);
            this.pedidos.push(pedido);
            console.log(`Pedido criado para ${cliente.nome}: ${produto}`);
        } else {
            console.log(`Cliente ${nomeCliente} não encontrado.`);
        }
    }
}

// Uso do Facade
const sistema = new SistemaFacade();

sistema.adicionarCliente("Alice");
sistema.adicionarCliente("Bob");

sistema.criarPedido("Alice", "Produto A");
sistema.criarPedido("Carlos", "Produto B"); // Este cliente não existe
```
<br>

- `adicionarCliente(nome)`: Adiciona um novo cliente à lista de clientes. Este método é simples e não expõe a complexidade de como os clientes são armazenados.
- `criarPedido(nomeCliente, produto)`: Cria um pedido para um cliente existente. Ele verifica se o cliente está na lista e, se estiver, cria o pedido. Se o cliente não for encontrado, exibe uma mensagem de erro.

- o cliente (ou usuário do sistema) interage apenas com a classe `SistemaFacade`, sem precisar se preocupar com os detalhes de implementação das classes Cliente e Pedido.
- isso torna o código mais limpo e fácil de entender, pois o usuário não precisa saber como os clientes e pedidos são gerenciados internamente.


<br>

|Vantagens| Desvantagens|
|-|:-:|
|Reduz o acoplamento entre o cliente e os subsistemas.|Funcionalidades importantes podem ser ocultadas.|
|Centraliza o controle de operações complexas.|Clientes podem se tornar dependentes da interface, dificultando mudanças.|
|Facilita a manutenção e expansão do sistema.|Mudanças no subsistema podem exigir atualizações frequentes na Facade.|
||Podem gerar sobrecarga no desempenho.|

<br>

##### Feito por: Gabriela, Heloísa, Lohaine, Maria e Miriam