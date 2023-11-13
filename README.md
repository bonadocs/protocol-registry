# Bonadocs Protocol Search Database

The protocol search DB repository serves as a public open-source database to power the protocol search feature in Bonadocs,
enabling public contribution without compromising the safety of developers who use the search tool.

## How does it work?

The Protocol Search Database is a GitHub repository indexed according to the rules defined in the [Indexing and Search](#indexing-and-search) section below.
This enables a publicly visible and verifiable record of protocols and their relevant metadata. The relatively small number of protocols
makes this approach not only feasible but also efficient.

## How to add your protocol


## Indexing and Search
### Indexing

When you add your protocol, you add the name to the `/names.txt` file and add the slugs to the relevant `/chain/evm[chainId].txt` files and `/tags/[tag].txt` files.
This is all the indexing that is necessary to enable the discovery of your protocol. Because of the relatively small number of protocols, this indexing
system is good and fast enough to power the search tool for most developers.

### Search
The search algorithm is simple. When a developer supplies a query text `q` optionally with tag `t` and/or chainId `c` on the search interface, the following things happen:
- The `names.txt` file is searched for the text `q`. The names and slugs of the protocols containing `q` are added to a result list.
- If a chainId `c` is supplied in the query, the `/chainId/evm{c}.txt` file is searched for the slugs. Only the slugs from the result list contained in the chain file are retained.
- If a tag `t` is supplied in the query, the `/tags/{t}.txt` file is searched for the slugs. Only the slugs from the result list contained in the tag file are retained.
- The final result list is returned for the query.

To pull the metadata for any protocol, the relevant metadata is downloaded from the `/data/[slug].json` file.

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
