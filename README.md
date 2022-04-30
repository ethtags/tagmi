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
Tags  
-----------------------------------------
| id  | publickey | nametag | num_votes | 
-----------------------------------------

Votes
--------------------------------------------------------------
| id  | tags_id | vote (enum) | voter_session | voter_pubkey |
--------------------------------------------------------------
```  
Should there be a `num_votes` column in the `Tags` table that is incremented/decremented everytime someone votes up/down/removes vote?
Or is it better to just calculate the number of votes separately by querying the total upvotes and downvotes from the `Votes` table when displaying them to the user?


## Open Questions
* Which code should be public, which code should be private?
* What licenses should be used for which pieces of code?
* How to protect against scraping?  
* What Data Privacy Laws do we need to respect?  
* What other laws do we need to respect? PCI?  
* Moving everything on-chain and making all data publicly available -- is this feasible in today's environment? Wait for ZKRollups and cross-chain/layer communication to mature?
* Submitting/Voting with a wallet for potential future airdrop.
