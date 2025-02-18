# Roadmap

This document defines a high level roadmap for Apollo Federation and upcoming
releases. Community and contributor involvement is vital for successfully
implementing all desired items for each release. We hope the items listed below
will inspire further engagement from the community to keep Apollo Federation
progressing and shipping exciting and valuable features.

Any dates listed below and specific issues that will ship in a given milestone
are subject to change but should give a general idea of what we are planning.

We are actively maintaining both the original Federation 1 (on the [version-0.x
branch](https://github.com/apollographql/federation/tree/version-0.x)) and the
new Federation 2 (on the [main branch](https://github.com/apollographql/federation)).

## Table of Contents

* [What's next](#whats-next)
  * [Federation 2 Preview](#federation-2-preview)
  * [Federation 2 GA](#federation-2-ga)
  * [Federation 2 Post-GA](#federation-2-post-ga)
  * [General Federation Enhancements](#general-federation-enhancements)
  * [Under Consideration](#under-consideration)

* [Released](#released)
  * [Federation 2 Alpha](#federation-2-alpha)
  * [Federation 1](#federation-1)
  * [Subgraph Compatibility Test Results](#subgraph-compatibility-test-results)

## What's Next

### Federation 2 Preview

* Expanded use of [core schemas](https://github.com/apollographql/core-schema-js) to compose your own directives in subgraphs.
* Type merging that can be relaxed even further with:
  * `@default` - [#1187](https://github.com/apollographql/federation/issues/1187)
  * `@inaccessible` - [#1178](https://github.com/apollographql/federation/issues/1178) and [core feature spec](https://specs.apollo.dev/)
* New directives that support a stronger source of truth with:
  * `@final` and `@shared` - [#1176](https://github.com/apollographql/federation/issues/1176)
* Field migration across subgraphs with:
  * `@override` - [#1177](https://github.com/apollographql/federation/issues/1177)
* Harmonizing shared value types across subgraphs to steward core common types to a desired state.
* Process subgraph and supergraph schemas with a new [core-schema-js](https://github.com/apollographql/core-schema-js) library.
* Additional composition strategies for user-defined core features
* Updated [join spec](https://specs.apollo.dev/join/v0.1/) with Federation 2 enhancements
* Updated docs
* Enhanced test automation

### Federation 2 GA

* Enhanced backwards compatibility test automation
* Migration guide from Fed 1 to Fed 2 with minimal changes.

### Federation 2 Post-GA

* Importing shared types into subgraph schemas, to keep things more DRY.
* `Entity interfaces` can be spread across multiple subgraphs & interface queries without knowledge of implementing concrete types.
* Nested `@provides` support beyond what Fed 2 alpha already supports natively.
* Advanced caching, auth, demand control, rate limiting, governance, and more!

### General Federation Enhancements

* Improved Gateway performance via AS shape/op-based reporting

### Under Consideration

* Replace `serviceList` API with more flexible, reactive option - [#1180](https://github.com/apollographql/federation/issues/1180)

## Released

### Federation 2 Alpha

* [Announcing Federation 2 - Blog Post](https://www.apollographql.com/blog/announcement/backend/announcing-federation-2/)
* Backwards compatible, requiring no major changes to your subgraphs.
* New v2 Apollo Gateway -- continues to support all existing plugins and customizations.
* New v2 Subgraph package -- separates composition from subgraph enablement code and is backwards compatible so no changes needed.
* Rover CLI and Apollo Workbench releases with Federation 2 composition support.

* Cleaner syntax for a smoother developer experience
  * Build with any natural GraphQL schema
  * First-class support for value type merging of shared interfaces, enums, and other value types.
  * Common tasks like extending a federated type or denormalizing a field for better performance are now possible without special directives and keywords.

* Deliver smaller increments with better shared types
  * Improved shared ownership model with enhanced type merging
  * Flexible `value type merging` is now supported
    * Value types don’t need to be identical across subgraphs.
    * Value type definitions are now merged into a single unified type, much like type merging support for federated types today. Smaller incremental changes, like adding a field, can often be rolled out one subgraph at a time.
  * `Federated entity types` have improved shared ownership
    * Fields can now exist in multiple subgraphs simultaneously.
    * This paves the way for natively supported field migrations with an asynchronous transfer of ownership from one subgraph to another with no downtime or tight release coordination.
* Catch errors sooner with improved static analysis
  * Deeper static analysis, better error messages and a new generalized composition model that helps you catch more errors at build-time instead of at runtime.
  * Clean-sheet implementation of the core composition and query-planning engine that powers the Apollo Gateway
  * The rewritten composition engine now validates all theoretically possible queries and provides more descriptive error messages when a query can’t be satisfied.

* New composition hints help you understand how schema definitions influence query planning and performance. We’ve integrated them into the powerful tools for Apollo Federation:
  * Apollo Workbench shows composition hints in the problems tray with new hover tips.
  * Rover includes composition hints in both standard and structured JSON output so you can integrate them with other tools in your pipeline.
  * Apollo Studio uses composition hints to help you ensure design guidelines and best practices.

* v2 Gateway can run supergraph schemas produced using either Federation 1 composition or the new Federation 2 composition.
  * Supergraph schemas specify the [core features](https://specs.apollo.dev/) they require for `SECURITY` and `EXECUTION`
  * Apollo Gateway observes the required [core feature](https://specs.apollo.dev/) versions (like [join](https://specs.apollo.dev/join/v0.1/)) and uses the appropriate implementation.

* For the latest Federation 2 release info see the `CHANGELOG.md` in each sub-project on the [main branch](https://github.com/apollographql/federation).

* Let us know what you think on the [Community Forum](https://community.apollographql.com/t/announcing-apollo-federation-2/1821)

### Federation 1

* Originally [released in 2019](https://www.apollographql.com/blog/announcement/apollo-federation-f260cf525d21/), Federation powers some of the largest graphs in the world.
* Some notable additions:
  * skip fetches when possible (based on `@skip` and `@include` usages)
  * `@tag` supported on subgraphs and composed into supergraphs - see [https://specs.apollo.dev/](https://specs.apollo.dev/)
  * `@inaccessible` support on supergraphs
* For the latest Federation 1 release info see the `CHANGELOG.md` in each sub-project on the [version-0.x branch](https://github.com/apollographql/federation/tree/version-0.x).

### Subgraph Compatibility Test Results

* [Over 12 languages and GraphQL frameworks](https://www.apollographql.com/docs/federation/other-servers/) support acting as a subgraph in a federated graph.
* Their support is tracked in Apollo's [subgraph compatibility repository](https://github.com/apollographql/apollo-federation-subgraph-compatibility).
* See [Subgraph Library Maintainer Support](https://community.apollographql.com/t/apollo-federation-subgraph-library-maintainer-support/1112) to learn more.
