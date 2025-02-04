---
title: Como o Entity SQL difere do Transact-SQL
ms.date: 03/30/2017
ms.assetid: 9c9ee36d-f294-4c8b-a196-f0114c94f559
ms.openlocfilehash: 54d7a3fa8ce6e8a0aba6194bfc034eb4d47dbf60
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66489922"
---
# <a name="how-entity-sql-differs-from-transact-sql"></a>Como o Entity SQL difere do Transact-SQL
Este tópico descreve as diferenças entre [!INCLUDE[esql](../../../../../../includes/esql-md.md)] e Transact-SQL.  
  
## <a name="inheritance-and-relationships-support"></a>Suporte a herança e relações  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] trabalha diretamente com esquemas conceituais de entidade e dá suporte a recursos de modelo conceitual, como herança e relações.  
  
 Ao trabalhar com herança, geralmente é útil selecionar instâncias de um subtipo de uma coleção de instâncias de supertipo. O [oftype](../../../../../../docs/framework/data/adonet/ef/language-reference/oftype-entity-sql.md) operador na [!INCLUDE[esql](../../../../../../includes/esql-md.md)] (semelhante à `oftype` em C# sequências) fornece esse recurso.  
  
## <a name="support-for-collections"></a>Suporte para coleções  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] trata coleções como entidades de primeira classe. Por exemplo:  
  
- As expressões de coleção são válidas em uma cláusula `from`.  
  
- As subconsultas `in` e `exists` foram generalizadas para permitir quaisquer coleções.  
  
     Um subconsulta é um tipo de coleção. `e1 in e2` e `exists(e)` são as construções [!INCLUDE[esql](../../../../../../includes/esql-md.md)] para executar essas operações.  
  
- A operações de conjunto, como `union`, `intersect` e `except`, agora funcionam em coleções.  
  
- As junções funcionam em coleções.  
  
## <a name="support-for-expressions"></a>Suporte para expressões  
 Transact-SQL tem subconsultas (tabelas) e expressões (linhas e colunas).  
  
 Para dar suporte a coleções e coleções aninhadas, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] transforma tudo em uma expressão. [!INCLUDE[esql](../../../../../../includes/esql-md.md)] é mais Combinável do que o Transact-SQL — cada expressão pode ser usada em qualquer lugar. As expressões de consulta sempre resultam em coleções dos tipos projetados e podem ser usadas em qualquer lugar em que uma expressão de coleção seja permitida. Para obter informações sobre expressões de Transact-SQL que não têm suporte no [!INCLUDE[esql](../../../../../../includes/esql-md.md)], consulte [expressões sem suporte](../../../../../../docs/framework/data/adonet/ef/language-reference/unsupported-expressions-entity-sql.md).  
  
 Os itens a seguir são todos consultas [!INCLUDE[esql](../../../../../../includes/esql-md.md)] válidas:  
  
```  
1+2 *3  
"abc"  
row(1 as a, 2 as b)  
{ 1, 3, 5}   
e1 union all e2  
set(e1)  
```  
  
## <a name="uniform-treatment-of-subqueries"></a>Tratamento uniforme de subconsultas  
 Dada sua ênfase em tabelas, Transact-SQL realiza a interpretação contextual de subconsultas. Por exemplo, uma subconsulta no `from` cláusula é considerada um multiset (tabela). Mas a mesma subconsulta usada na cláusula `select` é considerada uma subconsulta escalar. Da mesma forma, uma subconsulta usada no lado esquerdo de uma `in` operador é considerado uma subconsulta escalar, enquanto o lado direito deve ser uma subconsulta multiset.  
  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] elimina essas diferenças. Uma expressão tem uma interpretação uniforme que não depende do contexto no qual é usada. [!INCLUDE[esql](../../../../../../includes/esql-md.md)] considera todas as subconsultas multiset subconsultas. Se desejar um valor escalar da subconsulta, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornece o `anyelement` operador que opera em uma coleção (neste caso, a subconsulta) e extrai um valor singleton da coleção.  
  
### <a name="avoiding-implicit-coercions-for-subqueries"></a>Evitando coerções implícitas para subconsultas  
 Um efeito colateral relacionado ao tratamento uniforme de subconsultas é a conversão implícita de subconsultas em valores escalares. Especificamente, no Transact-SQL, um multiset de linhas (com um único campo) é convertido implicitamente em um valor escalar cujo tipo de dados é do campo.  
  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] não oferece suporte a essa coerção implícita. O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornece o operador de ANYELEMENT para extrair um valor singleton de uma coleção, e uma cláusula `select value` para evitar criar um wrapper de linha durante uma expressão de consulta.  
  
## <a name="select-value-avoiding-the-implicit-row-wrapper"></a>Selecione valor: Evitando o Wrapper de linha implícito  
 A cláusula select em uma subconsulta de Transact-SQL cria implicitamente um wrapper de linha ao redor dos itens na cláusula. Isso indica que não podemos criar coleções de escalares ou objetos. Transact-SQL permite uma coerção implícita entre um rowtype com um campo e um valor singleton do mesmo tipo de dados.  
  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornece a cláusula `select value` para ignorar a construção de linha implícita. Somente um item pode ser especificado em uma cláusula `select value`. Quando tal cláusula é usada, nenhum wrapper de linha é construído ao redor dos itens na cláusula `select`, e uma coleção da forma desejada pode ser gerada, por exemplo: `select value a`.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] também fornece o construtor de linha para construir linhas arbitrárias. `select` utiliza um ou mais elementos da projeção e resulta em um registro de dados com campos, como a seguir:  
  
 `select a, b, c`  
  
## <a name="left-correlation-and-aliasing"></a>Correlação à esquerda e aliases  
 No Transact-SQL, expressões em um determinado escopo (como uma única cláusula `select` ou `from`) não podem referenciar expressões definidas anteriormente no mesmo escopo. Alguns dialetos do SQL (incluindo Transact-SQL) dão suporte a formas limitadas no `from` cláusula.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] generaliza as correlações à esquerda no `from` cláusula e trata-as uniformemente. As expressões na cláusula `from` podem referenciar as definições anteriores (definições à esquerda) na mesma cláusula sem a necessidade de sintaxe adicional.  
  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] também impõe restrições adicionais em consultas que envolvem cláusulas `group by`. Expressões na `select` cláusula e `having` só pode se referir a cláusula de tais consultas para o `group by` chaves através de seus aliases. A construção a seguir é válida em Transact-SQL, mas que não está em [!INCLUDE[esql](../../../../../../includes/esql-md.md)]:  
  
```  
select t.x + t.y from T as t group by t.x + t.y  
```  
  
 Para fazer isso em [!INCLUDE[esql](../../../../../../includes/esql-md.md)]:  
  
```  
select k from T as t group by (t.x + t.y) as k  
```  
  
## <a name="referencing-columns-properties-of-tables-collections"></a>Referenciando colunas (propriedades) de tabelas (coleções)  
 Todas as referências a colunas em [!INCLUDE[esql](../../../../../../includes/esql-md.md)] devem ser qualificadas com o alias de tabela. A construção a seguir (supondo que `a` é uma coluna válida da tabela `T`) é válido no Transact-SQL, mas não no [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
```  
select a from T  
```  
  
 A forma em [!INCLUDE[esql](../../../../../../includes/esql-md.md)] é  
  
```  
select t.a as A from T as t  
```  
  
 Os aliases de tabela são opcionais na cláusula `from`. O nome da tabela é usado como o alias implícito. O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] permite também a forma a seguir:  
  
```  
select Tab.a from Tab  
```  
  
## <a name="navigation-through-objects"></a>Navegação por objetos  
 Transact-SQL usa o "." notação para referenciar colunas de (uma linha de) uma tabela. O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] amplia essa notação (emprestada de linguagens de programação) para oferecer suporte à navegação pelas propriedades de um objeto.  
  
 Por exemplo, se `p` for uma expressão do tipo Pessoa, a sintaxe [!INCLUDE[esql](../../../../../../includes/esql-md.md)] a seguir fará referência à cidade do endereço dessa pessoa.  
  
```  
p.Address.City   
```  
  
## <a name="no-support-for-"></a>Nenhum suporte para *  
 Transact-SQL dá suporte a não qualificada * sintaxe como um alias para a linha inteira e o qualificado \* sintaxe (t.\*) como um atalho para os campos dessa tabela. Além disso, o Transact-SQL permite que uma conta especial (\*) agregação, que inclui valores nulos.  
  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] não oferece suporte à construção *. Consultas de Transact-SQL no formato `select * from T` e `select T1.* from T1, T2...` pode ser expresso em [!INCLUDE[esql](../../../../../../includes/esql-md.md)] como `select value t from T as t` e `select value t1 from T1 as t1, T2 as t2...`, respectivamente. Além disso, essas construções manipulam a herança (substituibilidade do valor), embora as variantes `select *` sejam restritas a propriedades de nível superior do tipo declarado.  
  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] não oferece suporte à agregação `count(*)`. Use `count(0)` em seu lugar.  
  
## <a name="changes-to-group-by"></a>Alterações em group by  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] oferece suporte a aliases de chaves `group by`. Expressões na `select` cláusula e `having` cláusula deve se referir ao `group by` as chaves por meio desses aliases. Por exemplo, isso [!INCLUDE[esql](../../../../../../includes/esql-md.md)] sintaxe:  
  
```  
select k1, count(t.a), sum(t.a)  
from T as t  
group by t.b + t.c as k1  
```  
  
 ... é equivalente à seguinte Transact-SQL:  
  
```  
select b + c, count(*), sum(a)   
from T  
group by b + c  
```  
  
## <a name="collection-based-aggregates"></a>Agregações baseadas em coleção  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] oferece suporte a dois tipos de agregações.  
  
 As agregações baseadas em coleção operam em coleções e geram o resultado agregado. Elas podem aparecer em qualquer lugar na consulta, e não requerem uma cláusula `group by`. Por exemplo:  
  
```  
select t.a as a, count({1,2,3}) as b from T as t     
```  
  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] também oferece suporte a agregações do tipo SQL. Por exemplo:  
  
```  
select a, sum(t.b) from T as t group by t.a as a  
```  
  
## <a name="order-by-clause-usage"></a>Uso da cláusula ORDER BY  
 Transact-SQL permite que as cláusulas ORDER BY seja especificada somente no nível mais alto, selecione... DE.. WHERE mais alto. No [!INCLUDE[esql](../../../../../../includes/esql-md.md)], você pode usar uma expressão ORDER BY aninhada e ela pode ser colocada em qualquer lugar na consulta, mas a ordenação em uma consulta aninhada não é preservada.  
  
```  
-- The following query will order the results by the last name  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```  
  
```  
-- In the following query ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## <a name="identifiers"></a>Identificadores  
 No Transact-SQL, comparação de identificador com base no agrupamento de banco de dados atual. Na [!INCLUDE[esql](../../../../../../includes/esql-md.md)], identificadores sempre diferenciam maiusculas de minúsculas e diferencia acento (ou seja, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] faz distinção entre caracteres acentuados e não acentuados; 'por exemplo, a' não é igual a 'ã'). [!INCLUDE[esql](../../../../../../includes/esql-md.md)] trata versões de letras que aparecem o mesmo mas é páginas diferentes de código como caracteres diferentes. Para obter mais informações, consulte [conjunto de caracteres de entrada](../../../../../../docs/framework/data/adonet/ef/language-reference/input-character-set-entity-sql.md).  
  
## <a name="transact-sql-functionality-not-available-in-entity-sql"></a>Funcionalidade Transact-SQL não disponível em Entity SQL  
 A seguinte funcionalidade Transact-SQL não está disponível em [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
 DML  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] no momento não oferece suporte para instruções DML (Inserir, atualizar e excluir).  
  
 DDL  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] não oferece suporte para DDL na versão atual.  
  
 Programação imperativa  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] não oferece suporte para programação imperativa, ao contrário do Transact-SQL. Use, em vez disso, uma linguagem de programação.  
  
 Funções de agrupamento  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] ainda não oferece suporte para funções de agrupamento (por exemplo, CUBE, ROLLUP e GROUPING_SET).  
  
 Funções analíticas  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] (ainda) não oferece suporte para funções analíticas.  
  
 Funções internas, operadores  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] dá suporte a um subconjunto de Transact-SQL funções internas e operadores. Esses operadores e funções provavelmente têm suporte com os principais provedores de repositório. [!INCLUDE[esql](../../../../../../includes/esql-md.md)] usa as funções de store específicas declaradas em um manifesto do provedor. Além disso, o [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] permite que você declare internas e funções definidas pelo usuário existente de repositório para [!INCLUDE[esql](../../../../../../includes/esql-md.md)] usar.  
  
 Dicas  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] não oferece mecanismos para dicas de consulta.  
  
 Processando resultados de consulta em lotes  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] não oferece suporte a resultados de consulta em lotes. Por exemplo, é o seguinte Transact-SQL válida (enviando como um lote):  
  
```  
select * from products;  
select * from catagories;  
```  
  
 No entanto, a sintaxe [!INCLUDE[esql](../../../../../../includes/esql-md.md)] equivalente não tem suporte:  
  
```  
Select value p from Products as p;  
Select value c from Categories as c;  
```  
  
 O [!INCLUDE[esql](../../../../../../includes/esql-md.md)] oferece suporte a apenas uma instrução de consulta que gera resultado por comando.  
  
## <a name="see-also"></a>Consulte também

- [Visão geral do Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)
- [Expressões sem suporte](../../../../../../docs/framework/data/adonet/ef/language-reference/unsupported-expressions-entity-sql.md)
