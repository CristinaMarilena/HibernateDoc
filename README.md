# HibernateDoc

## Annotations

### @NamedEntityGraph

@link https://jeddict.github.io/page.html?l=tutorial/NamedEntityGraph

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

Where @NamedAttributeNode will define the target property/s that should be fetched.

After the entity graph is defined we cand use it in query or find methods to override fetchType semantics. 

The next code will fetch a Movie with all MovieActors and their MovieActorAwards.

**One movie = > all actors => all their awards**

**Movie      MovieActors      MovieActorsAwards
  id         id                    id
  name       actorName             awardName
             movie.id              actor.id**

     @NamedEntityGraph(  
    name = "movieWithActorsAndAwards",
    attributeNodes = {
        @NamedAttributeNode(value = "movieActors", subgraph = "movieActorsGraph")
    },
    subgraphs = {
        @NamedSubgraph(
                name = "movieActorsGraph",
                attributeNodes = {
                    @NamedAttributeNode("movieActorAwards")
                }
        )
    }
)

     
