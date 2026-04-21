# Seminar for Susanna

## Motivation for studying transformer expressiveness

- AI is super powerfull
- LLM are super cool
- They are based in the paper ATTN is all you need 


## How does a transformer work

- Explain transformers as the two boxes
    - Talk about autoregressive and what does it mean to accept/reject
    - What is CoT
- Start opening the boxes

### Distribution generation
- Tokens to vectors
    - Token embedding
    - Positional encoding
- ATTN + FF
    - Show formulas but say that the only important part is that they are adding to the previous vectors.
    - Mention the idea behind attn?
    - say smt about the relu in the FF because its useful for the proofs
- Output matrix
    - We need to transform the last vector in a probability distribution so the allow any possible numbers there is a correction matrix at the end


### Token selector
- Consume the probabilty distribution and generate the next token



## State of the art
There are a lot of decision to make about how to study this.

Depending on how you do your attn you could have encoder only, encoder-decoders or decoders only

- Turing complete (encoder decoder)
    - https://www.jmlr.org/papers/volume22/20-302/20-302.pdf
    - for the attn they use argmax instead of softmax
    - arbitrary precision

- A logic equivalence (encoder only)
    - https://arxiv.org/pdf/2310.03817
    - 


All these works use CoT for measure of power.
There is no agreement it's the only thing to play with.
For example this work uses the depth of the model:

- A little depth goes a long way 
    - https://arxiv.org/pdf/2503.03961
    - works over Q^n
    - A different construction:
        - no position encoding
	    - s layers, then repeat L times a set of r layers and end with t layers
	- they main thm is that with depth log n you can solve NL
		- they give a construction for transformers solving regular lang
		- they give a construction for transformers solving stConn


## Why do we study CoT?
Adding in the prompt the phrase "let’s think step by step" makes them work better.
Even adding wrong intermediate steps gives better results




## Our arbitrary decisions

- Our rounding system
    - +inf and -inf are replaced by numbers
    - round after every operation
- Takes on non-uniformity
- What does it mean to accept
- Fixed size tape



## Definition of CoT[T(n), d(n)]


## Primitives and normalization
- Flagging
- Linear transformation
    Remove output step
- Repeating a symbol or forcing the end
- Normalization
    - Infinity tricks



## CoT classes are closed by boolean operations
- Proof of not
- Sketch of or
    - Explain how to run two in parallel
    - Comment that using infinity tricks + linear transformations you get the or


## $CoT[0, log(n)] \subseteq CoT[log(n), log(n)] \subseteq AC^0$


## $SIZE(T(n)) \subseteq Cot[T(n), log(n)]$
- In particular $P/poly \subseteq Cot[poly(n), log(n)]$.
- Consistent to empirical observations, CoT gives more power.


Sketch of the proof:
- A language is in size(T(n)) iff {$C_n$} of size $T(n)$ computes it.
- Idea: build a transformer that computes a circuit of T(n) non-input gates in T(n) steps of CoT

- Compute the circuit on the topological order
- Each step of CoT computes one gate
- Most of the power is made by the positional embedding.
- {gate_id, gate_type, id_input1, id_input2}
- That's why is needed log(n) embedding size

Is it worth a picture here?
Toyota's image is weird, idk why they use it.
Even in the presentation it doesn't make sence.







## Real transformers are non-deterministic
- Picture of ChatGPT answering different to the same prompt



## New construction
- Change in image the argmax for sample
- What does it mean to compute a language?

## This definition is good
- Can simulate deterministic
- Close by boolean operations
- Accepts amplification

## Probabilistic versions of previous theorems hold
### Upper bound
$RCoT[0, log(n)] \subseteq RCoT[log(n), log(n)] \subseteq TC^0$

### Lower bound
An extra step of CoT is needed for each random bit of input

## The end