# hashwiki (wip)

An immutable wiki might at first seem counter-intuitive. How does one edit an immutable wiki?

Well, the thing is, traditionally the data for sites running MediaWiki, the most popular of wikis (used to run Wikipedia, you may have heard of it), is already treated as immutable. Although it's kept in a relational database, contributions themselves are never updated once added, they're simply kept in a history. The only thing that is updated is what might be called the 'index', where the latest contribution is shown. The primary issue with this approach, however, is that it expects a community to come to consensus on this source of truth.

Hashwiki is a bit of an experiment where, there doesn't have to be a single index page. They're simply sorted by date of their most recent edit, in order to reward frequent contributors who keep the page up-to-date with the latest contributions.

Contributions take the form of snippets, which can be ordered on a topic by a Table of Contents; the order of which can be sorted by hand. Snippets are tagged with a topic, which places them in the article for that topic, and then ordered within that topic. When an article is updated, a new index is produced.

Snippets and indexes must be verified by the client that they match their hash.

Further, any data should be capable of being easily downloaded and replicated on a different server.

## protocol (or lack thereof)

Anyone can go ahead and make their own hash wiki. in order for the data to be valid between implementations, however, it might be valuable to standardize on an algorithm.

JSON should be avoided. The path to the data is also the key, or path into any document that might need to keep similar things separate. Simply store the value at that path, and any implementation should simply map that key to its value. Any data associated with the value, such as its date, should be hashed.

The key provides context to the content, but the hash makes it so that all data is provably immutable, thus, it cannot be tampered with. all contributions are kept separate.

There should not be organizations backing the hashwiki; if you wish to contribute, instead, simply fork the wiki, create your own web interface into it, host it somewhere, and replicate the data as one sees fit. Any data that is added should also add to a master index: a long, append-only file that can be streamed to find all data on the wiki. If contributions might have merit, one can notify other operators of changes in the fork.

Implementation of a user system is left as an exercise to the operator, however, the consideration of users might not really add a lot to the discussion. If an interface can be designed around allowing for many many different contributors, it makes the system far more robust against wiki spam, sybil attacks, or any desire for consensus.

A voting or ranking system is vulnerable to sybil attack, so no content should be moderated, there's no value in that. Date modified, and number of sections, might be a better indicator of what's desired. If a server deems a piece of content to be particularly egregious, a hash blacklist can be implemented, to not serve that content to users. This is a point of authority, and a necessary one for site owners. These blacklists can be collaborated on and shared.

## TODO

finish wip
