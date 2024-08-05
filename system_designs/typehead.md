# System design for type head
Refer https://github.com/toextendmylimits/system_design/blob/main/search_autocomplete.md

# Design talk points
- Trie
- Components: collection service, aggregator, trie builder
- Trie Builder build trie in-meory, save to database, also update result to cache
- Data partition on letters
- How to update Trie? Primary/Secondary

- Client side optimaztion? Cache recent search hisotry, wait until a few characters and 160ms to query server
