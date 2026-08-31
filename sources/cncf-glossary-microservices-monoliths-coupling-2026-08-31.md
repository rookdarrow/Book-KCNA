---
source_url: "https://glossary.cncf.io/microservices-architecture/"
fetched_at: "2026-08-31T09:40:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (CC BY 4.0)"
objectives_covered: ["D4.2"]
concepts_covered: ["microservices", "loose-coupling", "monolithic-apps", "cloud-native-characteristics"]
---
# CNCF Cloud Native Glossary — Microservices, Monolithic Apps, Loosely Coupled Architecture

Three related glossary entries, fetched together because §3 teaches them as a
mutually reinforcing set rather than as separate definitions.

## Microservices Architecture (glossary.cncf.io/microservices-architecture/)

Definition, verbatim:

> "A microservices architecture is an architectural approach that breaks
> applications into individual independent (micro)services, with each service
> focused on a specific functionality."

Problem it addresses — verbatim fragment:

> "the entire app would have to be scaled to accommodate the increase — a very
> inefficient use of resources"

[Paraphrase of surrounding text, NOT verbatim: the entry states that the
traditional monolithic approach creates inefficiencies; that monoliths encourage
tight coupling and make it harder to enforce separation of concerns; and that
they require developers to understand the entire codebase before making changes.]

How it helps — verbatim fragments:

> "different teams to work simultaneously on a small part of a bigger application
> without inadvertently negatively impacting the rest of the app"

> "it also creates operational overhead — the things you need to deploy and keep
> track of increase by order of magnitude"

[Paraphrase, NOT verbatim: breaking functionality into separate services enables
independent deployment, updates, and scaling; the entry notes that many
cloud native technologies have emerged to address the operational challenges
inherent in microservices deployments.]

## Monolithic Apps (glossary.cncf.io/monolithic-apps/) — verbatim, complete

A monolithic application contains all functionality in a single deployable
program. This is often the simplest and easiest place to start when making an
application. However, once the application grows in complexity, monoliths can
become hard to maintain. With more developers working on the same codebase, the
likelihood of conflicting changes and the need for interpersonal communication
between developers increases.

**Problem it Addresses**

Devolving an application into microservices increases its operational overhead —
there are more things to test, deploy, and keep running. Early in a product's
lifecycle, it may be advantageous to defer this complexity and build a monolithic
application until the product is determined successful.

**How it Helps**

A well-designed monolith can uphold lean principles by being the simplest way to
get an application up and running. When the business value of the monolithic
application proves successful, it can be decomposed into microservices. Crafting
a microservices-based app before it has proven valuable may be premature spending
of engineering effort. If the application yields no value, that effort becomes
wasted.

## Loosely Coupled Architecture (glossary.cncf.io/loosely-coupled-architecture/) — verbatim, complete

Loosely coupled architecture is an architectural style where the individual
components of an application are built independently from one another (the
opposite paradigm of tightly coupled architectures). Each component, sometimes
referred to as a microservice, is built to perform a specific function in a way
that can be used by any number of other services. This pattern is generally
slower to implement than tightly coupled architecture but has a number of
benefits, particularly as applications scale.

Loosely coupled applications allow teams to develop features, deploy, and scale
independently, which allows organizations to iterate quickly on individual
components. Application development is faster and teams can be structured around
their competency, focusing on their specific application.
