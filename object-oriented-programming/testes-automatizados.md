
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
## 2) Tabela de Referência para JUnit
| JUnit 4 | Descrição |
|--|--|
| `import org.junit.*` | Importar o necessário para usarmos os termos abaixo|
| `@Test` | Identifica um método como um método de teste |
| `@Before` | Usado para preparar o ambiente de teste. Executado antes de cada teste. |
| `@After` | Executado depois de cada teste. Usado para limpar o ambiente após o teste. |
| `@BeforeClass` | Executado uma vez antes de todos os testes. Precisam ser definidos como `static` |
| `@AfterClass` | Executado uma vez depois de todos os testes. Precisam ser definidos como `static` |
| `@Ignore` or `@Ignore("Motivo de estar desabilitado")`| Marca que o teste em questão está desabilitado |
| `@Test (expected = Exception.clas)` | Falha se o método não jogar a exceção citada |
| `@Test (timeout=100)` | Falha se o método demorar mais do que 100 milisegundos |
## 3) Facilite sua vida com o import estático
Ao importar a biblioteca do JUnit, faça da seguinte maneira:
```
 import static org.junit.Assert.*;
 ```
 Assim, os métodos podem ser utilizados sem que seja necessário citar a classe antes de cada declaração:
 ```
 class TesteMatematico {

  @Test
  void doisMaisDois() {
    assertEquals(4, 2 + 2);
  }
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NTc3MzYwMzIsMTYwMDQyMDQ2MywxND
QyMjk5NTcwLDQ5MjAxMjg0MF19
-->