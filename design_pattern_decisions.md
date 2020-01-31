# Design pattern decisions

Our Bible is comprised of smarts contracts, a backend Node.js API and a front-end React.js app.

## Usage of an oracle

The KJV Bible has static verses. They aren't subject to alteration.

Therefore, in order to preserve verses from the KJV Bible, it became apparent that some method was required to supply accurate text for Bible verses. The alterative would be allowing users to set Bible verse text as they please, which would undoubtedly lead to innacurate Bible text.

A solution to the problem of providing accurate KJV Bible verse text was found by utilizing a combination of a backend Node.js API and the [Provable](https://provable.xyz) oracle service. When a user supplies Our Bible's smart conrract with a concatenatedReference (as documented in the contract), Provable is used to fetch accurate Bible verse data from the Our Bible API.

Once Provale retrieves the verse, the verse is sent back to the Our Bible smart contract where it is stored and preserved.

## Node.js API

The Node.js API is used for more than serving as a store for accurate Bible verse text.

In order to improve the user experience, when a verse is added to the smart contract, an event is fired from the contract that is, in turn, read by the API. The API keeps track of which verses have been added to the smart contract, which can be queried easily in the front-end app.

The API is used instead of directly querying the blockchain because data about the percentages of Bible books and chapters that have been added can be easily calculated and store in an off-chain database. 

Once all Bible verses have been added to the smart contract, i.e. 100% of books and chapters have been added, it will be more efficient to query the blockchain directly.

The fact of the matter is that most people couldn't care less about decentralization. Our Bible purposely acts as a mix of centralization and decentralization in order to provide users with a more familiar user experience while still maintaining pure decentralization in terms of its final form -- all verses being added to the blockchain.

## User interaction

The user interaction with Our Bible is pretty straightforward.

The user wants to store a bible verse on the Ethereum blockchain. He vists [ourbible.io](https://ourbible.io), chooses a verse, and uses his integrated browser wallet to preserve that verse on the blockchain.

Users may also skip the front-end app at [ourbible.io](https://ourbible.io) altogether and just sent Ethereum to the contract address. If the amount sent is at least equal to the verse price, a random verse will be selected by utlizing the Provable oracle.

Funds collected via the verse price are used to cover Provable fees, as well as to help cover the cost of running Our Bible.

## Strings library

Because Our Bible's smart contract revolves around the manipulation and storage of string values, and because string manipulation is a nightmare in Solidity, the [solidity-stringutils](https://github.com/Arachnid/solidity-stringutils) library is used.

