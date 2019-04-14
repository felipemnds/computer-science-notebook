
>  ***Lista de Referências:***
> 1. http://www.caelum.com.br/apostila-java-testes-xml-design-patterns/testes-automatizados/#3-4-testes-de-unidade
> 2. https://www.youtube.com/watch?v=Q2zBRTgKXHo

# Parte 1. Teste de Unidade
**Testes de unidade** são testes que testam apenas uma classe ou método, verificando se seu comportamento está de acordo com o desejado.
> Mas lembre-se sempre: testes de unidade testam **apenas** unidades (métodos isolados)!
# Parte 2. JUnit
O **JUnit** (junit.org) é um framework muito simples para facilitar a criação destes testes de unidade e em especial sua execução.
## 1) Convenções e Anotação
Para cada classe, teremos uma classe correspondente (por convenção, com o sufixo `Test`) que contará todos os testes relativos aos métodos dessa classe. Essa classe ficará no pacote de mesmo nome, mas na _Source Folder_ de testes (`src/test/java`).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQyNTY2NTY3MiwxNDQyMjk5NTcwLDQ5Mj
AxMjg0MF19
-->