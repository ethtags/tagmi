# tagmi

## Purpose
Crowdsource the nametags of EVM-based public addresses.  

## Product Design
### Feature List
#### MVP
* Etherscan.io and its affiliates  
* Chrome/Brave Extension  
* Help make Tagmi better opt-in settings  

#### Roadmap
* Embed Code Snippet  
* Firefox Extension  
* nansen.ai  
* debank.com  
* zapper.fi  
* app.zerion.io  
* Telegram Bot  
* Discord Bot  
* opensea.io  
* looksrare.io  
* Look for stats on most used apps in EVM-based crypto and plug in there  
* Non-EVM based chains, e.g. Bitcoin

### Marketing
* Threads/content on how using tagmi can help you perform in the markets. Tracking whales, VCs, etc.  
* Threads/content on how using tagmi can help you keep organizations honest.  

## Technical Design

### Database
#### Tables
```
Addresses
-------------
| publickey |
-------------

Tags  
---------------------------------------
| id  | addresses_publickey | nametag |
---------------------------------------

Votes
-------------------------------
| id  | tags_id | vote (enum) |
-------------------------------
```  

#### Endpoints
```
GET     /{address}/tags             Returns all nametags for a given address
POST    /{address}/tags             Create a new nametag for a given address

GET     /{address}/votes            Return all votes for all nametags of a given address
GET     /{address}/votes/{tagId}    Returns all votes for a given address and nametag
POST    /{address}/votes/{tagId}    Upvote/Downvote a given address and nametag
DELETE  /{address}/votes/{tagId}    Delete a vote for a given address and nametag
```


## Open Questions
* What are the moral/ethical implications here?
* Which code should be public, which code should be private?
* What licenses should be used for which pieces of code?
* How to protect against scraping?  
* What Data Privacy Laws do we need to respect?  
* What other laws do we need to respect? PCI?  
* Moving everything on-chain and making all data publicly available -- is this feasible in today's environment? Wait for ZKRollups and cross-chain/layer communication to mature?
* Submitting/Voting with a wallet for potential future airdrop.
