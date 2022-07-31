## Chapter 4.0 Day 2 Quests

**1. Instead of console logging the result after the script executes, I want you to:**
  * Make a new variable named greeting using useState
  * Set the greeting variable to the response of the script call
  * Create a `<p>` tag after the `<div className={styles.flex}>`tag
  * Put the greeting variable inside of that `<p>` tag. This will make the result of your script show on your webpage!

```javascript
import Head from 'next/head'
import styles from '../styles/Home.module.css'
import Nav from '../components/Nav.jsx';
import { useState, useEffect } from 'react';
import * as fcl from '@onflow/fcl';

export default function Home() {

  const [newGreeting, setNewGreeting] = useState('');
  const [ greeting, setGreeting ] = useState('');

  function runTransaction() {
    console.log("Running Transaction!");
    console.log("Changing the greeting to: " + newGreeting);
  }

  async function executeScript() {
    const response = await fcl.query({
      cadence: `
      import HelloWorld from 0x01

      pub fun main(): String {
        return HelloWorld.greeting
      }
      `, 
      args: (arg, t) => []
    })

    setGreeting(response)
  }

  useEffect(() => {
    executeScript()
  }, [])

  return (
    <div className={styles.container}>
      <Head>
        <title>Emerald DApp</title>
        <meta name="description" content="Created by Amethyst" />
        <link rel="icon" href="https://i.imgur.com/hvNtbgD.png" />
      </Head>

      <Nav />

      <main className={styles.main}>
        <h1 className={styles.title}>
          Welcome to my <a href="https://twitter.com/AmethystCodes" target="_blank">Emerald Dapp!</a>
        </h1>
        <p className={styles.p}>✨ Where Dreams are Made ✨</p>
        
        <div className={styles.flex}>
          <button onClick={runTransaction}>
            Run Transaction
          </button>
          <input onChange={(e) => setNewGreeting(e.target.value)} placeholder="Add a New Greeting" />
          <p>{greeting}</p>
        </div>
      </main>
    </div>
  )
}
```
**2a. I deployed a contract called `SimpleTest` to an account with an address of `0x6c0d53c676256e8c`. I want you to make a button that, when clicked, executes a script to read the `number` variable from that contract. Submit all the code you used to call the script, and the result of the script.**

```javascript
import Head from 'next/head'
import styles from '../styles/Home.module.css'
import Nav from '../components/Nav.jsx';
import { useState, useEffect } from 'react';
import * as fcl from '@onflow/fcl';

export default function Home() {

  const [newGreeting, setNewGreeting] = useState('');
  const [ greeting, setGreeting ] = useState('');
  const [ number, setNumber ] = useState('');

  function runTransaction() {
    console.log("Running Transaction!");
    console.log("Changing the greeting to: " + newGreeting);
  }

  async function executeScript() {
    const response = await fcl.query({
      cadence: `
      import HelloWorld from 0x01

      pub fun main(): String {
        return HelloWorld.greeting
      }
      `, 
      args: (arg, t) => []
    })

    setGreeting(response)
  }

  useEffect(() => {
    executeScript()
  }, [])

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

    setNumber(response)
  }

  return (
    <div className={styles.container}>
      <Head>
        <title>Emerald DApp</title>
        <meta name="description" content="Created by Amethyst" />
        <link rel="icon" href="https://i.imgur.com/hvNtbgD.png" />
      </Head>

      <Nav />

      <main className={styles.main}>
        <h1 className={styles.title}>
          Welcome to my <a href="https://twitter.com/AmethystCodes" target="_blank">Emerald Dapp!</a>
        </h1>
        <p className={styles.p}>✨ Where Dreams are Made ✨</p>
        
        <div className={styles.flex}>
          <button onClick={runTransaction}>
            Run Transaction
          </button>
          <input onChange={(e) => setNewGreeting(e.target.value)} placeholder="Add a New Greeting" />
        </div>
        <br></br>
        <div className={styles.flex}>
          <button onClick={readNumber}>
            Pick a Number
          </button>
        </div>
        <p>{greeting}</p>
        <p>{number}</p>
      </main>
    </div>
  )
}
```
**2b. Then, I want you to remove the button, and make the script execute every time the page refreshes. Submit all the code you used to do this.**

```javascript
import Head from 'next/head'
import styles from '../styles/Home.module.css'
import Nav from '../components/Nav.jsx';
import { useState, useEffect } from 'react';
import * as fcl from '@onflow/fcl';

export default function Home() {

  const [newGreeting, setNewGreeting] = useState('');
  const [ greeting, setGreeting ] = useState('');
  const [ number, setNumber ] = useState('');

  function runTransaction() {
    console.log("Running Transaction!");
    console.log("Changing the greeting to: " + newGreeting);
  }

  async function executeScript() {
    const response = await fcl.query({
      cadence: `
      import HelloWorld from 0x01

      pub fun main(): String {
        return HelloWorld.greeting
      }
      `, 
      args: (arg, t) => []
    })

    setGreeting(response)
  }

  useEffect(() => {
    executeScript()
  }, [])

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

    setNumber(response)
    console.log(response)
  }

  useEffect(() => {
    readNumber()
  }, [])

  return (
    <div className={styles.container}>
      <Head>
        <title>Emerald DApp</title>
        <meta name="description" content="Created by Amethyst" />
        <link rel="icon" href="https://i.imgur.com/hvNtbgD.png" />
      </Head>

      <Nav />

      <main className={styles.main}>
        <h1 className={styles.title}>
          Welcome to my <a href="https://twitter.com/AmethystCodes" target="_blank">Emerald Dapp!</a>
        </h1>
        <p className={styles.p}>✨ Where Dreams are Made ✨</p>
        
        <div className={styles.flex}>
          <button onClick={runTransaction}>
            Run Transaction
          </button>
          <input onChange={(e) => setNewGreeting(e.target.value)} placeholder="Add a New Greeting" />
        </div>
        <div className={styles.flex}>
          <p>{greeting}</p>
        </div>
      </main>
    </div>
  )
}
```
