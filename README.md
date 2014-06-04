Cake: An Instanced Approach to Bitcoin Protocol Layers
======================================================

The entity who signed following:

HJz4bx6eZl5y7CoF9ZBNn2GhtYko32L68ysDMnvNDOZm/9ECegPn4BWq+VWITIO3NUuF4rI7I1xbzLtuyOvSGVU=

takinglaughterseriously@gmail.com

June 3, 2014


**Abstract:**

	By considering a Bitcoin transaction output of arbitrary size to represent a specific quantity of tokens, we can implement a protocol layer that has flexibility similar to the Master Protocol, and security similar to colored coins. This unique representation of tokens provides a means by which an abstraction of quantity and quality combined with the inherently validity of Bitcoin transactions grants the trustless exchange of tokens for Bitcoin. The model of this protocol allows an instanced approach to implementation that provides a base level of security and transaction definitions while fostering the creativity and innovation of the community.


	
**Introduction:**

The nature of the Bitcoin protocol and network lend to the incentivization of various projects which are parasitic to the blockchain. Namely these are protocols which store data in the blockchain, and use that data as the input for a state machine which defines quantities and qualities of tokens “in” various bitcoin addresses. The vague implementation of these protocols unfortunately has lead to a financial liability associated with these higher level transactions due to the challenge of transaction validation, and inattention to the importance of protocol specification.

This paper proposes a methodology of crafting transactions which can form a protocol on top of Bitcoin, while taking advantage of Bitcoin’s inherent protection against double-spends, and proof of work. The key advantage, however, is the ability to fork an implementation of the protocol quickly and efficiently while providing the depth of customization previously available only in full base protocol cryptocurrencies. Due diligence is still of critical importance, but this playground can serve to mitigate risk in the pursuit of practicality in Bitcoin protocol layers, and as a means of crowdsourcing functional innovation.



**The transaction model:**

The transaction model is flexible and can be generalized by the following rules of transaction interpretation:

A transaction consumes the tokens represented by the input.
A transaction will send all tokens to the last output, unless otherwise specified by an OP_RETURN output.

If we spend an output that represents a quantity of tokens in a normal Bitcoin transaction, the tokens will typically be returned to the sender at a change address. By carefully crafting transactions, we can guarantee that an invalid transaction on this protocol layer will return all tokens to the sender. This basic mechanism of token transfer allows the protocol to stay in line with Bitcoin best practices by not reusing addresses, and provides a means by which the fungibility of an output is violated only insofar that it represents a quantity of tokens.

The OP_RETURN output specifies how the transaction is to be processed. The encoded data acts as a script which when interpreted using formal definitions can perform a wide variety of functions.



**The case for script:**

A small number of simple functions can quickly be defined and specified to support basic token transactions.

For example, let us say that we expect the payload of a script to be in the following format:

	functionIdentifier parameter01 parameter02

We can then specify that in order to split a token output we need to construct the OP_RETURN as such:

	tokenSplit outputX quantityX

Where *quantityX* tokens is sent to the address associated with the output at index *outputX*, and the remainder is sent to the last output.

The flexibility of script can be powerful, however it’s important to note that as the complexity of a system increases it becomes less trivial to consider all possible cases. The scripting functionality is intended to push the envelope in cryptocurrencies by implementing a protocol that has **potential but no inherent value.** By removing the risk associated the development of protocol layers the goal is to encourage the pursuit of a **model of practicality** in Bitcoin protocol layers, and the crowdsourcing of **functional innovation.**

There are minor requirements in the application of script, however, to maintain the feasibility of the protocol’s transaction model:

Each address that has a quantity of tokens received an output from the transaction that last spent those tokens.

This rule supports the transaction model, and also enables a script to perform complex functions with a small data footprint, by referring to input and output indices instead of full addresses.



**Staged transactions:**

Script can be contained in one or more OP_RETURN outputs across one or more transactions. A script that spans multiple transactions can establish a **staged transaction**, which allows a transaction to be reviewed before submitted, or a proposed transaction to be synchronized with some external event.

A staged transaction must adhere to the following requirements:

- Each transaction has an output equal to the sum of the inputs minus any transaction fees.
- If a transaction is the [n]th out of a total of [m] script transactions, then transaction [n+1] must spend the an output of transaction [n].
- The [m]th transaction spends an output from transaction [m-1], and is called the **terminal transaction.**
- The terminal transaction must fulfill the requirements established by the script.

A staged transaction can be broadcast for only the cost of the miners fee, and contemplated for validity by any relevant parties. The terminal transaction can be broadcast as desired by the sending user, and provided the staged transaction is was not invalidated, the terminal transaction will finalize it.

The core benefit of staged transactions lie in the potential for trustless and secure exchange of Bitcoin with any tokens. This ability is granted when a staged transaction is approved by both the buyer and the seller, and the terminal transaction is signed by both parties. The terminal transaction simultaneously sends the Bitcoin to the seller and finalizes the transfer of tokens to the buyer.



**Instanced implementation:**

By globally defining a sufficiently large ecosystem parameter in the header of OP_RETURN outputs, developers can self serve an instance of the protocol and have a platform on which to innovate, experiment, or even deploy functional implementations. Note that the term instance is used specifically to identify a protocol implementation that is interoperable with other protocol implementations.

The effect of instanced implementation is that a wealth of tokens with different qualities and properties can take advantage of the Bitcoin network and securely interact across protocol implementations and between layers. By encouraging a side by side instance of the protocol the community stands to benefit from the experiences of other developers, as well as to standardize a platform on which innovation can cross project lines.



**The specification:**

One major issue with current protocol implementations on top of Bitcoin is the ambiguity between valid transactions, and their invalid double spends. The inclusion of these invalid transactions in the blockchain poses a threat to the valid transactions simply because *it is possible for software to interpret these transactions differently.* The issue is further exacerbated by vague, incomplete, informal, nondefinitive and overall poor specifications.

The transaction model of this protocol drastically reduces the ambiguity between valid and invalid transactions by reducing possible outcomes of a transaction. We only need to consider the question, “Where did the tokens go?” whereas other protocols require interpretation to answer these questions:

- Were tokens spent?
- How many were spent?
- Who were they sent to?
- Can that address receive tokens?
- Can the sender send tokens?
- If tokens weren’t sent, could it still be a valid transaction?
- How else can a transaction interact with the protocol?
- Under what circumstances does the protocol accept the senders input?
- Etc…

A core difference between the two methodologies is the manner in which actions or events can be organized on the blockchain. The utilization of the transaction model outlined by this protocol allows for the implicit movement of tokens and the explicit organization between untrusted parties via staged transactions. In comparison, alternate protocols only use explicit movement of tokens, and thus must rely on a time or block count and fee specification to enable reasonably “safe” exchange of tokens for Bitcoin.

These unnecessary complications drastically increase the complexity of protocol specification and therefore affect ease of implementation, safety of interpretation, ability to scale, and overall transaction security.

This protocol intends to outline a method by which discrete definitions of script functions can be formalized for objective interpretation by software. These definitions can be referenced by software to determine the validity of an occurrence of that function in a script.

This formalization of definitions along with the transaction model outline a method by which the validity of a protocol transaction can be independently determined with reasonable confidence.



**Revision control:**

In the scenario that a protocol has been deployed for use, the developers may find it infeasible to serve another protocol instance to fix a bug or implement a few feature. 

In this case, the developers can encode the formal definitions of script functions in transactions to store them in the blockchain. By issuing a different definition of a previously defined function, the function definition can be revised to the new definition.

Best practice would be for the developers to stage a transaction which outlines and establishes all specification changes, and indicate the smallest block number at which the terminal transaction can finalize the staged transaction. In this manner it’s possible to hard fork a protocol instantaneously, without risks above and beyond that which is inherent in a protocol specification revision.

This method of revision control further enables the ability to reasonably prove the validity of a transaction at the time that the transaction was broadcast to the network. By programmatically accessing the function definitions stored in the blockchain that are relevant to a transaction, a client can provably define a chain of token ownership from issuance to the current holder.



**Considerations:**

Transaction malleability poses a challenge to the ability to rely on a string of unconfirmed transactions. It should be noted though, that while an attacker may be able to inconvenience the staging of a transaction, or it’s subsequent terminal transaction, there is no risk to either the tokens in those outputs or the actions finalized by the terminal transaction.

Numerous transactions that each require transaction fees can sum to a non negligible value. This protocol is conceptual and can be implemented on testnet or altcoins to minimize this cost.

This protocol could effectively incentivize the traditional developer to monetize a token, rather than the traditional asset issuer. My hope is that if this is the case the developer’s token derives its value from the properties that lend to the value of his specific protocol instance.

The security of a protocol instance is entirely dependent on the definitions outlined by the relevant developers. The existence of **a** model of security does not mean that due diligence is not necessary when dealing with other protocol instances.

Zero confirmation transactions in an instance of this protocol *can* be treated the same way as a 0 confirmation Bitcoin transaction. Stay conscious of the meaning of this.
