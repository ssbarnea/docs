---
description: >-
  GRI is a command line tool I created over a weekend for helping me with code
  reviews across multiple Gerrit Servers.
---

# gri : Gerrit Reduced Interface

## Why not improving GerTTY?

[GerTTY](https://github.com/openstack/gertty) is lovely and improving it would have being my first choice but at this moment I would evaluate it as "unmaintained", or at least not an active project. I would not have a chance of introducing major changes like consolidating reviews from multiple servers.

If you ever used [GerTTY](https://github.com/openstack/gertty) you probably know that it supports multiple servers, but it does this in a way that requires you to start a different instance for each server. There is effectively no way to see all reviews in a single terminal window. This was a deal-breaker for me.

## Minimal configuration

Shortly, at this moment there is no configuration file for [`gri`](https://github.com/pycontribs/gri), as it loads Gerrit servers from `~/gertty.yaml` config, with one caveat credentials are loaded from `~/netrc` file. That was my decision as I found the idea of storing credentials in a single place, different than tool config safer.

### CLI Options

By default `gri` will list only your own reviews. To display incoming ones add `-i` . Debug mode will print `json` received from gerrit.

```text
$ gri --help                                                                                                                                                              [11:33:34]
Usage: gri [OPTIONS]

Options:
  -d, --debug        Debug mode
  -i, --incoming     Incoming reviews (not mine)
  -s, --server TEXT  Query a single server instead of all
  --help             Show this message and exit.
```

The `-s` option is the most recent addition, and allows you to query only one server. If you do `-s0`it will query only the first server from your config. It proved to be quick way to focus on reviews from a single server.

### Sorting order

The sorting order is not configurable yet and is based on a scoring system which values more reviews that are closer to being merged and that penalizes reviews that are unlikely to be ready to merge. So down-votes from users of CI, draft/wip/dnm statuses or merge conflicts do all lower the score value. 

