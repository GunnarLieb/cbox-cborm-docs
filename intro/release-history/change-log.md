# What's New With 2.0.0

## Compatibility Updates

* You will need to move the `orm` configuration structure in your `config/ColdBox.cfc` to the `moduleSettings` struct and rename it to `cborm` to standardize it to module settings.

{% code title="config/ColdBox.cfc" %}
```javascript
moduleSettings = {

    cborm = {
        inject = {
            enabled = true,
            includes = "",
            excludes = ""
        }
    }

};
```
{% endcode %}

* `deleteByQuery()` reworked entirely to do native bulk delete queries.  It now also returns the number of records removed
* The `evict()` method was renamed to `evictCollection()` to better satisfy the same contract in hibernate
* The `evictEntity()` method was renamed to `evict()` to better satisfay the same contract in hibernate
* Removed `byExample` on many listing methods

## General Updates

* **Mementifier** is now a dependency for cborm \([www.forgebox.io/view/mementifier](https://www.forgebox.io/view/mementifier)\), which can be used for producing state out of ORM entities for auditing or building JSON Api's.
* **cbStreams** is now a dependency for cborm \([www.forgebox.io/view/cbstreams](https://www.forgebox.io/view/cbstreams)\), all criteria queries and major listing methods support the return of streams instead of array of objects
* Full Null Support
* Performance update on creating active entities as datasource discovery has been reworked
* Updated build process to latest in Ortus template
* Dropped Railo, Lucee 4.5, ACF11 support
* More direct scoping for performance updates
* Optimized EventHandler so it is lighter and quicker when doing orm injections
* Documented all functions with extra examples and notes and hibernate references
* ColdBox 5 and 4 discrete ORM Injection DSLs

## Criteria Queries

* They have been adapted to work with Hibernate 3, 4 and 5
* New fail fast method for `get()` -&gt; `getOrFail()` to throw an entity not found exception
* New alias methods for controlling the result transformations `asStruct(), asStream(), asDistinct()` that will apply result transformers for you instead of doing `.resultTransformer( c.ALIAS_TO_ENTITY_MAP )`, whish is long and boring, or return to you a java stream via cbStreams.
* When calling native restrictions, no more reflection is used to discover the restriction type thus increasing over 70% in performance when creating criteria queries
* You can now negate any criteria restriction by prefixing it with a `not`.  So you can do: `.notEq(), notBetween(), notIsNull(), notIsIn()` and much more.
* The `list()` method has a new `asStream` boolean argument that if true, will return the results as a cbStream. \(\(www.forgebox.io/view/cbStreams\)\)
* New Methods: `idCast()` and `autoCast()` added for quick casting of values
* New method: `queryHint()` so you can add your own vendor specific query hints for optimizers.
* New method: `comment( string )` so you can add arbitrary comments to the generated SQL, great for debugging
* `sqlRestriction()` deprecated in favor of the shorthand notation: `sql()`
* The `sql()` restriction now supports binding positional parameters. You can pass them in an array and we will infer the types: `sql( "id = ? and isActive = ?", [ "123", true ] )`.  Or you can pass in a struct of `{value:"", type:""}` instead:

```javascript
restrictions.sql( "userName = ? and firstName like ?", [
    { value : "joe", type : "string" },
    { value : "%joe%", type : "string" }
] );
```

The available types are the following which match the Hibernate Types

```javascript
this.TYPES = {
    "string"         : "StringType",
    "clob"            : "ClobType",
    "text"            : "TextType",
    "char"            : "ChareacterType",
    "boolean"         : "BooleanType",
    "yesno"         : "YesNoType",
    "truefalse"        : "TrueFalseType",
    "byte"             : "ByteType",
    "short"         : "ShortType",
    "integer"         : "IntegerType",
    "long"             : "LongType",
    "float"            : "FloatType",
    "double"         : "DoubleType",
    "bigInteger"    : "BigIntegerType",
    "bigDecimal"    : "BigDecimalType",
    "timestamp"     : "TimestampType",
    "time"             : "TimeType",
    "date"             : "DateType",
    "calendar"        : "CalendarType",
    "currency"        : "CurrencyType",
    "locale"         : "LocaleType",
    "timezone"        : "TimeZoneType",
    "url"             : "UrlType",
    "class"         : "ClassType",
    "blob"             : "BlobType",
    "binary"         : "BinaryType",
    "uuid"             : "UUIDCharType",
    "serializable"    : "SerializableType"
};
```

* Detached Criteria builder now has a `maxResults( maxResults )` method to limit the results by
* Detached Criteria sql projections now take aliases into account
* SQL Projections and SQL Group By projections now respect aliases

## Base ORM Service

* New Fail fast methods: `getOrFail() proxies to get(), findOrFail() proxies to findIt()` that if not entity is produced will throw a `EntityNotFound` exception
* All listing methods can now return the results as a cbStream by passing the `asStream` boolean argument.
* Removed `criteriaCount(), criteriaQuery()` from BaseService, this was the legacy criteria builder approach, please use `newCriteria()` instead.
* Update `getEntityGivenName` to support ACF2018
* Lazy loading `BeanPopulator` for performance on creations
* Lazy loading `ORMEventHandler` for performance on creations
* Lazy loading `restrictions` for performance on creations
* Base service can now be initialized with a `datasource`, or uses the default one declared
* Added optional `datasource` to many listing methods
* Added consistency on querying options to all major functions to include `ignoreCase, sorting and timeouts`.
* Added ability to `getAll()` to retrieve read only entities using the `readOnly` argument.
* The `getAll()` method has a new `properties` argument that if passed will allow you to retrieve an array of structs according to the passed in properties.
* New method: `idCast( entity, id )` to auto cast your entity `id` value to java type automatically for you, no more javacasting
* New method: `autoCast( entity, propertyName, value )` to auto cast any value for any entity property automatically, no more javacasting.
* New method: `getKeyValue( entity )` which will give you the value of the entity's unique identifier
* New method: `isDirty( entity )` which will let you know if the entity has dirty values or has its values changed since loaded from the db
* New method: `getEntityMetadata( entity )` which will return to you the hibernate's metadata for a specific entity.
* `getPropertyNames()` argument of `entityname` renamed to `entity` to allow not only for a name but an actual entity as well.
* `getTableName()` argument of `entityname` renamed to `entity` to allow not only for a name but an actual entity as well.
* `getKey()` argument of `entityname` renamed to `entity` to allow not only for a name but an actual entity as well.
* ORM Encapsulation of hibernate metadata retrieval via `getEntityMetadata()`
* `deleteByQuery()` reworked entirely to do native bulk delete queries.  It now also returns the number of records removed
* `deleteWhere()` missing flush argument, added datasource as well
* New properties: `wirebox` : a WireBox reference already injected, `logger` : a prepared logger for the class, `datasource` The default datasource or constructed datasource for the class.
* Logging of all activity now available via the `debug` level, even for dynamic methods.
* Refactored all dynamic finders and counters to their own class, which improves not only performance but weight of orm service based entities.
* All dynamic method calls can now return cbStreams as the results
* All dynamic method calls accept a structure as an argument or named as `options` that can have the following keys now:

```javascript
{
    ignoreCase     : boolean (false)
    maxResults     : numeric (0)
    offset         : numeric (0)
    cacheable      : boolean (false)
    cacheName      : string (default)
    timeout        : numeric (0)
    datasource     : string (defaults)
    sortBy         : hql to sort by,
    autoCast       : boolean (true),
    asStream    : boolean (false)
}

results = ormservice.findByLastLoginBetween( "User", "01/01/2008", "11/01/2008", { sortBy="LastName" } );
```

* All dynamic finders/counters values are autocasted, you no longer need to cast the values, we will do this for you. You can turn it off via the `autocast:false` in the options to the calls.

## Virtual Entity Service

Remember this entity extends Base Service, so we get all the features above plus the following:

## Active Entity

Remember this entity extends the Virtual Service, so we get all the features above plus the following:

* Faster creation speeds due to lazy loading of dependencies and better datasource determination.
* `refresh(), merge(), evict()` refactored to encapsulate login in the base orm service and not itself

