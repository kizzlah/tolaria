---
type: Note
---
# types

Portent
Types ​
The Portent type system defines eight core object types.

The names are intentionally ordinary. A portable knowledge model should not require a private ontology before it becomes useful.

These types are defaults. They are meant to cover the common shape of personal and organizational knowledge with almost no setup. You should be able to look at a piece of information and usually decide whether it is a project, operation, responsibility, task, event, note, topic, or person.

Implementations may add custom types, but Portent-compatible tools should make the default set easy to use first.

The type system answers the question: what is this?

PORT vs ENTP Types ​
The eight types split into two groups:

PORT: actionable types - Project, Operation, Responsibility, Task.
ENTP: non-actionable records - Event, Note, Topic, Person
PORT organizes things to do. ENTP organizes inert information: things that happened, things you know, things you care about, and people or agents involved in the graph.

PORT and ENTP are the two big type groups in Portent

![portent-type-groups.png](https://portent.md/article/portent-type-groups.png)

PORT types describe things to do. They are actionable objects: the work you perform once or repeatedly, in one sitting or across a longer span.

The four actionable types are defined by two questions:

Size: can this be completed in one sitting?
Recurrence: is this one-and-done or recurring?
That gives four useful categories:

Responsibility: recurring work that cannot be completed in one sitting.
Project: one-and-done work that cannot be completed in one sitting.
Operation: recurring work that can be completed in one sitting.
Task: one-and-done work that can be completed in one sitting.
You can organize anything you need to do based on size and recurrence

/Users/kbc/Documents/Tolaria/Portent/port.md

![port-work-matrix.png](attachments/1786896053455-port-work-matrix.png)

You can organize anything you need to do based on size and recurrence.

Project ​
A Project is a bounded effort that produces an output.

Projects usually:

have a beginning and an end
cannot be completed in one sitting
have success criteria
have a timeline or deadline
advance one or more responsibilities
Example: "Launch Portent v0.1 website by the end of the quarter."

Projects are about outputs. They can belong to responsibilities when the project is meant to improve or maintain a long-running outcome.

Operation ​
An Operation is recurring work that can usually be completed in one sitting.

Operations usually belong to a responsibility, but can also support a project.

Example: "Weekly training review" belongs to "Maintain personal health."

Responsibility ​
A Responsibility is a long-running area of accountability.

Responsibilities usually:

do not have a natural end date
describe outcomes rather than outputs
have measurable indicators or KPIs
are maintained or improved over time
Example: "Maintain personal health," measured by resting heart rate, VO2 max, weekly training volume, and sleep consistency.

Responsibilities are about standards and outcomes. They usually do not have a fixed definition of done.

Task ​
A Task is one-off work that can usually be completed in one sitting.

Tasks are part of the Portent worldview, but they do not need to live inside the knowledge base. A team may keep tasks in Todoist, Linear, GitHub Issues, or another dedicated system while still relating them to Portent projects and responsibilities.

Example: "Book a padel court for Tuesday."

ENTP types describe inert knowledge. They are not work items by themselves: they record what happened, what is known, what is interesting, and who is involved.

Event ​
An Event is something that happened and should be retained in long-term memory.

Events can include meetings, conversations, decisions, achievements, incidents, personal moments, or external changes.

Example: "Meeting with Alice about the Portent vocabulary."

Note ​
A Note is a durable knowledge artifact.

It can be a document, resource, reference, tool, decision record, research summary, checklist, or any material that helps advance or understand another object.

Example: "Why folders conflate model and view."

Topic ​
A Topic is an area of interest or conceptual lens.

Topics do not imply performance expectations. They collect knowledge without requiring ownership, completion, or measurable progress.

Example: "Knowledge graphs."

Person ​
A Person is a real-world person or, where useful, an AI agent treated as an actor in the system.

People can be contacts, collaborators, customers, vendors, authors, attendees, decision makers, or stakeholders.

Example: "Ada Lovelace."
