## Chapter 3.0 Day 1 Quests

**1. Deploy a contract to account 0x03 called "JacobTucker". Inside that contract, declare a constant variable named is, and make it have type String. Initialize it to "the best" when your contract gets deployed.**

```cadence
pub contract JacobTucker {
  pub let is: String

  init() {
    self.is = "the best"
  }
}
```
**2. Check that your variable is actually equals "the best" by executing a script to read that variable. Include a screenshot of the output.**

![Reading a Script in Cadence](/images/read-variable.png)
