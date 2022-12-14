Summary
 - [unchecked-transfer](#unchecked-transfer) (2 results) (High)
 - [events-maths](#events-maths) (2 results) (Low)
 - [missing-zero-check](#missing-zero-check) (3 results) (Low)
 - [reentrancy-benign](#reentrancy-benign) (1 results) (Low)
 - [reentrancy-events](#reentrancy-events) (1 results) (Low)
 - [timestamp](#timestamp) (1 results) (Low)
 - [assembly](#assembly) (1 results) (Informational)
 - [pragma](#pragma) (1 results) (Informational)
 - [solc-version](#solc-version) (6 results) (Informational)
 - [naming-convention](#naming-convention) (8 results) (Informational)
 - [constable-states](#constable-states) (2 results) (Optimization)
## unchecked-transfer
Impact: High
Confidence: Medium
 - [ ] ID-0
[StakeVRT.withdrawToken(address)](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L116-L121) ignores return value by [IERC20(token).transfer(msg.sender,IERC20(token).balanceOf(address(this)))](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L117-L120)

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L116-L121


 - [ ] ID-1
[StakeVRT.deposit(uint256,uint256)](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L73-L95) ignores return value by [iVrt.transferFrom(msg.sender,address(this),_amount)](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L78)

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L73-L95


## events-maths
Impact: Low
Confidence: Medium
 - [ ] ID-2
[StakeVRT.setUserScoreDivisor(uint256)](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L54-L57) should emit an event for: 
	- [userScoreDivisor = _userScoreDivisor](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L56) 

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L54-L57


 - [ ] ID-3
[StakeVRT.setPerSecondDivisor(uint256)](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L63-L66) should emit an event for: 
	- [perSecondDivisor = _perSecondDivisor](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L65) 

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L63-L66


## missing-zero-check
Impact: Low
Confidence: Medium
 - [ ] ID-4
[StakeVRT.constructor(address,address)._rSnacks](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L42) lacks a zero-check on :
		- [snacks = _rSnacks](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L43)

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L42


 - [ ] ID-5
[StakeVRT.withdrawETH().to](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L112) lacks a zero-check on :
		- [to.transfer(address(this).balance)](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L113)

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L112


 - [ ] ID-6
[StakeVRT.constructor(address,address)._vrt](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L42) lacks a zero-check on :
		- [vrt = _vrt](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L46)

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L42


## reentrancy-benign
Impact: Low
Confidence: Medium
 - [ ] ID-7
Reentrancy in [StakeVRT.deposit(uint256,uint256)](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L73-L95):
	External calls:
	- [iVrt.transferFrom(msg.sender,address(this),_amount)](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L78)
	State variables written after the call(s):
	- [stakes[msg.sender].lastClaim = block.timestamp](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L87)
	- [stakes[msg.sender].amount = (userStake.amount + _amount)](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L89)
	- [stakes[msg.sender].time += time](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L90)
	- [stakes[msg.sender].unlockTimestamp += time](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L91)
	- [stakes[msg.sender].score = stakes[msg.sender].amount * stakes[msg.sender].time / userScoreDivisor](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L92)

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L73-L95


## reentrancy-events
Impact: Low
Confidence: Medium
 - [ ] ID-8
Reentrancy in [StakeVRT.deposit(uint256,uint256)](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L73-L95):
	External calls:
	- [iVrt.transferFrom(msg.sender,address(this),_amount)](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L78)
	Event emitted after the call(s):
	- [Deposit(msg.sender,_amount,_time,block.timestamp)](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L94)

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L73-L95


## timestamp
Impact: Low
Confidence: Medium
 - [ ] ID-9
[StakeVRT.deposit(uint256,uint256)](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L73-L95) uses timestamp for comparisons
	Dangerous comparisons:
	- [_time > maxExtension](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L84)

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L73-L95


## assembly
Impact: Informational
Confidence: High
 - [ ] ID-10
[console._sendLogPayload(bytes)](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/hardhat/console.sol#L7-L14) uses assembly
	- [INLINE ASM](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/hardhat/console.sol#L10-L13)

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/hardhat/console.sol#L7-L14


## pragma
Impact: Informational
Confidence: High
 - [ ] ID-11
Different versions of Solidity are used:
	- Version used: ['0.8.17', '>=0.4.22<0.9.0', '^0.8.0']
	- [^0.8.0](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/@openzeppelin/contracts/access/Ownable.sol#L4)
	- [^0.8.0](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/@openzeppelin/contracts/token/ERC20/IERC20.sol#L4)
	- [^0.8.0](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/@openzeppelin/contracts/utils/Context.sol#L4)
	- [0.8.17](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L2)
	- [>=0.4.22<0.9.0](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/hardhat/console.sol#L2)

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/@openzeppelin/contracts/access/Ownable.sol#L4


## solc-version
Impact: Informational
Confidence: High
 - [ ] ID-12
Pragma version[^0.8.0](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/@openzeppelin/contracts/utils/Context.sol#L4) allows old versions

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/@openzeppelin/contracts/utils/Context.sol#L4


 - [ ] ID-13
solc-0.8.17 is not recommended for deployment

 - [ ] ID-14
Pragma version[^0.8.0](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/@openzeppelin/contracts/token/ERC20/IERC20.sol#L4) allows old versions

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/@openzeppelin/contracts/token/ERC20/IERC20.sol#L4


 - [ ] ID-15
Pragma version[0.8.17](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L2) necessitates a version too recent to be trusted. Consider deploying with 0.6.12/0.7.6/0.8.16

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L2


 - [ ] ID-16
Pragma version[^0.8.0](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/@openzeppelin/contracts/access/Ownable.sol#L4) allows old versions

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/@openzeppelin/contracts/access/Ownable.sol#L4


 - [ ] ID-17
Pragma version[>=0.4.22<0.9.0](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/hardhat/console.sol#L2) is too complex

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/hardhat/console.sol#L2


## naming-convention
Impact: Informational
Confidence: High
 - [ ] ID-18
Constant [StakeVRT.year](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L25) is not in UPPER_CASE_WITH_UNDERSCORES

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L25


 - [ ] ID-19
Contract [console](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/hardhat/console.sol#L4-L1532) is not in CapWords

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/node_modules/hardhat/console.sol#L4-L1532


 - [ ] ID-20
Parameter [StakeVRT.deposit(uint256,uint256)._time](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L73) is not in mixedCase

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L73


 - [ ] ID-21
Constant [StakeVRT.month](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L24) is not in UPPER_CASE_WITH_UNDERSCORES

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L24


 - [ ] ID-22
Parameter [StakeVRT.setUserScoreDivisor(uint256)._userScoreDivisor](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L54) is not in mixedCase

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L54


 - [ ] ID-23
Parameter [StakeVRT.claimRewards(address)._user](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L102) is not in mixedCase

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L102


 - [ ] ID-24
Parameter [StakeVRT.setPerSecondDivisor(uint256)._perSecondDivisor](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L63) is not in mixedCase

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L63


 - [ ] ID-25
Parameter [StakeVRT.deposit(uint256,uint256)._amount](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L73) is not in mixedCase

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L73


## constable-states
Impact: Optimization
Confidence: High
 - [ ] ID-26
[StakeVRT.rewardFactor](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L22) should be constant

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L22


 - [ ] ID-27
[StakeVRT.scoreFactor](https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L21) should be constant

https://github.com/Mjavala/vrt-staking-audit/blob/e557ab6d1196b8b7102e159b698207ac16316751/contracts/StakeVRT.sol#L21


