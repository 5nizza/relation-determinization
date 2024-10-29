# Functional synthesis benchmarks

The [release](https://github.com/5nizza/relation-determinization/releases) contains the actual files.

These QBF benchmarks are from the field of reactive synthesis. There, given a behavioural specification, we want to automatically synthesize a system that satisfies the specification. The problem can be reduced to solving safety games. A classical approach to solving safety games is done in three steps: first, we find a winning region (the set of states from which the game can be won); second, we find a _non_-deterministic strategy to always stay in the winning region; and third, we extract one possible deterministic strategy. The strategy determinization can be formulated as a Boolean relation determinization problem, i.e., functional synthesis. The presented benchmarks do exactly that.

Each benchmark encodes a formula of the form:

$$
\forall i,t.\exists o{:}~ W(t) \rightarrow \mathit{SafeTransIntoW}(t,i,o)
$$

where:
- $W(t)$ is a function characterising the winning region of a safety game; it depends only on state variables.
- $\mathit{SafeTransIntoW}(t,i,o)$ is true if and only if the $(i,o)$-transition from $t$ leads into a position in the winning region.

The package contains the following files:
- `file.qcir`: QCIR files in quantifier-prenex form that use only AND/NOT operations.
- `file.ite.qcir`: QCIR files in quantifier-prenex form that use ITE operations.
- `file.solution.aag`: solutions in AIGER format. Every solution also contains a mapping from input and output AIGER variables to QCIR variables from `file.qcir`. For instance, in an AIGER solution file the line `i2 qcir 3` maps the second AIGER input to QCIR variable `3` in the corresponding cleansed QCIR. The solutions were produced by the strategy-determinization procedure of the game solver `sdf`. That solver heavily relies on the described structure of the formula, so producing smaller solutions will be challenging. Most solutions were produced in less than 10 seconds, the rest -- in less than 1 hour.

