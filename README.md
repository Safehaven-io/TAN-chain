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

[![N|Solid](https://safehaven.io/files/TAN.png)](https://safehaven.io)

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

<p>In the table below, all optional parameters are denoted in <code>(round brackets)</code> with non-empty default values indicated after the <code>=</code> symbol. You should also consult the list of <a href="/developers/api-errors/">error codes and messages</a>.</p>
<h5>General utilities</h5>
<table>
<tr>
<td><strong>Command</strong></td>
<td><strong>Parameters</strong></td>
<td><strong>Description</strong></td>
</tr>
<tr class="api">
<td><code>getblockchainparams</code></td>
<td><code>(display-names=true)<br/>(with-upgrades=true)</code></td>
<td>Returns a list of values of this <a href="/developers/blockchain-parameters/">blockchain&#8217;s parameters</a>. Use <code>display-names</code> to set whether parameters are shown with display names (with hyphens) or canonical names (without hyphens). Use <code>with-upgrades</code> to set whether to show the chain&#8217;s latest parameters (after any upgrades) or its original parameters (in the genesis block). Note that as of MultiChain 1.0.1, only the protocol version can be upgraded.</td>
</tr>
<tr class="api">
<td><code>getruntimeparams</code></td>
<td><code></code></td>
<td>Returns a selection of this node&#8217;s <a href="/developers/runtime-parameters/">runtime parameters</a>, which are set when the node starts up. Some parameters can be modified while MultiChain is running using <code>setruntimeparam</code>.</td>
</tr>
<tr class="api">
<td><code>setruntimeparam</code></td>
<td><code>param value</code></td>
<td>Sets the <a href="/developers/runtime-parameters/">runtime parameter</a> <code>param</code> to <code>value</code> and immediately applies the change. Currently supported parameters: <code style="white-space:normal;">autosubscribe bantx handshakelocal hideknownopdrops lockadminminerounds lockblock maxshowndata mineemptyrounds miningrequirespeers miningturnover</code>.</td>
</tr>
<tr class="api">
<td><code>getinfo</code></td>
<td><code></code></td>
<td>Returns general information about this node and blockchain. MultiChain adds some fields to Bitcoin Core&#8217;s response, giving the blockchain&#8217;s <code>chainname</code>, <code>description</code>, <code>protocol</code>, peer-to-peer <code>port</code>. There are also <code>incomingpaused</code> and <code>miningpaused</code> fields &ndash; see the <code>pause</code> command. The <code>burnaddress</code> is an address with no known private key, to which assets can be sent to make them provably unspendable. The <code>nodeaddress</code> can be passed to other nodes for connecting. The <code>setupblocks</code> field gives the length in blocks of the <a href="/developers/blockchain-parameters/#setup">setup phase</a> in which some consensus constraints are not applied.</td>
</tr>
<tr class="api">
<td><code>help</code></td>
<td><code></code></td>
<td>Returns a list of available API commands, including MultiChain-specific commands.</td>
</tr>
<tr class="api">
<td><code>stop</code></td>
<td><code></code></td>
<td>Shuts down the this blockchain node, i.e. stops the <code>multichaind</code> process.</td>
</tr>
</table>
<h5>Managing wallet addresses</h5>
<table>
<tr class="api">
<td><code>addmultisigaddress</code></td>
<td><code>nrequired ["key", ...]</code></td>
<td>Creates a pay-to-scripthash (P2SH) multisig address and adds it to the wallet. Funds sent to this address can only be spent by transactions signed by <code>nrequired</code> of the specified keys. Each <code>key</code> can be a full public key, or an address if the corresponding key is in the node&#8217;s wallet. (Public keys for a wallet&#8217;s addresses can be obtained using the <code>getaddresses</code> call with <code>verbose=true</code>.) Returns the P2SH address.</td>
</tr>
<tr class="api">
<td><code>getaddresses</code></td>
<td><code>(verbose=false)</code></td>
<td>Returns a list of addresses in this node&#8217;s wallet. Set <code>verbose</code> to <code>true</code> to get more information about each address, formatted like the output of the <code>validateaddress</code> command. For more control see the new <code>listaddresses</code> command.</td>
</tr>
<tr class="api">
<td><code>getnewaddress</code></td>
<td><code></code></td>
<td>Returns a new address whose private key is added to the wallet.</td>
</tr>
<tr class="api">
<td><code>importaddress</code></td>
<td><code>address(es) (label)<br/>(rescan=true)</code></td>
<td>Adds <code>address</code> (or a full public key, or an array of either) to the wallet, without an associated private key. This creates one or more <a href="https://bitcoin.org/en/glossary/watch-only-address">watch-only addresses</a>, whose activity and balance can be retrieved via various APIs (e.g. with the <code>includeWatchOnly</code> parameter), but whose funds cannot be spent by this node. If <code>rescan</code> is <code>true</code>, the entire blockchain is checked for transactions relating to all addresses in the wallet, including the added ones. Returns <code>null</code> if successful.</td>
</tr>
<tr class="api">
<td><code>listaddresses</code></td>
<td><code>(addresses=*) (verbose=false)</br>(count=MAX) (start=-count)</code></td>
<td>Returns information about the addresses in the wallet. Provide one or more addresses (comma-delimited or as an array) to retrieve information about specific addresses only, or use <code>*</code> for all addresses in the wallet. Use <code>count</code> and <code>start</code> to retrieve part of the list only, with negative <code>start</code> values (like the default) indicating the most recently created addresses.</td>
</tr>
</table>
<h5>Working with non-wallet addresses</h5>
<table>
<tr class="api">
<td><code>createkeypairs</code></td>
<td><code>(count=1)</code></td>
<td>Generates one or more public/private key pairs, which are not stored in the wallet or drawn from the node&#8217;s key pool, ready for external key management. For each key pair, the <code>address</code>, <code>pubkey</code> (as embedded in transaction inputs) and <code>privkey</code> (used for signatures) is provided.</td>
</tr>
<tr class="api">
<td><code>createmultisig</code></td>
<td><code>nrequired<br/>["key", ...]</code></td>
<td>Creates a pay-to-scripthash (P2SH) multisig address. Funds sent to this address can only be spent by transactions signed by <code>nrequired</code> of the specified keys. Each <code>key</code> can be a full hexadecimal public key, or an address if the corresponding key is in the node&#8217;s wallet. Returns an object containing the P2SH address and corresponding redeem script.</td>
</tr>
<tr class="api">
<td><code>validateaddress</code></td>
<td><code>address|<br/>privkey|pubkey</code></td>
<td>Returns information about <code>address</code>, or the address corresponding to the specified <code>privkey</code> private key or <code>pubkey</code> public key, including whether this node has the address&#8217;s private key in its wallet.</td>
</tr>
</table>
<h5>Permissions management</h5>
<table>
<tr class="api">
<td><code>grant</code></td>
<td><code>addresses permissions<br/>(native-amount=0)<br/>(start-block) (end-block)<br/>(comment) (comment-to)</code></td>
<td>Grants <code>permissions</code> to <code>addresses</code>, a comma-separated list of addresses. For global permissions, set <code>permissions</code> to one of <code>connect</code>, <code>send</code>, <code>receive</code>, <code>create</code>, <code>issue</code>, <code>mine</code>, <code>activate</code>, <code>admin</code>, or a comma-separated list thereof. For per-asset or per-stream permissions, use the form <code>entity.issue</code> or <code>entity.write,admin</code> where <code>entity</code> is an asset or stream name, ref or creation txid. If the chain uses a native currency, you can send some to each recipient using the <code>native-amount</code> parameter. Returns the txid of the transaction granting the permissions. For more information, see <a href="/developers/permissions-management/">permissions management</a>.</td>
</tr>
<tr class="api">
<td><code>grantfrom</code></td>
<td><code>from-address to-addresses<br/>permissions (native-amount=0)<br/>(start-block) (end-block)<br/>(comment) (comment-to)</code></td>
<td>This works like <code>grant</code>, but with control over the <code>from-address</code> used to grant the permissions. It is useful if the node has multiple addresses with administrator permissions.</td>
</tr>
<tr class="api">
<td><code>grantwithdata</code> <br/><small>or&nbsp;<code>grantwithmetadata</code></small></td>
<td><code>addresses permissions<br/>data-hex|object<br/>(native-amount=0)<br/>(start-block) (end-block)</code></td>
<td>This works like <code>grant</code>, but with an additional data-only transaction output. To include raw data, pass a <code>data-hex</code> hexadecimal string. To publish the data to a stream, pass an object <code>{"for":stream,"key":"...","data":"..."}</code> where <code>stream</code> is a stream name, ref or creation txid, the <code>key</code> is in text form, and the <code>data</code> is hexadecimal.</td>
</tr>
<tr class="api">
<td><code>grantwithdatafrom</code> <br/><small>or&nbsp;<code>grantwithmetadatafrom</code></small></td>
<td><code>from-address to-addresses<br/>permissions data-hex|object<br/>(native-amount=0)<br/>(start-block) (end-block)</code></td>
<td>This works like <code>grantwithdata</code>, but with control over the <code>from-address</code> used to grant the permissions.</td>
</tr>
<tr class="api">
<td><code>listpermissions</code></td>
<td><code>(permissions=*)<br/>(addresses=*)<br/>(verbose=false)</code></td>
<td>Returns a list of all permissions which have been explicitly granted to addresses. To list information about specific global permissions, set <code>permissions</code> to one of <code>connect</code>, <code>send</code>, <code>receive</code>, <code>issue</code>, <code>mine</code>, <code>activate</code>, <code>admin</code>, or a comma-separated list thereof. Omit or pass <code>*</code> or <code>all</code> to list all global permissions. For per-asset or per-stream permissions, use the form <code>entity.issue</code>, <code>entity.write,admin</code> or <code>entity.*</code> where <code>entity</code> is an asset or stream name, ref or creation txid. Provide a comma-delimited list in <code>addresses</code> to list the permissions for particular addresses or <code>*</code> for all addresses. If <code>verbose</code> is <code>true</code>, the <code>admins</code> output field lists the administrator/s who assigned the corresponding permission, and the <code>pending</code> field lists permission changes which are waiting to reach <a href="/developers/permissions-management/#consensus">consensus</a>.</td>
</tr>
<tr class="api">
<td><code>revoke</code></td>
<td><code>addresses permissions<br/>(native-amount=0)<br/>(comment) (comment-to)</code></td>
<td>Revokes <code>permissions</code> from <code>addresses</code>, a comma-separated list of addresses. The <code>permissions</code> parameter works the same as for <code>grant</code>. This is equivalent to calling <code>grant</code> with <code>start-block=0</code> and <code>end-block=0</code>. Returns the txid of transaction revoking the permissions. For more information, see <a href="/developers/permissions-management/">permissions management</a>.</td>
</tr>
<tr class="api">
<td><code>revokefrom</code></td>
<td><code>from-address to-addresses<br/>permissions (native-amount=0)<br/>(comment) (comment-to)</code></td>
<td>This works like <code>revoke</code>, but with control over the <code>from-address</code> used to revoke the permissions. It is useful if the node has multiple addresses with administrator permissions.</td>
</tr>
</table>
<h5>Asset management</h5>
<table>
<tr class="api">
<td><code>issue</code></td>
<td><code>address name|params<br/>qty (units=1)<br/>(native-amount=min-per-output)<br/>({"custom-field-1":"x",...})</code></td>
<td>Creates a new asset on the blockchain, sending the initial <code>qty</code> units to <code>address</code>. To create an asset with the default behavior, use an asset name only for <code>name|params</code>. For more control, use an object such as <code>{"name":"asset1","open":true}</code>. If <code>open</code> is <code>true</code> then additional units can be issued in future by the same key which signed the original issuance, via the <code>issuemore</code> or <code>issuemorefrom</code> command. The smallest transactable unit is given by <code>units</code>, e.g. <code>0.01</code>. If the chain uses a native currency, you can send some with the new asset using the <code>native-amount</code> parameter. Returns the txid of the issuance transaction. For more information, see <a href="/developers/native-assets/">native assets</a>.</td>
</tr>
<tr class="api">
<td><code>issuefrom</code></td>
<td><code>from-address to-address<br/>name|params qty (units=1)<br/>(native-amount=min-per-output)<br/>({"custom-field-1":"x",...})</code></td>
<td>This works like <code>issue</code>, but with control over the <code>from-address</code> used to issue the asset. It is useful if the node has multiple addresses with <code>issue</code> permissions.</td>
</tr>
<tr class="api">
<td><code>issuemore</code></td>
<td><code>address asset qty<br/>(native-amount=min-per-output)<br/>({"custom-field-1":"x",...})</code></td>
<td>Issues <code>qty</code> additional units of <code>asset</code>, sending them to <code>address</code>. The <code>asset</code> can be specified using its name, ref or issuance txid – see <a href="/developers/native-assets/">native assets</a> for more information. If the chain uses a native currency, you can send some with the new asset units using the <code>native-amount</code> parameter. Any custom fields will be attached to the new issuance event, and not affect the original values (use <code>listassets</code> with <code>verbose=true</code> to see both sets). Returns the txid of the issuance transaction.</td>
</tr>
<tr class="api">
<td><code>issuemorefrom</code></td>
<td><code>from-address to-address<br/>asset qty<br/>(native-amount=min-per-output)<br/>({"custom-field-1":"x",...})</code></td>
<td>This works like <code>issuemore</code>, but with control over the <code>from-address</code> used.</td>
</tr>
<tr class="api">
<td><code>listassets</code></td>
<td><code>(assets=*) (verbose=false)</br>(count=MAX) (start=-count)</code></td>
<td>Returns information about assets issued on the blockchain. Pass an asset name, ref or issuance txid in <code>assets</code> to retrieve information about one asset only, an array thereof for multiple assets, or <code>*</code> for all assets. In assets with multiple issuance events, the top-level <code>issuetxid</code> and <code>details</code> fields refer to the first issuance only &ndash; set <code>verbose</code> to <code>true</code> for details about each of the individual issuances. Use <code>count</code> and <code>start</code> to retrieve part of the list only, with negative <code>start</code> values (like the default) indicating the most recently created assets. Extra fields are shown for assets to which this node is subscribed.</td>
</tr>
</table>
<h5>Querying wallet balances and transactions</h5>
<table>
<tr class="api">
<td><code>getaddressbalances</code></td>
<td><code>address (minconf=1)<br/>(includeLocked=false)</code></td>
<td>Returns a list of all the asset balances for <code>address</code> in this node&#8217;s wallet, with at least <code>minconf</code> confirmations. Use <code>includeLocked</code> to include unspent outputs which have been locked, e.g. by a call to <code>preparelockunspent</code>.</td>
</tr>
<p>  <!--<br />
<tr>
<td><code>getassetbalances</code></td>
<td><code>(account=&quot;&quot;) (minconf=1)<br/>(includeWatchOnly=false)<br/>(includeLocked=false)</code></td>
<td>Returns a list of all the asset balances for <code>account</code> in this node's wallet, with at least <code>minconf</code> confirmations. Omit the <code>account</code> parameter or use <code>&quot;&quot;</code> for the default account – see <a href="#accounts">note about accounts</a>. Use <code>includeWatchOnly</code> to include the balance of <a href="https://bitcoin.org/en/glossary/watch-only-address">watch-only addresses</a> and <code>includeLocked</code> to include unspent outputs which have been locked, e.g. by a call to <code>preparelockunspent</code>.</td>
</tr>
<p>--></p>
<tr class="api">
<td><code>getaddresstransaction</code></td>
<td><code>address txid<br/>(verbose=false)</code></td>
<td>Provides information about transaction <code>txid</code> related to <code>address</code> in this node&#8217;s wallet, including how it affected that address&#8217;s balance. Use <code>verbose</code> to provide details of transaction inputs and outputs.</td>
</tr>
<tr class="api">
<td><code>getmultibalances</code></td>
<td><code>(addresses=*)</br>(assets=*)</br>(minconf=1)<br/>(includeWatchOnly=false)<br/>(includeLocked=false)</code></td>
<td>Returns a list of balances of the <code>addresses</code> in this node&#8217;s wallet for the specified <code>assets</code>, with at least <code>minconf</code> confirmations. The <code>addresses</code> are specified as a comma-delimited list or array, or <code>*</code> for all addresses with non-zero balances. The <code>assets</code> are specified as an array of asset names, refs or issuance txids, or <code>*</code> for all assets with non-zero balances. Use <code>includeWatchOnly</code> to include <a href="https://bitcoin.org/en/glossary/watch-only-address">watch-only addresses</a> (only relevant if <code>addresses=*</code>) and <code>includeLocked</code> to include unspent outputs which have been locked, e.g. by a call to <code>preparelockunspent</code>. The response includes a <code>total</code> of the balances shown.</td>
</tr>
<tr class="api">
<td><code>gettotalbalances</code></td>
<td><code>(minconf=1)<br/>(includeWatchOnly=false)<br/>(includeLocked=false)</code></td>
<td>Returns a list of all the asset balances in this node&#8217;s wallet, with at least <code>minconf</code> confirmations. Use <code>includeWatchOnly</code> to include the balance of <a href="https://bitcoin.org/en/glossary/watch-only-address">watch-only addresses</a> and <code>includeLocked</code> to include unspent outputs which have been locked, e.g. by a call to <code>preparelockunspent</code>.</td>
</tr>
<tr class="api">
<td><code>getwallettransaction</code></td>
<td><code>txid<br/>(includeWatchOnly=false)<br/>(verbose=false)</code></td>
<td>Provides information about transaction <code>txid</code> in this node&#8217;s wallet, including how it affected the node&#8217;s total balance. Use <code>includeWatchOnly</code> to consider <a href="https://bitcoin.org/en/glossary/watch-only-address">watch-only addresses</a> as if they belong to this wallet and <code>verbose</code> to provide details of transaction inputs and outputs.</td>
</tr>
<tr class="api">
<td><code>listaddresstransactions</code></td>
<td><code>address<br/>(count=10) (skip=0)<br/>(verbose=false)</code></td>
<td>Lists information about the <code>count</code> most recent transactions related to <code>address</code> in this node&#8217;s wallet, including how they affected that address&#8217;s balance. Use <code>skip</code> to go back further in history and <code>verbose</code> to provide details of transaction inputs and outputs.</td>
</tr>
<tr class="api">
<td><code>listwallettransactions</code></td>
<td><code>(count=10) (skip=0)<br/>(includeWatchOnly=false)<br/>(verbose=false)</code></td>
<td>Lists information about the <code>count</code> most recent transactions in this node&#8217;s wallet, including how they affected the node&#8217;s total balance. Use <code>skip</code> to go back further in history and <code>includeWatchOnly</code> to consider <a href="https://bitcoin.org/en/glossary/watch-only-address">watch-only addresses</a> as if they belong to this wallet. Use <code>verbose</code> to provide the details of transaction inputs and outputs. Note that unlike Bitcoin Core&#8217;s <code>listtransactions</code> command, the response contains one element per transaction, rather than one per transaction output.</td>
</tr>
</table>
<h5>Sending one-way payments</h5>
<table>
<tr class="api">
<td><code>send</code> <br/><small>or&nbsp;<code>sendtoaddress</code></small></td>
<td><code>address amount<br/>(comment)<br/>(comment-to)</code></td>
<td>Sends one or more assets to <code>address</code>, returning the txid. In Bitcoin Core, the <code>amount</code> field is the quantity of the bitcoin currency. For MultiChain, an <code>{"asset":qty, ...}</code> object can be used for <code>amount</code>, in which each <code>asset</code> is an asset name, ref or issuance txid, and each <code>qty</code> is the quantity of that asset to send (see <a href="/developers/native-assets/">native assets</a>). Use <code>&quot;&quot;</code> as the <code>asset</code> inside this object to specify a quantity of the native currency. See also <code>sendasset</code> for sending a single asset and <code>sendfrom</code> to control the address whose funds are used.</td>
</tr>
<tr class="api">
<td><code>sendasset</code> <br/><small>or&nbsp;<code>sendassettoaddress</code></small></td>
<td><code>address asset qty<br/>(native-amount=min-per-output)<br/>(comment) (comment-to)</code></td>
<td>Sends <code>qty</code> of <code>asset</code> to <code>address</code>, returning the txid. The <code>asset</code> can be specified using its name, ref or issuance txid – see <a href="/developers/native-assets/">native assets</a> for more information. See also <code>sendassetfrom</code> to control the address whose funds are used, <code>send</code> for sending multiple assets in one transaction, and <code>sendfrom</code> to combine both of these.</td>
</tr>
<tr class="api">
<td><code>sendassetfrom</code></td>
<td><code>from-address to-address<br/>asset qty<br/>(native-amount=min-per-output)<br/>(comment) (comment-to)</code></td>
<td>This works like <code>sendasset</code>, but with control over the <code>from-address</code> whose funds are used. Any change from the transaction is sent back to <code>from-address</code>. See also <code>sendfrom</code> for sending multiple assets in one transaction.</td>
</tr>
<tr class="api">
<td><code>sendfrom</code> <br/><small>or&nbsp;<code>sendfromaddress</code></small></td>
<td><code>from-address to-address amount<br/>(comment) (comment-to)</code></td>
<td>This works like <code>send</code>, but with control over the <code>from-address</code> whose funds are used. Any change from the transaction is sent back to <code>from-address</code>.</td>
</tr>
<tr class="api">
<td><code>sendwithdata</code> <br/><small>or&nbsp;<code>sendwithmetadata</code></small></td>
<td><code>address amount data-hex|object</code></td>
<td>This works like <code>send</code>, but with an additional data-only transaction output. To include raw data, pass a <code>data-hex</code> hexadecimal string. To publish the data to a stream, pass an object <code>{"for":stream,"key":"...","data":"..."}</code> where <code>stream</code> is a stream name, ref or creation txid, the <code>key</code> is in text form, and the <code>data</code> is hexadecimal.</td>
</tr>
<tr class="api">
<td><code>sendwithdatafrom</code> <br/><small>or&nbsp;<code>sendwithmetadatafrom</code></small></td>
<td><code>from-address to-address<br/>amount data-hex|object</code></td>
<td>This works like <code>sendwithdata</code>, but with control over the <code>from-address</code> whose funds are used. Any change from the transaction is sent back to <code>from-address</code>.</td>
</tr>
</table>
<h5>Atomic exchange transactions</h5>
<table>
<tr class="api">
<td><code>appendrawexchange</code></td>
<td><code>tx-hex txid vout<br/>{"asset":qty, ...}</code></td>
<td>Adds to the raw atomic exchange transaction in <code>tx-hex</code> given by a previous call to <code>createrawexchange</code> or <code>appendrawexchange</code>. This adds an offer to exchange the asset/s in output <code>vout</code> of transaction <code>txid</code> for <code>qty</code> units of <code>asset</code>, where <code>asset</code> is an asset name, ref or issuance txid (use <code>&quot;&quot;</code> as the <code>asset</code> to specify a quantity of the native currency). The <code>txid</code> and <code>vout</code> should generally be taken from <code>preparelockunspent</code> or <code>preparelockunspentfrom</code>. Multiple items can be specified within the fourth parameter to request multiple assets. Returns a raw transaction in the <code>hex</code> field alongside a <code>complete</code> field stating whether the exchange is complete (i.e. balanced) or not. If complete, the transaction can be broadcast to the network using <code>sendrawtransaction</code>. If not, it can be passed to a further counterparty, who can call <code>decoderawexchange</code> and <code>appendrawexchange</code> as appropriate.</td>
</tr>
<tr class="api">
<td><code>completerawexchange</code></td>
<td><code>tx-hex txid vout<br/>{"asset":qty, ...}<br/>(data-hex|object)</code></td>
<td>This works like <code>appendrawexchange</code> but finalizes the exchange, preventing any further additions. (Technically, it adds a <code>SIGHASH_ALL</code> signature.) If the completed exchange is not balanced, an error is returned. Optional metadata can be added to the transaction, signed by this user only. To include raw data, pass a <code>data-hex</code> hexadecimal string. To publish the data to a stream, pass an object <code>{"for":stream,"key":"...","data":"..."}</code> where <code>stream</code> is a stream name, ref or creation txid, the <code>key</code> is in text form, and the <code>data</code> is hexadecimal. Returns a raw transaction in hexadecimal which can be broadcast to the network using <code>sendrawtransaction</code>.</td>
</tr>
<tr class="api">
<td><code>createrawexchange</code></td>
<td><code>txid vout<br/>{"asset":qty, ...}</code></td>
<td>Creates a new atomic exchange transaction which offers to exchange the asset/s in output <code>vout</code> of transaction <code>txid</code> for <code>qty</code> units of <code>asset</code>, where <code>asset</code> is an asset name, ref or issuance txid (use <code>&quot;&quot;</code> as the <code>asset</code> to specify a quantity of the native currency). The <code>txid</code> and <code>vout</code> should generally be taken from the response to <code>preparelockunspent</code> or <code>preparelockunspentfrom</code>. Multiple items can be specified within the third parameter to request multiple assets. Returns a raw partial transaction in hexadecimal which can be passed to the counterparty, who can call <code>decoderawexchange</code> and <code>appendrawexchange</code> as appropriate.</td>
</tr>
<tr class="api">
<td><code>decoderawexchange</code></td>
<td><code>tx-hex<br/>(verbose=false)</code></td>
<td>Decodes the raw exchange transaction in <code>tx-hex</code>, given by a previous call to <code>createrawexchange</code> or <code>appendrawexchange</code>. Returns details on the offer represented by the exchange and its present state. The <code>offer</code> field in the response lists the quantity of native currency and/or assets which are being offered for exchange. The <code>ask</code> field lists the native currency and/or assets which are being asked for. The <code>candisable</code> field specifies whether this wallet can disable the exchange transaction by double-spending against one of its inputs. The <code>cancomplete</code> field specifies whether this wallet has the assets required to complete the exchange. The <code>complete</code> field specifies whether the exchange is already complete (i.e. balanced) and ready for sending. If <code>verbose</code> is <code>true</code> then all of the individual stages in the exchange are listed. Other fields relating to fees are only relevant for blockchains which use a native currency.</td>
</tr>
<tr class="api">
<td><code>disablerawtransaction</code></td>
<td><code>tx-hex</code></td>
<td>Sends a transaction to disable the offer of exchange in <code>tx-hex</code>, returning the txid. This is achieved by spending one of the exchange transaction&#8217;s inputs and sending it back to the wallet. To check whether this can be used on an exchange transaction, check the <code>candisable</code> field of the output of <code>decoderawexchange</code>.</td>
</tr>
<tr class="api">
<td><code>preparelockunspent</code></td>
<td><code>{"asset":qty, ...}<br/>(lock=true)</code></td>
<td>Prepares an unspent transaction output (useful for building atomic exchange transactions) containing <code>qty</code> units of <code>asset</code>, where <code>asset</code> is an asset name, ref or issuance txid (use <code>&quot;&quot;</code> as the <code>asset</code> to specify a quantity of the native currency). Multiple items can be specified within the first parameter to include several assets within the output. The output will be locked against automatic selection for spending unless the optional <code>lock</code> parameter is set to <code>false</code>. Returns the <code>txid</code> and <code>vout</code> of the prepared output.</td>
</tr>
<tr class="api">
<td><code>preparelockunspentfrom</code></td>
<td><code>from-address<br/>{"asset":qty, ...}<br/>(lock=true)</code></td>
<td>This works like <code>preparelockunspent</code>, but with control over the <code>from-address</code> whose funds are used to prepare the unspent transaction output. Any change from the transaction is send back to <code>from-address</code>.</td>
</tr>
</table>
<h5>Stream management</h5>
<table>
<tr class="api">
<td><code>create</code></td>
<td><code>type=stream name open<br/>({"custom-field-1":"x",...})</code></td>
<td>Creates a new stream on the blockchain called <code>name</code>. Pass the value <code>"stream"</code> in the <code>type</code> parameter (the <code>create</code> API can also be used to create upgrades). If <code>open</code> is <code>true</code> then anyone with global <code>send</code> permissions can publish to the stream, otherwise publishers must be explicitly granted per-stream <code>write</code> permissions. Returns the txid of the transaction creating the stream.</td>
</tr>
<tr class="api">
<td><code>createfrom</code></td>
<td><code>from-address<br/>type=stream name open<br/>({"custom-field-1":"x",...})</code></td>
<td>This works like <code>create</code>, but with control over the <code>from-address</code> used to create the stream. It is useful if the node has multiple addresses with <code>create</code> permissions.</td>
</tr>
<tr class="api">
<td><code>liststreams</code></td>
<td><code>(streams=*) (verbose=false)</br>(count=MAX) (start=-count)</code></td>
<td>Returns information about streams created on the blockchain. Pass a stream name, ref or creation txid in <code>streams</code> to retrieve information about one stream only, an array thereof for multiple streams, or <code>*</code> for all streams. Use <code>count</code> and <code>start</code> to retrieve part of the list only, with negative <code>start</code> values (like the default) indicating the most recently created streams. Extra fields are shown for streams to which this node has subscribed.</td>
</tr>
</table>
<h5>Publishing stream items</h5>
<table>
<tr class="api">
<td><code>publish</code></td>
<td><code>stream key data-hex</code></td>
<td>Publishes an item in <code>stream</code>, passed as a stream name, ref or creation txid, with <code>key</code> provided in text form and <code>data-hex</code> in hexadecimal.</td>
</tr>
<tr class="api">
<td><code>publishfrom</code></td>
<td><code>from-address<br/>stream key data-hex</code></td>
<td>This works like <code>publish</code>, but publishes the item from <code>from-address</code>. It is useful if a stream is open or the node has multiple addresses with per-stream <code>write</code> permissions.</td>
</tr>
</table>
<h5>Managing stream and asset subscriptions</h5>
<table>
<tr class="api">
<td><code>subscribe</code></td>
<td><code>asset(s)|stream(s)<br/>(rescan=true)</code></td>
<td>Instructs the node to start tracking one or more <code>asset(s)</code> or <code>stream(s)</code>. These are specified using a name, ref or creation/issuance txid, or for multiple items, an array thereof. If <code>rescan</code> is <code>true</code>, the node will reindex all items from when the assets and/or streams were created, as well as those in other subscribed entities. Returns <code>null</code> if successful. See also the <code>autosubscribe</code> <a href="/developers/runtime-parameters/">runtime parameter</a>.</td>
</tr>
<tr class="api">
<td><code>unsubscribe</code></td>
<td><code>asset(s)|stream(s)</code></td>
<td>Instructs the node to stop tracking one or more <code>asset(s)</code> or <code>stream(s)</code>. Assets or streams are specified using a name, ref or creation/issuance txid, or for multiple items, an array thereof.</td>
</tr>
</table>
<h5>Querying subscribed assets</h5>
<table>
<tr class="api">
<td><code>getassettransaction</code></td>
<td><code>asset txid<br/>(verbose=false)</code></td>
<td>Retrieves a specific transaction  <code>txid</code> involving <code>asset</code>, passed as an asset name, ref or issuance txid, to which the node must be subscribed. Set <code>verbose</code> to <code>true</code> for additional information about the transaction.</td>
</tr>
<tr class="api">
<td><code>listassettransactions</code></td>
<td><code>asset (verbose=false)<br/>(count=10) (start=-count)<br/>(local-ordering=false)</code></td>
<td>Lists transactions involving <code>asset</code>, passed as an asset name, ref or issuance txid, to which the node must be subscribed. Set <code>verbose</code> to <code>true</code> for additional information about each transaction. Use <code>count</code> and <code>start</code> to retrieve part of the list only, with negative <code>start</code> values (like the default) indicating the most recent items. Set <code>local-ordering</code> to <code>true</code> to order transactions by when first seen by this node, rather than their order in the chain.</td>
</tr>
</table>
<h5>Querying subscribed streams</h5>
<table>
<tr class="api">
<td><code>getstreamitem</code></td>
<td><code>stream txid<br/>(verbose=false)</code></td>
<td>Retrieves a specific item with <code>txid</code> from <code>stream</code>, passed as a stream name, ref or creation txid, to which the node must be subscribed. Set <code>verbose</code> to <code>true</code> for additional information about the item&#8217;s transaction. If an item&#8217;s <code>data</code> is larger than the <code>maxshowndata</code> <a href="/developers/runtime-parameters/">runtime parameter</a>, it will be returned as an object whose fields can be used with <code>gettxoutdata</code>.</td>
</tr>
<tr class="api">
<td><code>gettxoutdata</code></td>
<td><code>txid vout<br/>(count-bytes=INT_MAX)<br/>(start-byte=0)</code></td>
<td>Returns the data embedded in output <code>vout</code> of transaction <code>txid</code>, in hexadecimal. This is particularly useful if a stream item&#8217;s data is larger than the <code>maxshowndata</code> <a href="/developers/runtime-parameters/">runtime parameter</a>. Use the <code>count-bytes</code> and <code>start-byte</code> parameters to retrieve part of the data only.</td>
</tr>
<tr class="api">
<td><code>liststreamblockitems</code></td>
<td><code>stream blocks</br>(verbose=false)<br/>(count=MAX) (start=-count)</code></td>
<td>This works like <code>liststreamitems</code>, but listing items within the specified blocks only. One or more <code>blocks</code> can be specified using their heights, hashes or timestamps &ndash; see the <code>listblocks</code> command for more information.</td>
</tr>
<tr class="api">
<td><code>liststreamkeyitems</code></td>
<td><code>stream key (verbose=false)<br/>(count=10) (start=-count)<br/>(local-ordering=false)</code></td>
<td>This works like <code>liststreamitems</code>, but listing items with the given <code>key</code> only.</td>
</tr>
<tr class="api">
<td><code>liststreamkeys</code></td>
<td><code>stream (keys=*)<br/>(verbose=false)<br/>(count=MAX) (start=-count)<br/>(local-ordering=false)</code></td>
<td>Provides information about keys in <code>stream</code>, passed as a stream name, ref or creation txid. Pass a single key in <code>keys</code> to retrieve information about one key only, pass an array for multiple keys, or <code>*</code> for all keys. Set <code>verbose</code> to <code>true</code> to include information about the first and last item with each key shown. See <code>liststreamitems</code> for details of the <code>count</code>, <code>start</code> and <code>local-ordering</code> parameters.</td>
</tr>
<tr class="api">
<td><code>liststreamitems</code></td>
<td><code>stream (verbose=false)<br/>(count=10) (start=-count)<br/>(local-ordering=false)</code></td>
<td>Lists items in <code>stream</code>, passed as a stream name, ref or creation txid. Set <code>verbose</code> to <code>true</code> for additional information about each item&#8217;s transaction. Use <code>count</code> and <code>start</code> to retrieve part of the list only, with negative <code>start</code> values (like the default) indicating the most recent items. Set <code>local-ordering</code> to <code>true</code> to order items by when first seen by this node, rather than their order in the chain. If an item&#8217;s <code>data</code> is larger than the <code>maxshowndata</code> <a href="/developers/runtime-parameters/">runtime parameter</a>, it will be returned as an object whose fields can be used with <code>gettxoutdata</code>.</td>
</tr>
<tr class="api">
<td><code>liststreampublisheritems</code></td>
<td><code>stream address<br/>(verbose=false)<br/>(count=10) (start=-count)<br/>(local-ordering=false)</code></td>
<td>This works like <code>liststreamitems</code>, but listing items published by the given <code>address</code> only.</td>
</tr>
<tr class="api">
<td><code>liststreampublishers</code></td>
<td><code>stream (addresses=*)<br/>(verbose=false)<br/>(count=MAX) (start=-count)<br/>(local-ordering=false)</code></td>
<td>Provides information about publishers who have written to <code>stream</code>, passed as a stream name, ref or creation txid. Pass a single address in <code>addresses</code> to retrieve information about one publisher only, pass an array or comma-delimited list for multiple publishers, or <code>*</code> for all publishers. Set <code>verbose</code> to <code>true</code> to include information about the first and last item by each publisher shown. See <code>liststreamitems</code> for details of the <code>count</code>, <code>start</code> and <code>local-ordering</code> parameters, relevant only if <code>address=*</code>.</td>
</tr>
</table>
<h5>Managing wallet unspent outputs</h5>
<table>
<tr class="api">
<td><code>combineunspent</code></td>
<td><code>(addresses=*) (minconf=1)<br/>(maxcombines=100) (mininputs=2)<br/>(maxinputs=100) (maxtime=15)</code></td>
<td>Sends transactions to combine unspent outputs (UTXOs) belonging to the same address into a single unspent output, returning a list of txids. This can improve wallet performance, especially for miners in a chain with short block times and non-zero block rewards. Set <code>addresses</code> to a comma-separated list of addresses to combine outputs for, or <code>*</code> for all addresses in the wallet. Only combines outputs with at least <code>minconf</code> confirmations, using between <code>mininputs</code> and <code>maxinputs</code> per transaction. A single call to <code>combineunspent</code> can create up to <code>maxcombines</code> transactions over up to <code>maxtime</code> seconds. See also the <code>autocombine</code> <a href="/developers/runtime-parameters/">runtime parameters</a>.</td>
</tr>
<tr class="api">
<td><code>listlockunspent</code></td>
<td><code></code></td>
<td>Returns a list of locked unspent transaction outputs in the wallet. These will not be used when automatically selecting the outputs to spend in a new transaction.</td>
</tr>
<tr class="api">
<td><code>listunspent</code></td>
<td><code>(minconf=1) (maxconf=999999)<br/>(["address", ...])</code></td>
<td>Returns a list of unspent transaction outputs in the wallet, with between <code>minconf</code> and <code>maxconf</code> confirmations. For a MultiChain blockchain, each transaction output includes <code>assets</code> and <code>permissions</code> fields listing any assets or permission changes encoded within that output. If the third parameter is provided, only outputs which pay an <code>address</code> in this array will be included.</td>
</tr>
<tr class="api">
<td><code>lockunspent</code></td>
<td><code>unlock<br/>([{"txid":"id","vout":n},...])</code></td>
<td>If <code>unlock</code> is <code>false</code>, locks the specified transaction outputs in the wallet, so they will not be used for automatic coin selection. If <code>unlock</code> is <code>true</code>, it unlocks the specified outputs, or unlocks all outputs if no second parameter is provided.</td>
</tr>
</table>
<h5>Working with raw transactions</h5>
<table>
<tr class="api">
<td><code>appendrawchange</code></td>
<td><code>tx-hex address<br/>(native-fee)</code></td>
<td>Adds a change output to the raw transaction in <code>tx-hex</code> given by a previous call to <code>createrawtransaction</code>. Any assets or native currency in the transaction inputs which are not claimed in the outputs will be sent to <code>address</code>, minus the <code>native-fee</code> (which is calculated automatically if omitted). The returned raw transaction can be signed and broadcast to the network using <code>signrawtransaction</code> and <code>sendrawtransaction</code>.</td>
</tr>
<tr class="api">
<td><code>appendrawdata</code> <br/><small>or&nbsp;<code>appendrawmetadata</code></small></td>
<td><code>tx-hex data-hex|object</code></td>
<td>Adds a metadata output (using an <code>OP_RETURN</code>) to the raw transaction in <code>tx-hex</code> given by a previous call to <code>createrawtransaction</code>. Raw metadata can be specified in <code>data-hex</code> in hexadecimal form. Alternatively, an <code>object</code> can be passed to represent asset issuance, stream creation or a stream item &ndash; see <a href="/developers/raw-transactions/">raw transactions</a> for more details. The returned raw transaction can be signed and broadcast to the network using <code>signrawtransaction</code> and <code>sendrawtransaction</code>.</td>
</tr>
<tr class="api">
<td><code>appendrawtransaction</code></td>
<td><code>tx-hex<br/>[{"txid":"id","vout":n},...]<br/>({"address":amount,...})</br>(data=[]) (action="")</code></td>
<td>This works like <code>createrawtransaction</code> but adds the given inputs and (regular or metadata) outputs to the raw transaction specified in <code>tx-hex</code>, rather than creating a new transaction. It is particularly useful for accepting an offer of exchange using an address whose private key is held outside the node&#8217;s wallet. Note that if <code>tx-hex</code> contains more outputs than inputs, the new outputs will be inserted at position <code>n</code>, where <code>n</code> is the number of inputs in <code>tx-hex</code>. (This is important to preserve the viability of certain types of transaction signatures.)</td>
</tr>
<tr class="api">
<td><code>createrawtransaction</code></td>
<td><code>[{"txid":"id","vout":n},...]<br/>{"address":amount,...}</br>(data=[]) (action="")</code></td>
<td>Creates a transaction spending the specified inputs, sending to the given addresses. In Bitcoin Core, each <code>amount</code> field is a quantity of the bitcoin currency. For MultiChain, an <code>{"asset":qty, ...}</code> object can be used for <code>amount</code>, in which each <code>asset</code> is an asset name, ref or issuance txid, and each <code>qty</code> is the quantity of that asset to send (see <a href="/developers/native-assets/">native assets</a>). Use <code>&quot;&quot;</code> as the <code>asset</code> inside this object to specify a quantity of the native currency. The optional <code>data</code> array adds one or more metadata outputs to the transaction, where each element is a raw hexadecimal string or object, formatted as passed to <code>appendrawdata</code>. The optional <code>action</code> parameter can be <code>lock</code> (locks the given inputs in the wallet), <code>sign</code> (signs the transaction using wallet keys), <code>lock,sign</code> (does both) or <code>send</code> (signs and sends the transaction). If <code>action</code> is <code>send</code> the txid is returned. If <code>action</code> contains <code>sign</code>, an object with <code>hex</code> and <code>complete</code> fields is returned, as for <code>signrawtransaction</code>. Otherwise, the raw transaction hexadecimal is returned. See <a href="/developers/raw-transactions/">raw transactions</a> for more details on building raw transactions.</td>
</tr>
<tr class="api">
<td><code>createrawsendfrom</code></td>
<td><code>from-address<br/>{"to-address":amount,...}</br>(data=[]) (action="")</code></td>
<td>This works like <code>createrawtransaction</code>, except it automatically selects the transaction inputs from those belonging to <code>from-address</code>, to cover the appropriate amounts. One or more change outputs going back to <code>from-address</code> will also be added to the end of the transaction.</td>
</tr>
<tr class="api">
<td><code>decoderawtransaction</code></td>
<td><code>tx-hex</code></td>
<td>Returns a JSON object describing the serialized transaction in <code>tx-hex</code>. For a MultiChain blockchain, each transaction output includes <code>assets</code> and <code>permissions</code> fields listing any assets or permission changes encoded within that output. There will also be a <code>data</code> field listing the content of any <code>OP_RETURN</code> outputs in the transaction.</td>
</tr>
<tr class="api">
<td><code>sendrawtransaction</code></td>
<td><code>tx-hex</code></td>
<td>Validates the raw transaction in <code>tx-hex</code> and transmits it to the network, returning the txid. The raw transaction can be created using <code>createrawtransaction</code>, (optionally) <code>appendrawdata</code> and <code>signrawtransaction</code>, or else <code>createrawexchange</code> and <code>appendrawexchange</code>.</td>
</tr>
<tr class="api">
<td><code>signrawtransaction</code></td>
<td><code>tx-hex<br/>([{parent-output},...])<br/>(["private-key",...])<br/>(sighashtype=ALL)</code></td>
<td>Signs the raw transaction in <code>tx-hex</code>, often provided by a previous call to <code>createrawtransaction</code> or <code>createrawsendfrom</code>. Returns a raw hexadecimal transaction in the <code>hex</code> field alongside a <code>complete</code> field stating whether it is now completely signed. If complete, the transaction can be broadcast to the network using <code>sendrawtransaction</code>. If not, it can be passed to other parties for additional signing. To create chains of unbroadcast transactions, pass an optional array of <code>{parent-output}</code> objects, each of which takes the form <code>{"txid":txid,"vout":n,"scriptPubKey":hex}</code>. To sign using (only) private keys which are not in the node&#8217;s wallet, pass an array of <code>"private-key"</code> strings, formatted as per the output of <code>dumpprivkey</code>. To sign only part of the transaction, use the <code>sighashtype</code> parameter to control the <a href="https://bitcoin.org/en/developer-guide#signature-hash-types">signature hash type</a>.</td>
</tr>
</table>
<h5>Peer-to-peer connections</h5>
<table>
<tr class="api">
<td><code>addnode</code></td>
<td><code>ip(:port)<br/>command</code></td>
<td>Manually adds or removes a peer-to-peer connection (peers are also discovered and added automatically). The <code>ip</code> can be a hostname, IPv4 address, IPv4-as-IPv6 address or IPv6 address. For the entire <code>ip:port</code> you can also use the part after the <code>@</code> symbol of the other node&#8217;s <code>nodeaddress</code>, as given by the <code>getinfo</code> command. The <code>command</code> parameter should be one of <code>add</code> (to manually queue a node for the next available slot), <code>remove</code> (to remove a node), or <code>onetry</code> (to immediately connect to a node even if a slot is not available).</td>
</tr>
<tr class="api">
<td><code>getaddednodeinfo</code></td>
<td><code>verbose (ip(:port))</code></td>
<td>If <code>verbose=true</code>, returns information about a node which was added using <code>addnode</code>, or all such nodes if <code>ip(:port)</code> is omitted. If <code>verbose=false</code>, returns a list of added nodes only.</td>
</tr>
<tr class="api">
<td><code>getnetworkinfo</code></td>
<td><code></code></td>
<td>Returns information about the network ports to which the node is connected, and its local IP addresses.</td>
</tr>
<tr class="api">
<td><code>getpeerinfo</code></td>
<td><code></code></td>
<td>Returns information about the other nodes to which this node is connected. If this is a MultiChain blockchain, includes <code>handshake</code> and <code>handshakelocal</code> fields showing the remote and local address used during the handshaking for that connection.</td>
</tr>
<tr class="api">
<td><code>ping</code></td>
<td><code></code></td>
<td>Sends a ping message to all connected nodes to measure network latency and backlog. The results are received asynchronously and retrieved from the <code>pingtime</code> field of the response to <code>getpeerinfo</code>.</td>
</tr>
</table>
<h5>Messaging signing and verification</h5>
<table>
<tr class="api">
<td><code>signmessage</code></td>
<td><code>address|privkey<br/>message</code></td>
<td>Returns a base64-encoded digital signature which proves that <code>message</code> was approved by the owner of <code>address</code> (which must belong to this wallet) or any other private key given in <code>privkey</code>. The signature can be verified by any node using the <code>verifymessage</code> command.</td>
</tr>
<tr class="api">
<td><code>verifymessage</code></td>
<td><code>address signature<br/>message</code></td>
<td>Verifies that <code>message</code> was approved by the owner of <code>address</code> by checking the base64-encoded digital <code>signature</code> provided by a previous call to <code>signmessage</code>. The result is <code>true</code> or <code>false</code> unless an error occurred.</td>
</tr>
</table>
<h5>Querying the blockchain</h5>
<table>
<tr class="api">
<td><code>getblock</code></td>
<td><code>hash|height<br/>(verbose=1)</code></td>
<td>Returns information about the block with <code>hash</code> (retrievable from <code>getblockhash</code>) or at the given <code>height</code> in the active chain. Set <code>verbose</code> to <code>0</code> or <code>false</code> for the block in raw hexadecimal form. Set to <code>1</code> or <code>true</code> for a block summary including the <code>miner</code> address and a list of txids. Set to <code>2</code> to <code>3</code> to include more information about each transaction and its raw hexadecimal. Set to <code>4</code> to include a full description of each transaction, formatted like the output of <code>decoderawtransaction</code>.</td>
</tr>
<tr class="api">
<td><code>getblockchaininfo</code></td>
<td><code></code></td>
<td>Returns information about the blockchain, including the <code>bestblockhash</code> of the most recent block on the active chain, which can be compared across nodes to check if they are perfectly synchronized.</td>
</tr>
<tr class="api">
<td><code>getblockhash</code></td>
<td><code>height</code></td>
<td>Returns the hash of the block at the given <code>height</code>. This can be passed to <code>getblock</code> to get information about the block.</td>
</tr>
<tr class="api">
<td><code>getmempoolinfo</code></td>
<td><code></code></td>
<td>Returns information about the memory pool, which contains transactions that the node has seen and validated, but which have not yet been confirmed on the active chain. If the memory pool is growing continuously, this suggests that transactions are being generated faster than the network is able to process them.</td>
</tr>
<tr class="api">
<td><code>getrawmempool</code></td>
<td><code></code></td>
<td>Returns a list of transaction IDs which are in the node&#8217;s memory pool (see <code>getmempoolinfo</code>).</td>
</tr>
<tr class="api">
<td><code>getrawtransaction</code></td>
<td><code>txid (verbose=0)</code></td>
<td>If <code>verbose</code> is <code>1</code>, returns a JSON object describing transaction <code>txid</code>. For a MultiChain blockchain, each transaction output includes <code>assets</code> and <code>permissions</code> fields listing any assets or permission changes encoded within that output. There will also be a <code>data</code> field listing the content of any <code>OP_RETURN</code> outputs in the transaction.</td>
</tr>
<tr class="api">
<td><code>gettxout</code></td>
<td><code>txid vout<br/>(unconfirmed=false)</code></td>
<td>Returns details about an unspent transaction output <code>vout</code> of <code>txid</code>. For a MultiChain blockchain, includes <code>assets</code> and <code>permissions</code> fields listing any assets or permission changes encoded within the output. Set <code>unconfirmed</code> to true to include unconfirmed transaction outputs. </td>
</tr>
<tr class="api">
<td><code>listblocks</code></td>
<td><code>blocks<br/>(verbose=false)</code></td>
<td>Returns information about the blocks specified, on the active chain only. The <code>blocks</code> parameter can contain a comma-delimited list or array of block heights, hashes, height ranges (e.g. <code>100-200</code>) or <code>-n</code> for the most recent <code>n</code> blocks. Alternatively, pass an object <code>{"starttime":...,"endtime":...}</code> for blocks whose timestamps are in the given range.</td>
</tr>
</table>
<h5>Advanced wallet control</h5>
<table>
<tr class="api">
<td><code>backupwallet</code></td>
<td><code>filename</code></td>
<td>Creates a backup of the <code>wallet.dat</code> file in which the node&#8217;s private keys and watch-only addresses are stored. The backup is created in file <code>filename</code>. <strong>Use with caution</strong> &ndash; any node with access to this file can perform any action restricted to this node&#8217;s addresses.</td>
</tr>
<tr class="api">
<td><code>dumpprivkey</code></td>
<td><code>address</code></td>
<td>Returns the private key associated with <code>address</code> in this node&#8217;s wallet. <strong>Use with caution</strong> &ndash; any node with access to this private key can perform any action restricted to the address.</td>
</tr>
<tr class="api">
<td><code>dumpwallet</code></td>
<td><code>filename</code></td>
<td>Dumps the entire set of private keys in the wallet into a human-readable text format in file <code>filename</code>. <strong>Use with caution</strong> &ndash; any node with access to this file can perform any action restricted to this node&#8217;s addresses.</td>
</tr>
<tr class="api">
<td><code>encryptwallet</code></td>
<td><code>passphrase</code></td>
<td>This encrypts the node&#8217;s wallet for the first time, using <code>passphrase</code> as the password for unlocking. Once encryption is complete, the wallet&#8217;s private keys can no longer be retrieved directly from the <code>wallet.dat</code> file on disk, and MultiChain will stop and need to be restarted. <strong>Use with caution</strong> &ndash; once a wallet has been encrypted it cannot be permanently unencrypted, and must be unlocked for signing transactions with the <code>walletpassphrase</code> command. In a permissioned blockchain, MultiChain will also require the wallet to be unlocked before it can connect to other nodes, or sign blocks that it has mined.</td>
</tr>
<tr class="api">
<td><code>getwalletinfo</code></td>
<td><code></code></td>
<td>Returns information about the node&#8217;s wallet, including the number of transactions (<code>txcount</code>) and unspent transaction outputs (<code>utxocount</code>), the pool of pregenerated keys. If the wallet has been encrypted and unlocked, it also shows when it is <code>unlocked_until</code>.</td>
</tr>
<tr class="api">
<td><code>importprivkey</code></td>
<td><code>privkey(s) (label)<br/>(rescan=true)</code></td>
<td>Adds a <code>privkey</code> private key (or an array thereof) to the wallet, together with its associated public address. If <code>rescan</code> is <code>true</code>, the entire blockchain is checked for transactions relating to all addresses in the wallet, including the added ones. Returns <code>null</code> if successful.</td>
</tr>
<tr class="api">
<td><code>importwallet</code></td>
<td><code>filename</code></td>
<td>Imports the entire set of private keys which were previously dumped (using <code>dumpwallet</code>) into file <code>filename</code>. The entire blockchain will be rescanned for transactions relating to the addresses corresponding with these private keys.</td>
</tr>
<tr class="api">
<td><code>walletlock</code></td>
<td><code></code></td>
<td>This immediately relocks the node&#8217;s wallet, independent of the timeout provided by a previous call to <code>walletpassphrase</code>.</td>
</tr>
<tr class="api">
<td><code>walletpassphrase</code></td>
<td><code>passphrase timeout</code></td>
<td>This uses <code>passphrase</code> (as set in earlier calls to <code>encryptwallet</code> or <code>walletpassphrasechange</code>) to unlock the node&#8217;s wallet for signing transactions for the next <code>timeout</code> seconds. In a permissioned blockchain, this will also need to be called before the node can connect to other nodes or sign blocks that it has mined.</td>
</tr>
<tr class="api">
<td><code>walletpassphrasechange</code></td>
<td><code>old-passphrase<br/>new-passphrase</code></td>
<td>This changes the wallet&#8217;s password from <code>old-passphrase</code> to <code>new-passphrase</code>.</td>
</tr>
</table>
<h5>Blockchain upgrading</h5>
<table>
<tr class="api">
<td><code>approvefrom</code></td>
<td><code>from-address<br/>upgrade approve</code></td>
<td>Approves the specified upgrade from admin <code>from-address</code> if <code>approve=true</code>, or removes a previous approval if <code>approve=false</code>. The <code>upgrade</code> can be specified using its name or creation txid. Returns the txid of the approval transaction.</td>
</tr>
<tr class="api">
<td><code>create</code></td>
<td><code>type=upgrade<br/>name open=false<br/>{"protocol-version":100xx}</code></td>
<td>Creates a new (as yet unapproved) upgrade on the blockchain called <code>name</code>. Pass the value <code>"upgrade"</code> in the <code>type</code> parameter (the <code>create</code> API can also be used to create streams) and <code>false</code> for the <code>open</code> parameter. For now, only the protocol version can be upgraded, for example from <code>10008</code> to <code>10009</code>. You can also pass <code>{"protocol-version":100xx,"startblock":yy}</code> to create an upgrade that will only be applied after a certain block height. Note that an address requires both <code>admin</code> and <code>create</code> permissions to create an upgrade. Returns the txid of the transaction creating the upgrade.</td>
</tr>
<tr class="api">
<td><code>createfrom</code></td>
<td><code>from-address type=upgrade<br/>name open=false<br/>{"protocol-version":100xx}</code></td>
<td>This works like <code>create</code>, but with control over the <code>from-address</code> used to create the upgrade. It is useful if the node has multiple addresses with both <code>admin</code> and <code>create</code> permissions.</td>
</tr>
<tr class="api">
<td><code>listupgrades</code></td>
<td><code>(upgrades=*)</code></td>
<td>Returns information about upgrades on the blockchain, whether pending or approved. Pass an upgrade name or creation txid in <code>upgrades</code> to retrieve information about one upgrade only, an array thereof for multiple upgrades, or <code>*</code> for all upgrades. The response includes information on whether each upgrade has been <code>approved</code> by consensus, which <code>admins</code> have approved it so far, how many more admins are <code>required</code> to reach consensus, and the <code>appliedblock</code> where the upgrade became active.</td>
</tr>
</table>
<h5>Advanced node control</h5>
<table>
<tr class="api">
<td><code>clearmempool</code></td>
<td><code></code></td>
<td>Removes all unconfirmed transactions from this node&#8217;s memory pool. This can only be called after <code>pause incoming,mining</code>. Successful if no error is returned.</td>
</tr>
<tr class="api">
<td><code>pause</code></td>
<td><code>tasks</code></td>
<td>Pauses the specified <code>tasks</code>, specified as a comma-delimited list of <code>mining</code> (i.e. generating blocks) and/or <code>incoming</code> (i.e. processing of incoming blocks and transactions). Successful if no error is returned.</td>
</tr>
<tr class="api">
<td><code>resume</code></td>
<td><code>tasks</code></td>
<td>Resumes the specified <code>tasks</code>, specified as in the <code>pause</code> command. Successful if no error is returned.</td>
</tr>
<tr class="api">
<td><code>setlastblock</code></td>
<td><code>hash|height</code></td>
<td>Rewinds this node&#8217;s active chain to <code>height</code> or rewinds/switches to another block with <code>hash</code>. This can only be called after <code>pause incoming,mining</code>. Returns the hash of the last block in the chain after the change.</td>
</tr>
</table>
</div>
<div class="alphabetical" style="display:none;">
<h4>Alphabetical list of API commands &ndash; <a href="#" id="click-by-category">view by category</a></h4>
<p>In the table below, all optional parameters are denoted in <code>(round brackets)</code>.</p>
<table>
<tbody id="alphabetical-apis">
<tr>
<td><strong>Command</strong></td>
<td><strong>Parameters</strong></td>
<td><strong>Description</strong></td>
</tr>
</tbody>
</table>
