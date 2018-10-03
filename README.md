# HibernateDoc

## Annotations

### @NamedEntityGraph

What is an entity graph?

Fetch plans for query or find operations. It will define some properties that would eventually be fetched lazily or eagerly.

#### Defining an EntityGraph

     @Entity
     @NamedEntityGraph(name = "my-graph-name", attributeNodes = @NamedAttributeNode("myProperty"))
     public class MyEntity{
        ....
       SomeType myProperty;
        ....
     }


After the entity graph is defined we cand use it in query or find methods to override fetchType semantics. 
