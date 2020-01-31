# Avoiding common attacks

Our Bible's smart contract seeks to avoid and mitigate common attacks.

## Denial of Service by Block Gas Limit or startGas (SWC-128)

If the length of KJV Bible verse texts were unkown, the contract could be open to DoS attachs due to a block's gas limit.

The Provable oracle service has a gas price of 20 GWei. By setting the provableGasLimit in the contract to 500,000, the maximum amount of gas that can be used by a Provable query is 1,000,000, which is well below a block's maximim gas limit of 10,000,000 as of this writing.

Similarly, the longest verse text in the KJV Bible is Esther 8:9. The text returned from the Provable query uses about 900,000 gas to store the text in the smart contract. Therefore, the longest Bible verse can be stored in the contract without breaking the 1,000,000 gas limit set in provableGasLimit.

The smart contract is not open to DoS attacks by block gas limit because Bible verse text lengths are known and finite.
