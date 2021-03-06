---
layout: page
title: Configuring a Message Area
---
## Message Conferences
**Message Conferences** and **Areas** allow for grouping of message base topics.

## Conferences
Message Conferences are the top level container for *1:n* Message *Areas* via the `messageConferences` block in `config.hjson`. A common setup may include a local conference and one or more conferences each dedicated to a particular message network such as fsxNet, ArakNet, etc.

Each conference is represented by a entry under `messageConferences`. Each entries top level key is it's *conference tag*.

| Config Item | Required | Description |
|-------------|----------|-------------|
| `name`      | :+1: | Friendly conference name |
| `desc`      | :+1: | Friendly conference description. |
| `sort`      | :-1: | Set to a number to override the default alpha-numeric sort order based on the `name` field. |
| `default`   | :-1: | Specify `true` to make this the default conference (e.g. assigned to new users) |
| `areas`     | :+1: | Container of 1:n areas described below |
| `acs`       | :-1: | A standard [ACS](/docs/configuration/acs.md) block. See **ACS** below. |

### ACS
An optional standard [ACS](/docs/configuration/acs.md) block can be supplied with the following rules:
* `read`: ACS require to read (see) this conference. Defaults to `GM[users]`.

### Example

```hjson
{
  messageConferences: {
    local: { // conference tag
      name: Local
      desc: Local discussion
      sort: 1
      default: true
      acs: {
        read: GM[users] // default
      }
    }
  }
}
```

## Message Areas
Message Areas are topic specific containers for messages that live within a particular conference. The top level key for an area sets it's *area tag*. For example, "General Discussion" may live under a Local conference while an fsxNet conference may contain "BBS Discussion".

| Config Item | Required | Description                                                                     |
|-------------|----------|---------------------------------------------------------------------------------|
| `name`      | :+1:     | Friendly area name. |
| `desc`      | :+1:     | Friendly area description. |
| `sort`      | :-1:     | Set to a number to override the default alpha-numeric sort order based on the `name` field. |
| `default`   | :-1:     | Specify `true` to make this the default area (e.g. assigned to new users) |
| `acs`       | :-1: | A standard [ACS](/docs/configuration/acs.md) block. See **ACS** below. |

### ACS
An optional standard [ACS](/docs/configuration/acs.md) block can be supplied with the following rules:
* `read`: ACS require to read (see) this conference. Defaults to `GM[users]`.

### Example

```hjson
messageConferences: {
  local: {
    // ... see above ...
    areas: {
      enigma_dev: {                     // Area tag - required elsewhere!
        name: ENiGMA 1/2 Development   
        desc: ENiGMA 1/2 discussion!   
        sort: 1                        
        default: true
        acs: {
          read: GM[users] // default
        }
      }
    }
  }
}
```

## Importing
FidoNet style `.na` files as well as legacy `AREAS.BBS` files in common formats can be imported using `oputil.js mb import-areas`. See [The oputil CLI](/docs/admin/oputil.md) for more information and usage.
