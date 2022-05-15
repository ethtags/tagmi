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
GET     /{address}/tags                   Return all nametags and their votes for a given address  
    Request Body  
        {}  

    Response Body  
     [
        {
            "id": 1,
            "nametag": "Address One Nametag One",
            "upvotes": 10,
            "downvotes": 2,
            "owned": false,
        },
        {
            "id": 2,
            "nametag": "Address One Nametag Two",
            "upvotes": 10,
            "downvotes": 2,
            "owned": true,
        }
    ]


POST    /{address}/tags                   Create a new nametag for a given address and auto-upvote it
    Request Body  
    
        {
            "nametag": "Test Address One"
        }

    Response Body  
        {
            "id": 1,
            "nametag": "Test Address One",
            "votes": [
                {
                    "id": 1,
                    "value": true,
                    "owned": true
                },
                ...
            ]
        }


GET     /{address}/tags/{tag_id}/votes    Returns all votes for a given address and nametag
    Request Body
        {}
    
    Response Body
        [
            {
                "id": 1,
                "value": true,
                "owned": false
            },
            {
                "id": 2,
                "value": true,
                "owned": false
            },
            {
                "id": 3,
                "value": true,
                "owned": true
            }
        ]

POST    /{address}/tags/{tag_id}/votes    Upvote/Downvote a given address and nametag
    Request Body
        {
            "value": true
        }

    Response Body
        {
            "id": 2,
            "value": true,
            "owned": true
        }


GET     /{address}/votes/{vote_id}        Returns specific vote
    Request Body
        {}

    Response Body
        {
            "id": 1,
            "value": true,
            "owned": true
        }


UPDATE  /{address}/votes/{vote_id}        Update a vote for a given address and nametag, must have been created by the requestor
    Request Body
        {
            "value": false
        }

    Response Body
        {
            "id": 1,
            "value": false,
            "owned": true
        }


DELETE  /{address}/votes/{vote_id}        Delete a vote for a given address and nametag, must have been created by the requestor
    Request Body
        {}

    Response Body
        {}
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
