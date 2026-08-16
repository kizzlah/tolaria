---
type: Note
---
# relationships

Relationships
Graph relationships explain what an object is useful for.

Portent defines a small default relationship model. Implementations may add more specific relationship names, but they should preserve the distinction between primary and secondary context.

The default relationship model is deliberately small. Most objects need one answer for primary context and several answers for secondary usefulness. belongs\_to and related\_to are the conventions that make this possible without designing a custom relationship vocabulary first.

Relationships connect objects without forcing the knowledge base into a rigid relational schema.

![portent-relationship-shapes.png](https://portent.md/article/portent-relationship-shapes.png)

PORT items tend to express ownership and composition, while ENTP records express relatedness

PORT items tend to express ownership and composition, while ENTP records express relatedness.

Why not a relational schema. Relational systems require explicit relationships between every pair of tables you want to connect. That can be useful for strict consistency, but it creates a large semantic surface: many relationship fields that often mean similar things in different places.

Portent keeps the relationship vocabulary small and cross-type. The same belongs\_to and related\_to fields can be understood across projects, events, notes, people, topics, responsibilities, operations, and tasks.

Why not folders. Folders are good at one thing: exclusive containment.

That makes traversal simple, but it also makes meaning fragile. A meeting note can only sit in one folder, even if it belongs to a project, involves people, covers topics, and produces tasks.

Portent treats folder-like ownership as one relationship among others. belongs\_to captures primary ownership. related\_to captures secondary usefulness.

Why graph relationships. Graph relationships create less semantic surface and more cross-type meaning.

That matters more in an AI-assisted knowledge base. Humans and agents can ask generic questions like:

Which notes have no belongs\_to and no related\_to?
Which events are related to this person?
Which projects belong to this responsibility?
Which topics collect notes across multiple projects?
The model remains flexible, but the relationships stay recognizable everywhere.

Belongs To
belongs\_to is the default primary relationship.

It means the object has a main context or parent. Most objects should have at most one primary parent for a given organizing purpose.

Examples:

a task belongs to a project
an operation belongs to a responsibility
an event belongs to a project
a note belongs to a responsibility when it is part of that responsibility's operating system
has is the default inverse of belongs\_to.

It is usually rendered by tools rather than written manually. If an operation belongs to a responsibility, the responsibility has that operation. If an event belongs to a project, the project has that event.

Tools may render the inverse as contains or children when that language fits the interface better.

Related To
related\_to is the default secondary relationship.

It means there is useful context without ownership or composition. It is appropriate for many-to-many links.

Examples:

a meeting event is related to every attendee
a note is related to multiple topics
a project is related to the responsibility it is meant to improve
a person is related to projects they influence
referred\_by is the default inverse of related\_to.

It helps tools show backlinks without pretending there is ownership. If a note is related to a topic, the topic is referred by that note. If a meeting event is related to a person, the person can show that event as a related reference.

Tools may render this as linked\_from, backlinks, or simply related items.

Specific relationships. Portent does not try to define every possible relationship.

Specific implementations can add relationships such as authored\_by, attended\_by, depends\_on, blocks, documents, mentions, or supersedes when the default names would hide important meaning.

The rule is simple: use defaults until precision removes ambiguity.

Frontmatter example:

---

```
type: Event\
belongs_to: "[[Launch Portent v0.1]]"\
related_to:

* "[[Knowledge graphs]]"

* "[[Alice Example]]"

* "[[Portent vocabulary]]"
```

---
