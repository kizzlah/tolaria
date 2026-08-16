---
type: Note
---
# What it is

Portent

Start Here ​
Portent is an open specification for portable knowledge base systems.

It starts from a simple claim: knowledge is best managed as a graph of typed objects and relationships, not as a hierarchy of folders or a complex web of tables.

Portent is intentionally opinionated. It gives you defaults for the core model of a knowledge base so you can start organizing real information without designing a private ontology first.

The goal is not structure for its own sake. The goal is to make captured information retrievable at the moment it becomes useful.

Convention Over Configuration ​
Portent should be useful before it is customized.

It provides sane defaults so people can map their real information with very little setup. These defaults are opinionated because an empty modeling system pushes every user to become a taxonomy designer before they can organize anything.

Customization is welcome, but it should come after the defaults fail in a concrete situation.

The intended experience is close to Rails: start with conventions that are good enough for most cases, then override them when reality gives you a concrete reason.

Model Reality Before Views ​
Many knowledge bases conflate two different jobs:

modeling reality
rendering a useful view of that model
Folders, notebooks, and spaces are often views pretending to be models. They make a piece of information live in one place, then expect that place to answer every future retrieval question.

Portent separates the two. The model is made of typed objects and explicit relationships. Interfaces can then render whatever is useful on top of that model.

If the model is right, views become cheap.

Types, Relationships, And Lifecycle ​
Portent has three core concepts: a type system, graph relationships, and an information lifecycle.

The type system answers what something is. Relationships explain what it is useful for. Lifecycle state decides whether it needs attention, belongs in active work, or should be retained as archived memory.

These concepts are deliberately small. Portent should contain only the ideas that are broadly useful across personal and work knowledge bases.

For Life And Work ​
Portent is designed for knowledge bases that blend personal and professional information without confusing them.

A personal responsibility, like staying healthy, and a work responsibility, like improving product retention, have the same shape: they are long-running outcomes measured by indicators. A personal project and a work project also have the same shape: they are bounded efforts with a definition of done.

The model should be general enough to cover both without splitting your knowledge into incompatible systems.

Capture First, Organize Later ​
Knowledge work has a lifecycle.

You should be able to capture a rough thought, meeting note, task, resource, or draft without deciding its final structure. Organization happens later, when you can answer two questions:

What kind of thing is this?
What will I need it for?
Capture makes information available before it is fully understood. Organization makes it actionable by assigning type and relationships. Archiving keeps the active workspace clean when an object has completed its purpose or is no longer useful in ordinary work.

Portable Means Simple ​
The model should be easy enough to operate by hand and predictable enough for software to validate.

That is why Portent starts with a small vocabulary and plain, reusable relationships. Tools and teams can add more detail when needed, but the base model should remain easy to read, search, export, and reason about.

The more meaning lives in plain metadata, readable content, stable identifiers, and explicit links, the less it depends on any one vendor or interface.
