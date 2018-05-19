TAN-chain
Trust Alliance Network : Current Daemon and Node in Development

```

TanChain runtime parameters
  -offline                                 Start daemon in offline mode
  -initprivkey=<privkey>                   Manually set the private key as your default address
  -handshakelocal=<address>                Overwrite locally connected peer wallet addresses
  -miningrequirespeers=<n>                 If set overrides mining-requires-peers blockchain setting, values 0/1.
  -mineemptyrounds=<n>                     If set overrides mine-empty-rounds blockchain setting, values 0.0-1000.0 or -1.
  -miningturnover=<n>                      If set overrides mining-turnover blockchain setting, values 0-1.
  -shrinkdebugfilesize=<n>                 If shrinkdebugfile is 1, this controls the size of the debug file. Whenever the debug.log file reaches over 5 times this number of bytes, it is reduced back down to this size.
  -shortoutput                             Only show the node address (if connecting was successful) or an address in the wallet (if connect permissions must be granted by another node)
  -bantx=<txids>                           Comma delimited list of banned transactions.
  -lockblock=<hash>                        Blocks on branches without this block will be rejected

```  

[![N|Solid](https://safehaven/files/TAN.png)](https://safehaven/files/TAN.png)

### Things being worked on:
  - Legal entities user role
  - API Pipeline and Frontend
  - Reward mechanisms as described in the Whitepaper
  - Daemon in MultiChain (Enterprise level blockchain system)
  - Adding tamperproof ID tracking system in the TAN chain for verified/validated legal entities..
  
  ## Components
  - Web interface built in PHP, HTML, CSS, and Javascript
  - Network connects to Block explorer and Daemon utilizing restful API calls
  - Daemon build with Mulitchain (Will go live once TAN network & MVP Released
