# Simple-Vyper-ERC-20-Token-Template
🐍 Very Simple ERC-20 Smart Contract Template written in Vyper to create your own Cryptocurrency on the Ethereum Blockchain, with many customizable Options 📝

***I want to remind the Reader that Vyper is still heavily under development, the code could become invalid in further versions, because of security reasons. I will try to keep the code updated with the newest Vyper version.***

## DISCLAIMER: ⚠️⚠️⚠️

**To achieve full Solidity compatibility, we use the low-level num256 datatype in Vyper. This is NOT recommended for contracts where either full Solidity compatibility is not required, or no other compelling usage for using num256 over num exists. Notably, num256 is not overflow protected and may not support all the automatic security features of num as the language evolves. As the code of this token shows, the use of num256 over num also significantly complicates the contract code.** ⚠️

**THIS TOKEN HAS NOT BEEN AUDITED AND IS NOT RECOMMENDED FOR PRODUCTION FUNDS. While the authors have made every effort to ensure the security of the supplied code, funds loss is always a possibility, and both Vyper's compiler and language remain nascent and rapidly evolving.** ⚠️
