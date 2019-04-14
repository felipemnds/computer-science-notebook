
>  ***Lista de Referências:***
> 1. http://www.caelum.com.br/apostila-java-testes-xml-design-patterns/testes-automatizados/#3-4-testes-de-unidade
> 2. https://www.youtube.com/watch?v=Q2zBRTgKXHo

# Parte 1. Teste de Unidade
**Testes de unidade** são testes que testam apenas uma classe ou método, verificando se seu comportamento está de acordo com o desejado.
> Mas lembre-se sempre: testes de unidade testam **apenas** unidades (métodos isolados)!
# Parte 2. JUnit
O **JUnit** (junit.org) é um framework muito simples para facilitar a criação destes testes de unidade e em especial sua execução.
## 1) Convenções e Anotação
Ao invés de usarmos uma `main`, criamos um método com nome expressivo (normalmente com `test` como prefixo), além de inserir a notação `@Test` antes da declaração do método.
```
public class CandlestickFactoryTest {

 @Test  public void sequenciaSimplesDeNegocios() {
    // ...
  }
}
```
E ainda dentro deste método de testes, cada tentativa é chamada de **Assert**, com o valor *esperado* e o valor *atual*:
`Assert.assertEquals(40.5, candle.getAbertura(), 0.00001);`
## 2) Facilite sua vida com o import estático
Ao importar a biblioteca do JUnit, faça da seguinte maneira:
```
 import static org.junit.Assert.*;
 ```
 Assim, os métodos podem ser utilizados sem que seja necessário citar a classe antes de cada declara
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU0OTE2OTQ4LDE2MDA0MjA0NjMsMTQ0Mj
I5OTU3MCw0OTIwMTI4NDBdfQ==
-->