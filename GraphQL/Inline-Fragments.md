The first thing to remember is that [fragments](https://graphql.org/learn/queries/#fragments) are first. They are essentially reusable pieces that you can use from multiple queries in the same call. Something like this:

```graphql
{
  leftComparison: hero(episode: EMPIRE) {
    ...comparisonFields
  }
  rightComparison: hero(episode: JEDI) {
    ...comparisonFields
  }
}

fragment comparisonFields on Character {
  name
  appearsIn
  friends {
    name
  }
}
```

Notice that you can use the same Fragment to request the same fields across multiple queries/operations. 

Fragments fall over though if you imagine the idea of **not** knowing what might be coming to you in the return. They only work when the items share the same fields. [Inline fragments](https://graphql.org/learn/queries/#inline-fragments) allow you to essentially have a catch-all for return data. 

So, let's say it is possible to get two different types of data back, inline fragments allow you to define which field you want back **depending on the return type**. Like this example from the FATMAP API with collections. Since different types of objects can be held in a collection, you need to prepare for all of them:

```graphql
query {
	collection(id: 42004){
		id
		name
		author{
			parseUserId
		}
		items_page{
			items{
				__typename
				... on Adventure {
					id
					name
					type
					adventure_info
				}
				... on LivedAdventure {
					id
					name
					source_app
					completed_at
				}
			}
		}
	}
}
```

And the main thing to target here is the `__typename`. This is your target. So you are saying "depending on the type that I get back, ask for these fields". The accompanying pieces to the type name are the `... on` keywords which indicate to GraphQL what to do when that type comes back or is in the list. 