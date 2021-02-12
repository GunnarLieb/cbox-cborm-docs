# Detached Criteria Builder

Hibernate also supports the concept of detached criterias.  They are most useful for join conditions, subselects, and to query outside the current session.

> Some applications need to create criteria queries in "detached mode", where the Hibernate session is not available. Then you can execute the search in an arbitrary session.

To create an instance of Detached Criteria Builder, simply call the _createSubcriteria\(\)_ method on your existing criteria.

If you use ORM in your ColdBox apps, you are hopefully already taking full advantage of [Criteria Builder](../coldbox-criteria-builder/), ColdBox’s powerful, programmatic DSL builder for Hibernate Criteria queries \(and if you’re not using it, you should!\). With the new Detached Criteria Builder, you can expand the power and flexibility of your criteria queries with support for criteria and projection subqueries, all while using the same intuitive patterns of Criteria Builder. No fuss, just more flexibility and control for your criteria queries!

> "Some applications need to create criteria queries in "detached mode", where the Hibernate session is not available. It also allows you to express subqueries." Hibernate Docs

For more information about Detached Criteria and Subqueries, check out the following Hibernate documentation:

1. Hibernate Docs: [http://docs.jboss.org/hibernate/orm/3.5/reference/en/html/querycriteria.html\#querycriteria-detachedqueries](http://docs.jboss.org/hibernate/orm/3.5/reference/en/html/querycriteria.html#querycriteria-detachedqueries)
2. Hibernate DetachedCriteria: [http://docs.jboss.org/hibernate/orm/3.5/api/org/hibernate/criterion/DetachedCriteria.html](http://docs.jboss.org/hibernate/orm/3.5/api/org/hibernate/criterion/DetachedCriteria.html)
3. Hibernate Subqueries: [http://docs.jboss.org/hibernate/orm/3.5/api/org/hibernate/criterion/Subqueries.html](http://docs.jboss.org/hibernate/orm/3.5/api/org/hibernate/criterion/Subqueries.html)

> **INFO** The best place to see all of the functionality of the Detached Criteria Builder is to check out the latest [API Docs](./).

