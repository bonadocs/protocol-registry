# Bonadocs Protocol Search Database

The protocol search DB repository serves as a public open-source database to power the protocol search feature in Bonadocs,
enabling public contribution without compromising the safety of developers who use the search tool.

## How does it work?

The Protocol Search Database is a GitHub repository indexed according to the rules defined in the Indexing and Search section below.
This enables a publicly visible and verifiable record of protocols and their relevant metadata. The relatively small number of protocols
makes this approach not only feasible but also efficient.

## How to add your protocol


## Indexing and Search


## Why is Search powered by a GitHub Repository?

We want to ensure that the developers can trust the results of the search DB. We manually review each PR to add a protocol to the DB to achieve that.
The search feature is powered by protocol names and it is often impossible to verify that a contract deployed at a given address has any role in a protocol.
This means a fully open model would have significant risks that cannot be ignored. A fully decentralized process would require developing a protocol that
mitigates the risks correctly and efficiently while considering other factors, such as cost.

A manual review process that is open and public and can be verified by any interested parties is the compromise we have decided to make. If the DB grows
sufficiently large to make the current GitHub-powered process inefficient, we would consider building a more decentralized protocol to handle the load.

### Potential Limitations

- __Manual review is slower__. It would take longer to add a protocol to the search tool or update protocol information. If the demand is high, we will
  implement a solution to speed up update times for pre-reviewed protocols. Initial reviews will stay manual for the foreseeable future.
- __Search can be inefficient as the DB grows__. Based on our estimate of fewer than 10000 web3 protocols with active users across EVM chains, the current
  GitHub-based search solution is good enough to handle most users' needs.
