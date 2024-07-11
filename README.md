# Dominando os Princípios SOLID: Exemplos Práticos com Java

## Introdução

- **Autor:** Sandro Ramos
- **Objetivo:** Compreender os conceitos de **princípios SOLID** através de exemplos práticos.
- **Importância:** Essencial para a correta aplicação da **arquitetura limpa**.

## SRP: Single Responsibility Principle (Princípio da Responsabilidade Única)

### Definição

- Uma classe deve ter uma única responsabilidade, ou seja, **uma razão para mudar**.

### Exemplo de Violação

- Classe **ProcessaPedido**:
  - Método **processaPedido()**: Processa o pedido.
  - Método **salvar()**: Conecta ao banco de dados.
  - Método **enviarEmailConfirmacao()**: Envia um email de confirmação via SMTP.

### Problemas

- A classe tem múltiplas razões para mudar:
  - Mudança na regra de negócio.
  - Mudança no banco de dados.
  - Mudança no provedor de SMTP.

### Solução

- Separar responsabilidades:
  - **PostgresRepository**: Conexão com banco de dados.
  - **EnviarEmailConfirmacao**: Envio de email.
  - **ProcessaPedido** utiliza essas classes para cumprir sua responsabilidade.

### Benefícios

- Facilita a **manutenção** e **testabilidade**.
- Cada classe tem uma única razão para mudar.

## OCP: Open Closed Principle (Princípio do Aberto-Fechado)

### Definição

- Classes devem estar abertas para extensão, mas fechadas para modificação.

### Exemplo de Violação

- Adicionar validações diretamente na classe **ProcessaPedido**.

### Problemas

- Alterar diretamente a classe viola o OCP.

### Solução

- Utilizar **herança**:
  - Criar uma nova classe que herda de **ProcessaPedido** e adicionar as novas validações na classe filha.

### Benefícios

- Evita modificar classes existentes.
- Facilita a extensão de funcionalidades.

## LSP: Liskov Substitution Principle (Princípio da Substituição de Liskov)

### Definição

- Classes filhas devem poder substituir classes pais sem quebrar a aplicação.

### Exemplo de Violação

- Classe **PedidoValidadorEstoque**:
  - Valida o estoque e retorna **true** ou **false**.
- Nova classe **PedidoValidadorEstoqueEmbalagem**:
  - Valida estoque e embalagem, mas retorna exceção em vez de **false** quando a embalagem é inválida.

### Problemas

- Quebra a substituição de classes pai por classes filhas.

### Solução

- As classes filhas devem retornar valores esperados pela classe pai.

### Benefícios

- Mantém a **integridade** do esquema de herança.
- Facilita a substituição de classes sem problemas inesperados.

## ISP: Interface Segregation Principle (Princípio da Segregação de Interface)

### Definição

- Uma classe não deve ser forçada a implementar interfaces que não utiliza.

### Exemplo de Violação

- Interface **GerarRelatorioDeVendas**:
  - Métodos **gerarExcel()** e **gerarPDF()**.
- Classe **DataScience**:
  - Implementa **gerarExcel()** mas **gerarPDF()** é inútil para ela.

### Problemas

- Implementação de métodos inúteis.

### Solução

- Segregar interfaces:
  - **GerarRelatorioExcel** e **GerarRelatorioPDF**.
- Classes implementam apenas as interfaces necessárias.

### Benefícios

- Evita a implementação de métodos inúteis.
- Torna as interfaces mais específicas e **relevantes** para cada classe.

## DIP: Dependency Inversion Principle (Princípio da Inversão de Dependência)

### Definição

- Módulos de alto nível não devem depender de módulos de baixo nível, ambos devem depender de abstrações.

### Exemplo de Violação

- Classe **ProcessaPedido** depende diretamente de **PostgresRepository** e **EnviarEmailConfirmacao**.

### Problemas

- Mudanças nos detalhes (como o banco de dados) exigem mudanças na funcionalidade.

### Solução

- Utilizar **interfaces** para abstrair os detalhes:
  - **BancoDeDados** e **EnviarEmail**.
  - **PostgresRepository** e **OracleRepository** implementam **BancoDeDados**.

### Benefícios

- Desacopla código.
- Facilita mudanças e expansões sem alterar classes de alto nível.

## Conclusão

- Aplicação dos princípios **SOLID**:
  - Melhoram a **manutenibilidade**, **testabilidade** e **flexibilidade** do código.
  - Promovem um desenvolvimento mais **robusto** e **sustentável**.
