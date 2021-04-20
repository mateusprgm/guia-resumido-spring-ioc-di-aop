**Pojo(Plain Old Java Object):** 

É uma classe Java normal que não precisa implementar nenhuma interface ou possuir determinada anotação para que possa ser gerenciada por um framework.

Container deve satisfazer três requisitos: 

- Ser configurável.
- Controlar o ciclo de vida dos seus objetos.
- prover métodos de obtenção.

**Lookup:**

Usamos esta expressão para designar a obtenção de objetos a partir de um container.
Todo container deve prover alguma interface que nos forneça métodos que possibilitem obter objetos a partir do seu nome ou tipo.

No código abaixo, quando executamos o método lookup no objeto Context, estamos executando a obtenção de um objeto já preparado pelo container para execução.

	Context ctx = InitialContext();

	//Lookup em ação:
	Object objeto = ctx.lookup("meuObjeto");



**Bean** - É um objeto que possui seu ciclo de vida gerenciado pelo container de IoC/DI do Spring.

Uma boa maneira de entender como a inversão de controle se aplica é descrever o que vêm a ser o tal do ciclo de vida. Deve ser visto como um componente. O que diferencia um componente dos demais objetos, como um JavaBean, por exemplo, são as seguintes características:

- Possui baixa granularidade, ou seja, seus clientes não precisam saber quais as suas dependências internas.
- O que realmente importa para seus clientes é a interface disponibilizada pelo objeto, que define quais os serviços oferecidos pelo mesmo(é o seu contrato);
- São facilmente substituíveis por outras implementações que mantenham o mesmo contrato(plugabilidade).

**JavaBean:**

Foi um padrão adotado pela Sun para a escrita de componentes reutilizáveis. Todo JavaBean deve satisfazer três condições:

1 - Deve possuir um construtor público que não receba parâmetros.
2 - Todos os seus atributos visíveis devem ser declarados como privados(ou protegidos) e acessados apenas por métodos get & set.
3 - Deve implementar a interface java.io.Serializable.

**Exemplo: **

	Public class Pessoa implements java.io.Serializable {
		// construtor publico sem argumentos
		public Pessoa() {}

		private String nome;

		//getter
		public String getNome() {return this.nome;}

		//setter
		public void setNome(String valor) {this.nome = valor;}
	}


**Ciclo de Vida:**

O Ciclo de vida diz respeito às etapas de execução de um objeto. As fases pelas quais um objeto de negócio passa durante a execução de um programa são citados abaixo:

1 - O Objeto é instanciado.
2 - Se houverem dependências a serem injetadas no objeto, estas devem ser injetadas;
3 - Se após as dependências tiverem sido injetadas for necessário executar um método de inicialização, este deverá ser invocado;
4 - O objeto já inicializado e com todas as suas dependências injetadas é enviado ao cliente que dele necessita;
5 - Uma vez não mais necessário, existindo um método destrutor, este deverá ser invocado e o objeto descartado do container.

**Resumo de responsabilidade a grosso modo:**
	
- **IOC** - Controla o ciclo de vida de nossas aplicações.
- **DI** - Define quais classes iremos instanciar e quais lugares iremos injetá-las.
- **AOP** - Adiciona novos comportamentos as classes de forma transparente elas.

**IOC/DI** - Inversion of Control/Dependency Injection

Na inversão de controle, não é a classe cliente a responsável por definir quais serão suas dependências.
Esta responsabilidade é delegada a um container de injeção de dependências.

**AOP - Aspect Oriented Programming**

Comportamentos que aparecem por toda a aplicação que não estão necessariamente relacionados à lógica de negócio
que estamos implementando. Esse tipo de comportamento costuma gerar uma infinidade de código repetitivo espalhado por todo sistema. Chama-se este comportamento secundário de Aspecto.

**Exemplo de aspecto:**

	public class ClasseMuitoImportante{
		private ControleAcesso controleAcesso;

		public void metodoImportante(){
			if(controleAcesso.possuiPermissaoParaTal()){
				//executa código importante
			}
		} 
	}

	public class OutraClasseMuitoImportante{
		private ControleAcesso controleAcesso;

		public void apagarTudo(){
			if(controleAcesso.possuiPermissaoParaTal()){
				//Apaga tudo
			}
		} 
	}

Como visto acima, o exemplo, em duas classes, o mesmo código se repete, temos assim o exemplo de aspecto.
A forma de evitar esse disco arranhado é justamente o uso da AOP, pois ao invés de precisar escrever
o mesmo código em mais de uma classe, o AOP intercepta as chamadas de métodos em tempo de execução, de forma a evitar o alto acoplamento. Podendo alterar o comportamento da classe, sem que estas sequer saibam disto.
