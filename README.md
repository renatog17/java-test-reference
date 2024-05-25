# Testes de Software

Testes de Software são uma parte crucial no desenvolvimento de software. Através de testes unitários é possível verificar a consistência em métodos isolados de um software, através de testes integrados, obter resultados relativos à consultas em banco de dados, integração com outras API's como também com bibliotecas externas.
A gama de testes disponíveis não para por então. É possível ainda fazer testes de carga e de usabilidade, garantindo a escalabilidade e user experience adequadas.

## Testes Unitários
Para escrever testes unitários, diversas linguagens dispõe de seus próprios frameworks e bibliotecas, como o caso da linguagem Java, que possui o JUnit, que será utilizado neste material.

Testes de unidade, são essenciais para testar unidades isoladas de um código. Essas unidades, em Java, podem ser métodos. A característica primordial deste tipo de teste é garantir que partes isoladas do código estão funcionam bem e que continuarão funcionando após a implementação de novos métodos.

### Escrevendo Testes Unitários

A criação de testes segue um padrão onde uma determinada classe, que possue métodos a serem testados, terá uma respectiva classe de teste. A nomenclatura pode seguir o seguinte padrão:
* ``` <<nome_da_classe>> ```: nome da classe; 
* ```<<nome_da_classe>>Test```: classe de testes.

Esta nomenclatura pode ser vista a seguir, nas classes Desconto e DescontoTest:
```
public class Desconto {
	public Double retornarPrecoComDesconto(Double precoCompra) {
		if (precoCompra < 0.0) {
			throw new IllegalArgumentException("O preço da compra não pode ser negativo.");
		}
		if (precoCompra >= 30.0) {
			precoCompra = precoCompra - (precoCompra * 0.10);
		}
		return precoCompra;
	}
}
```

```
public class DescontoTest {
	
}
```

A classe Desconto possue um método retornarPrecoComDesconto(Double precoCompra), que será o método utilizado neste material para implementação dos testes unitários.

Ao analisar o único parâmetro de entrada deste método ```precoCompra``` é possível estipular quais são os limites que esta variável vai suportar e os intervalos mais críticos para teste. Uma compra não pode ter valor negativo, logo, o valor sempre será maior que 0. Então é importante analisar o comportamento deste método com valores negativos, iguais a zeros, e baixos, mas superiores a zero.


Temos então os seguintes métodos de teste:

	@BeforeEach
	public void setUp() {
		desconto = new Desconto();
	}
	
	@Test
	public void testePracoValorNegativoExcecao() {
	    assertThrows(IllegalArgumentException.class, ()->{
	    	desconto.retornarPrecoComDesconto(-1.0);
	    }) ;
	}
	
	@Test
	public void testePrecoIgualAZero() {
		Double preco = desconto.retornarPrecoComDesconto(0.0);
		assertEquals(Double.valueOf(0.0), preco);
	}
	
	@Test
	public void testePrecoValorMuitoBaixo() {
		Double preco = desconto.retornarPrecoComDesconto(0.05);
		assertEquals(Double.valueOf(0.05), preco);
	}

Agora precisamos analisar outro ponto crítico do código, que é quando o valor for próximo a 30. Devemos aplicar os mesmo raciocínio e testar o preco igual a um valor abaixo de 30, igual a 30 e superior a 30.

	@Test
	public void testePrecoAbaixoDoLimiteDoDesconto() {
		Double preco = desconto.retornarPrecoComDesconto(29.99999);
		assertEquals(Double.valueOf(29.99999), preco);
	}
	
	@Test
	public void testePrecoExatamenteNoLimiteDoDesconto() {
		Double preco =  desconto.retornarPrecoComDesconto(30.0);
		assertEquals(Double.valueOf(27.0), preco);
	}	
	
	@Test
	public void testePrecoAcimaDoLimiteDoDesconto() {
		Double preco = desconto.retornarPrecoComDesconto(30.01);
		assertEquals(Double.valueOf(27.009), preco);
	}

 Por fim, devemos analisar os limites mais altos que podem ser recebidos como entrada. Para a regra de negócio vamos considerar que o valor máximo possível é R$1000,00. 

 	@Test
	public void testePrecoMuitoAlto() {
		Double preco = desconto.retornarPrecoComDesconto(1000.0);
		assertEquals(Double.valueOf(900.0), preco);
	}
