# Chapter 10: logic

### Knowledge Representation (KR)
- Core problem in developing an intelligent system:
   - how to express knowledge in a computer-tractable form
- KR: a description that incorporates information about a problem, environment, entity
- Primary focus of KR is two fold;
   - how to represent the knowledge one has about a problem domain
   - how to reason using that knowledge in order to answer questions or make decisions
- KR deals with the problem of how to model the world sufficiently for intelligent application

### Proposition logic
- Propositional (boolean) logic - a simple language useful to illustrate basic ideas and Definitions
- user defines a set of propositional symbols, like p1 and p2
- user defines the semantics of these symbols
  - e.g. P1 means "its raining", p2 means "it is hot"

|A | B | A V B | A ^ B | A->B| A<-->B|
|:---:|:---:|:---:|:---:|:---:|:---:|
|T|T|T|T|T|T|
|T|F|T|F|F|F|
|F|T|T|F|T|F|
|F|F|F|F|T|T|

### Summary
- Logical agents apply inference to a knowlege base to derive new information and make decisions
- basic concepts of logic:
   - syntax: formal structure of sentences
   - semantics: truth of sentences wrt models
   - entailment: necessary truth of one sentence given another
   - inference: deriving sentences from other sentences
   - soundness: derivations only produce entailed sentences
   - completeness: derivations can produce all entailed sentences
- Truth table method is sound and compete for PL, but PL lacks expressive power 
