# RiotWatcher v1.0
RiotWatcher is a thin wrapper on top of the [Riot Games API for League of Legends][1]. All public methods as of the update on 2/4/2014 are supported in full. All game constants are also included in variable declarations.
No request limiting or anything of the sort is included in this package (I'm working on that, but its not exactly a trivial problem).

## To Start...
RiotWatcher uses the Requests Python package. To install:
```
pip install requests
```
You also need to be a have an API from Riot. Get that from [here][1].

## Using it...
All methods return dictionaries representing the json objects described by the official Riot API.
Any error (e.g. 404) that are known to the service are returned as custom objects (error_404, error_500, ...),
for you to deal with however you like. Any other HTTP errors that are not known returns of the API are raised as exceptions as in the Requests API.

Default region of this application is NA, but that can be changed during initialization.
```python
from riotwatcher import RiotWatcher

w = RiotWatcher('<your-api-key>')

me = w.get_summoner(name='pseudonym117')
print(me)

# takes list of summoner ids as argument, supports up to 40 at a time
# (limit enforced on riot's side, no warning from code)
my_mastery_pages = w.get_mastery_pages([me['id', ])[str(me['id'])]
# returns a dictionary, mapping from summoner_id to mastery pages
# unfortunately, this dictionary can only have strings as keys,
# so must convert id from a long to a string
print(my_mastery_pages)

my_ranked_stats = w.get_ranked_stats(me['id'])
print(my_ranked_stats)

my_ranked_stats_last_season = w.get_ranked_stats(me['id'], season=3)
print(my_ranked_stats_last_season)

# all static methods are prefaced with 'static'
# static requests do not count against your request limit
# but at the same time, they don't change often....
static_champ_list = w.static_get_champion_list()
print(static_champ_list)

# import new region code
from riotwatcher import EUROPE_WEST

# request data from EUW
froggen = w.get_summoner(name='froggen', region=EUROPE_WEST)
print(froggen)

# create watcher with EUW as its default region
euw = RiotClient('<your-api-key>', default_region='EUROPE_WEST')

# proper way to send names with spaces is to remove them, still works with spaces though
xpeke = w.get_summoner(name='fnaticxmid')
print(xpeke)
```
I might get around to fully documenting this at some point, but I am working on using it right now for other things, not documenting it.

### Maybe Important
I don't own any part of Riot or League of Legends or any of their stuff. Don't claim to, and neither should you. This != Riot. My views are mine, theirs are theirs. Mine != theirs.
Also if anything is trademarked, I don't own that trademark. Riot probably does.

[1]: https://developer.riotgames.com/