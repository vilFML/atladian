How can the NLP model rememebers the information from much earlier in the sentence?

Cognitive example:
"The dog is hungry, so it eats the \_." the word predicted is food. Because the information we need is earlier in the sequence.

Example 2:
"The dog is hungry. It goes to the kitchen and looks around. After a few minutes, it finds the \_"
**How much context should the model remember?**

# Fixed Content Window

For a model that can only see the last 4 words:
The feedforward Neural Network has no mechanism to remember information outside its input window.

It can be increased the word window, but there is a limitation for long sentences.

---

In spanish we read from left to right, and when the words are being read, comes a representation in the brain of every word read, updating the information about what it is being read. The information is added when the words are read.

In RNN, in every state, it gets combined with the previous hidden state to accumulate more information (context).
How much context should the model remember?

# Memory

# Feedforward vs RNN

For a feedforward, at each time step, the model uses **only the current** state input to compute the hidden state.

In RNN: At each time step, the model uses the current state inputs and the previous state.

# Unfold through time

In RNN you can use just one RNN cell and do a recurrence for it
If a sentence has 10 words, there is no need to create 10 weights but a single one gets reused.


# RNNs for NLP Tasks


| Tasks               | RNN Outputs                 |
| ------------------- | --------------------------- |
| Text Classification | For many tokens, one output |
| Sequence Labeling   | For many tokens, many       |
|                     |                             |



## Encoder-Decoder
For the context of machine translation.
1. The model reads all of the sentence (encoding).
2. The model gets the previous as context and provides a translation

# Bidirectional RNN
The standard RNN gets the left context only.
For the model, it can be used the hidden state of the previous token and also **the next token**. 


# Limitations and LSTMs
**RNNs** struggle with long-range dependencies.
In a long sentence, the model can be mislead by the words in between, considering them releavant.

A Long Short-Term Memory (LSTM) is still a RNN but instead of updating its hidden state, it learns about **information flow**. So that it knows which information is relevant.

A LTSM controls what information is kept: adding, updating and deleting it through computational blocks structures called **gates**, where the information flow is: Forget, Store, Update, Output.

