# .forever Subgraph

This Subgraph sources events from the ENS contracts. This includes the ENS registry, the Auction Registrar, and any resolvers that are created and linked to domains. The resolvers are added through dynamic data sources. More information on all of this can be found at [The Graph Documentation](https://thegraph.com/docs/quick-start).

# Example Queries

Here we have example queries, so that you don't have to type them in yourself eachtime in the graphiql playground:

```graphql
{
  domains {
    id
    labelName
    labelhash
    parent {
      id
    }
    subdomains {
      id
    }
    owner {
      id
    }
    resolver {
      id
    }
    ttl
  }
  resolvers {
    id
    address
    domain {
      id
    }
    events {
      id
      node
      ... on AddrChanged {
        a
      }
      ... on NameChanged {
        name
      }
      ... on AbiChanged {
        contentType
      }
      ... on PubkeyChanged {
        x
        y
      }
      ... on TextChanged {
        indexedKey
        key
      }
      ... on ContenthashChanged {
        hash
      }
      ... on InterfaceChanged {
        interfaceID
        implementer
      }
      ... on AuthorisationChanged {
        owner
        target
        isAuthorized
      }
    }
  }
}

```


# Development

After deploying the contracts, clone this repo inside the forever-contracts directory (the ens-subgraph references .forever contract ABIs from `../build/contracts` and addresses.json from `../addresses.json`)

Edit `addresses.json` and add the start block to index from for example: `startBlock: 12774296,` next to the network.


### Generate deployment code

```bash
yarn
yarn prepare
```

you should see `subgraph.yaml` generated with correct addresses. Run codegen

```bash
yarn codegen
```

### Deploy

locally 

```bash
yarn create-local
yarn deploy-local
```

deploy to the graph:
```
yarn build
yarn deploy
```
