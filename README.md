# Bonadocs Protocol Search Database

The protocol search DB repository serves as a public open-source database to power the protocol search feature in Bonadocs,
enabling public contribution without compromising the safety of developers who use the search tool.

## How does it work?

The Protocol Search Database is a GitHub repository indexed according to the rules defined in the [Indexing and Search](#indexing-and-search) section below.
This enables a publicly visible and verifiable record of protocols and their relevant metadata. The relatively small number of protocols
makes this approach sufficiently efficient.

## How to add a protocol

To add a protocol to the database, fork this repository and make the following updates:
- At the end of the `/names.txt` file, __APPEND__ the protocol name and slug in the following format: `slug: name`.
- Leave an empty line at the end of the file.
- The slug __MUST__ not have been used by a different protocol and must be reasonably similar to the protocol name.
  For example, you cannot add `uniswap: Compound`. Your PR will be rejected if this is detected.
- The slug __MUST__ include only lowercase letters of the English alphabet `(a-z)`, digits `(0-9)`, and can contain hyphens `(-)` in between one or more
  letters and digits. The slug must match the regex: `^[a-z0-9]+(?:-[a-z0-9]+)*$`. Some (syntactically) valid slugs are `uniswap`, `uniswap-v2`, and `uniswap-v2-pilot`.
  Note that slugs like `0123` would be syntactically valid but remember that the slug must be reasonably similar to the protocol name.
- You __SHOULD__ __APPEND__ the slug to the relevant `/chains/evm[chainId].txt` files for each chain your protocol runs on.
- The slug __MUST__ be included in at least one `/chains/evm[chainId].txt` file, corresponding to a chain the protocol
  runs on.
- You __SHOULD__ __APPEND__ the slug to the relevant `/tags/[tag].txt` files for each tag that applies to your protocol.
- The metadata should be added to the `/data/[slug].json` file.
  The format of the metadata is
  
  ````json
  {
     "name": "user-readable protocol name",
     "slug": "protocol-slug",
     "owners": "comma,separated,github,usernames",
     "tags": "comma,separated,tag,list",
     "chains": "1,56,137",
     "website": "https://url.of.main.website",
     "links": [
        {
           "label": "Link Label",
           "img": "ipfs://cid-of-square-svg-image-with-dimensions",
           "link": "https://link-location"
        },
        {
           "label": "Link Label 2",
           "link": "https://link-location-2"
        }
     ],
     "collection": "ipfs://cid-of-valid-collection-generated-by-bonadocs-editor"
  }
  ````
- Once done, you can submit a PR to commit your changes to the DB.
- Your PR text should include a link to your protocol home page and your Bonadocs collection page.
- Wait for your PR to be reviewed. We will do some due diligence to make sure you are not impersonating a protocol and using
  fake data. If we have any questions or concerns, we will raise them on the PR thread.
- Once your PR is reviewed, it will take some time for your changes to be broadcast because the files are cached on developers' devices. TTL is currently 2 hours.

## Indexing and Search
### Indexing

When you add your protocol, you add the name to the `/names.txt` file and add the slugs to the relevant `/chains/evm[chainId].txt` files and `/tags/[tag].txt` files.
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
