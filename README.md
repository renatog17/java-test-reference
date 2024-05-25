# Testes de Software

Testes de Software são uma parte crucial no desenvolvimento de software. Através de testes unitários é possível verificar a consistência em métodos isolados de um software, através de testes integrados, obter resultados relativos à consultas em banco de dados, integração com outras API's como também com bibliotecas externas.
A gama de testes disponíveis não para por então. É possível ainda fazer testes de carga e de usabilidade, garantindo a escalabilidade e user experience adequadas.

## Testes Unitários
Para escrever testes unitários, diversas linguagens dispõe de seus próprios frameworks e bibliotecas, como o caso da linguagem Java, que possui o JUnit, que será utilizado neste material.

Testes de unidade, são essenciais para testar unidades isoladas de um código. Essas unidades, em Java, podem ser métodos. A característica primordial deste tipo de teste é garantir que partes isoladas do código estão funcionam bem e que continuarão funcionando após a implementação de novos métodos.

### Escrevendo Testes Unitários

A criação de testes segue um padrão onde uma determinada classe, que possue métodos a serem testados, terá uma respectiva classe de teste. A nomenclatura pode seguir o seguinte padrão:
* ``` <<nome_da_classe>> ```: nome da classe; 
* ``````<<nome_da_classe>>Test```: classe de testes.
