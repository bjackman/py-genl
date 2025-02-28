# Python library for Generic Netlink

At [Blu Wireless](https://bluwireless.com/) we needed a tool for doing NL80211
interactions in Python test code. We couldn't find any libraries that
facilitates this in a way that leverages the strengths of Python, so we wrote
something. Most of the original code was specific to Blu Wireless' technology,
but the generic stuff was pulled out to create this library.

Netlink and Generic Netlink themselves aren't very complicated, but the
attribute system can result in reams of boilerplate code. The aim of this
library is to reduce that boilerplate. The key observation is that for
some/most/all genl families, given knowledge about which attributes appear in
which context and what type their payload should have, attribute sets can be
mapped to Python dictionaries. So to use this library you provide a _schema_
expressing that knowledge about attribute semantics in the protocol you're
using, and it gives you an ergonomic way to build and parse messages.

The best way to see what this really means is to take a look at nl80211.py,
where we define an example schema for NL80211 commands, and
examples/nl80211_dump.py, which uses that schema to query NL80211 for
information about a given WiFi adapter.

Works on both Python 2 and 3.

## Known limitations

- It would make sense for this library to help you build and parse multi-part
  Netlink messages, but it doesn't.

- No HTML documentation. There are docstrings in the code, though. The most
  interesting bit is `nlattr.NlAttrSchema`.
