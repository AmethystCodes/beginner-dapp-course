## Chapter 4.0 Day 3 Quests

**1. Write a function that executes a script with all the Cadence types that we reviewed today. Call the script when the page refreshes. Return something random from the Cadence script, and console log it to prove to me your script actually worked.**

```javascript

async function newScript() {
    const response = await fcl.query({
      cadence: `
      pub fun main(
        a: Int, 
        b: String, 
        c: UFix64, 
        d: Address, 
        e: Bool,
        f: String?,
        g: [Int],
        h: {String: Address}
      ): UFix64 {
        return c
      }
      `,
      args: (arg, t) => [
        arg("7", t.Int),
        arg("Hello Github", t.String),
        arg("73.0", t.UFix64),
        arg("0x01", t.Address),
        arg(false, t.Bool),
        arg(null, t.Optional(t.String)),
        arg([4, 2, 3], t.Array(t.Int)),
        arg(
          [
            { key: "FLOAT", value: "0x2d4c3caffbeab845" },
            { key: "EmeraldID", value: "0x39e42c67cc851cfb" }
          ], 
          t.Dictionary({ key: t.String, value: t.Address })
        )
      ]
    })
    console.log(response)
  }

  useEffect(() => {
    newScript()
  }, [])
```
