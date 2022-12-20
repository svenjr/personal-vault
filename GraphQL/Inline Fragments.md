The first thing to remember is that fragments are frist. They are essentially reusable pieces that you can use from multiple queries in the same call. Something like this:

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

Notice that you can use the same Fragement to request the same fields across multiple queries/operations. 