# Dynamic Finders- Counters

The ORM module supports the concept of dynamic finders and counters for ColdFusion ORM entities. A dynamic finder/counter looks like a real method but it is a virtual method that is intercepted by via `onMissingMethod`. This is a great way for you to do finders and counters using a programmatic and visual representation of what HQL to run.

This feature works on the Base ORM Service, Virtual Entity Services and also Active Entity services. The most semantic and clear representations occur in the Virtual Entity Service and Active Entity as you don't have to pass an entity name around.

