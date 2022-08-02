## Chapter 4.0 Day 4 Quests

**1. I deployed a contract called SimpleTest to an account with an address of 0x6c0d53c676256e8c. I want you to make a button that, when clicked, sends a transaction to change the number variable from that contract. If you're curious, you can see the contract here: https://flow-view-source.com/testnet/account/0x6c0d53c676256e8c/contract/SimpleTest**

```javascript

// Button that changess the `number` variable in the contract
<div className={styles.flex}>
  <input onChange={(e) => setNewNumber(e.target.value)} placeholder="Add a New Number!" />
    <button onClick={updateNumber}>Update Number</button>
</div>

```

**2. Immediately after you send the transaction, wait for the transaction to be "Sealed" just like we did today. Then, call a script to read the number from the contract. Console log the result.**

Submit all the code you used to send the transaction, and the result of the script.

```javascript
async function updateNumber() {
    const transactionId = await fcl.mutate({
      cadence: `
      import SimpleTest from 0x6c0d53c676256e8c
 
      transaction(myNewNumber: Int) {
       
        prepare(signer: AuthAccount) {}
         
        execute {
          SimpleTest.updateNumber(newNumber: myNewNumber)
        }
      }
      `,
      args: (arg, t) => [
        arg(newNumber, t.Int)
      ],
      proposer: fcl.authz,
      payer: fcl.authz,
      authorization: [fcl.authz],
      limit: 999
    })
 
    console.log("Here is the transactionId: " + transactionId);
 
    await fcl.tx(transactionId).onceSealed();
    readNumber(); // Result 44
  }
 
  async function readNumber() {
    const response = await fcl.query({
      cadence: `
      import SimpleTest from 0x6c0d53c676256e8c
 
      pub fun main(): Int {
        return SimpleTest.number
      }
      `,
      args: (arg, t) => []
    })
 
    setNewNumber(response)
    console.log(response)
  }
 
  useEffect(() => {
    readNumber()
  }, [])
```
