# Token Tester

### :sparkles: *Test a variety of unconventional tokens against your smart contracts* :sparkles:

"Wow, it's just a modifier? Now that's *ergonomic*"

-chad dev, probably

---

## Get Started & Usage

Install *token-tester*:

```bash
forge install bespoke-tokens/token-tester
```

*Decorate your test functions with the TokenTester modifier(s)*
```solidity
import "forge-std/Test.sol";

// *-*-*-*-* Import TokenTester *-*-*-*-*
import {TokenTester} from "token-tester/TokenTester.sol";

// *-*-*-*-* Inherit the TokenTester contract *-*-*-*-*
contract ExampleTest is Test, TokenTester {
    function setUp() public {
        // initialize your contract
    }
    
    // *-*-*-*-* Decorate your test with `usesERC20TokenTester`                       *-*-*-*-*
    // *-*-*-*-* The test is executed 22 times, each time with a different test token *-*-*-*-*
    function testDeposit() public usesERC20TokenTester {
        deal(address(tokenTest), address(this), 100);
        
        // use the inherited `tokenTest` (an ERC20) against the contracts
        myContract.deposit(address(tokenTest), 100);
        
        // perform typical assertions
    }
}
```

Enable token tester when running Foundry unit tests:
```bash
TOKEN_TEST=true; forge test --ffi

# view report.html in your browser
```

TODO: include html screenshot

## Why Token Tester is Useful
Developers face the challenge of unknowingly interfacing with miscompliant tokens. Hundreds[1] of[2] thousands[3] of[4] dollars[5]  in audits and bug bounties have been paid out for logical errors regarding token integrations. ERC standards are a growing list, now comprised of ERC-20, ERC-721, ERC-777, and ERC-4626 with more standards pending.

Token Tester provides a suite of *bespoke tokens* that encompass this range of standards and more, including tokens with fee-on-transfer logic, tokens with re-entrancy vulnerabilities, and tokens with malicious implementations.

## Token Pool:
Our full catalog of tokens can be found here:
- [weird-erc20](https://github.com/d-xo/weird-erc20)
- More soon, which includes actually-deployed contracts


TODO: cite code4rena and immunefi reports. Rari vault re-entrancy with cETH was 1 million
TODO: add more to catalog?

## Use Cases
Token Tester can be used in a variety of scenarios, including:

- Whitelist collateral tokens - Understand how your protocol may behave when choosing to whitelist a new token standard

- Deposit accounting - Confirm that tokens sporting fee-on-transfer are accounted for correctly

- Vault reward emissions - Safely distribute rewards to users through vault emissions and be confident your re-entrancy guards work as expected

- Swap rebasing economics - Ensure that rebasing token economics are handled correctly in your AMM 

TODO:cite AMP rebasing swap event

## Future Work

Token Tester was started as a hackathon project for ETHDenver 2023. If useful, our intention is to expand our token-standards (to include ERC-721, ERC-1155, ERC-777, and ERC-4626.

We also hope to procure deployed tokens to expand the Token Test Pool
