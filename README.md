# 🐍 Simple Vyper ERC 20 Token Template 🐍
🐍 Very Simple ERC-20 Smart Contract Template written in Vyper to create your own Cryptocurrency on the Ethereum Blockchain, with many customizable Options 📝

***I want to remind the Reader that Vyper is still heavily under development, the code could become invalid in further versions, because of security reasons. I will try to keep the code updated with the newest Vyper version.***

## DISCLAIMER: ⚠️⚠️⚠️

**To achieve full Solidity compatibility, we use the low-level num256 datatype in Vyper. This is NOT recommended for contracts where either full Solidity compatibility is not required, or no other compelling usage for using num256 over num exists. Notably, num256 is not overflow protected and may not support all the automatic security features of num as the language evolves. As the code of this token shows, the use of num256 over num also significantly complicates the contract code.** ⚠️

**THIS TOKEN HAS NOT BEEN AUDITED AND IS NOT RECOMMENDED FOR PRODUCTION FUNDS. While the authors have made every effort to ensure the security of the supplied code, funds loss is always a possibility, and both Vyper's compiler and language remain nascent and rapidly evolving.** ⚠️

## 📝 SmartContractCode.vy 🐍 
**⚠️ VYPER IS STILL UNDER DEVELOPMENT, THIS CODE SHOULD NOT BE USED IN PRODUCTION ⚠️**

```

# Solidity-Compatible EIP20/ERC20 Token
# Implements https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20-token-standard.md

# The use of the uint256 datatype as in this token is not
# recommended, as it can pose security risks.

# This token is intended as a proof of concept towards
# language interoperability and not for production use.

# Events issued by the contract
Transfer: event({_from: indexed(address), _to: indexed(address), _value: uint256(wei)})
Approval: event({_owner: indexed(address), _spender: indexed(address), _value: uint256(wei)})

balances: uint256(wei)[address]
allowances: (uint256(wei)[address])[address]
num_issued: uint256(wei)

@public
@payable
def deposit():
    _value: uint256(wei) = msg.value
    _sender: address = msg.sender
    self.balances[_sender] = self.balances[_sender] + _value
    self.num_issued = self.num_issued + _value
    # Fire deposit event as transfer from 0x0
    log.Transfer(0x0000000000000000000000000000000000000000, _sender, _value)

@public
def withdraw(_value : uint256(wei)) -> bool:
    _sender: address = msg.sender
    # Make sure sufficient funds are present, op will not underflow supply
    # implicitly through overflow protection
    self.balances[_sender] = self.balances[_sender] - _value
    self.num_issued = self.num_issued - _value
    send(_sender, _value)
    # Fire withdraw event as transfer to 0x0
    log.Transfer(_sender, 0x0000000000000000000000000000000000000000, _value)
    return True

@public
@constant
def totalSupply() -> uint256(wei):
    return self.num_issued

@public
@constant
def balanceOf(_owner : address) -> uint256(wei):
    return self.balances[_owner]

@public
def transfer(_to : address, _value : uint256(wei)) -> bool:
    _sender: address = msg.sender
    # Make sure sufficient funds are present implicitly through overflow protection
    self.balances[_sender] = self.balances[_sender] - _value
    self.balances[_to] = self.balances[_to] + _value
    # Fire transfer event
    log.Transfer(_sender, _to, _value)
    return True

@public
def transferFrom(_from : address, _to : address, _value : uint256(wei)) -> bool:
    _sender: address = msg.sender
    allowance: uint256(wei) = self.allowances[_from][_sender]
    # Make sure sufficient funds/allowance are present implicitly through overflow protection
    self.balances[_from] = self.balances[_from] - _value
    self.balances[_to] = self.balances[_to] + _value
    self.allowances[_from][_sender] = allowance - _value
    # Fire transfer event
    log.Transfer(_from, _to, _value)
    return True

@public
def approve(_spender : address, _value : uint256(wei)) -> bool:
    _sender: address = msg.sender
    self.allowances[_sender][_spender] = _value
    # Fire approval event
    log.Approval(_sender, _spender, _value)
    return True

@public
@constant
def allowance(_owner : address, _spender : address) -> uint256(wei):
    return self.allowances[_owner][_spender]

```
