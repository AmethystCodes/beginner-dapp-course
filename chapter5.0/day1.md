## Chapter 5.0 Day 1 Quests

**1. List all the possible transaction status codes and what each of them mean.**
  * 0: Unknown
  * 1: Transaction Pending - Awaiting Finalization
  * 2: Transaction Finalized - Awaiting Execution
  * 3: Transaction Executed - Awaiting Sealing
  * 4: Transaction Sealed - Transaction Complete. Results committed to the blockchain
  * 5: Transaction Expired
 
**2a. What does setTimeout do?**
 
`setTimeout` runs the `setTxStatus` after 2000 seconds have passed 

**2b. How would we change our code if we wanted the txStatus variable to reset back to its original state after 5 seconds?**
 
Change `setTimeout` to: `setTimeout(() => setTxStatus('Run Transaction'), 5000);`
  
**3. What does the `fcl.tx(transactionId).subscribe(res => {...})` function do?**
 
Allows you to get status updates about your transaction so the user knows the transaction status (Pending, Finalized, Executed, Sealed)
 
**4. Make at least 3 changes to the styling of the application. It can be anything (part of this quest is being creative!). List the 3 changes and point them out in a screenshot.**
 
 * Title
 * Button Colors
 * Rounded Corner

![FinalScreenshot](/images/final.png)
