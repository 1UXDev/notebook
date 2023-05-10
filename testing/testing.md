# Testing
1. Linting
2. Unit Test
3. integration tests
4. E2E Test

### Unit Tests
run small code blocks to test if something works
* like testing all the buttons in a car
* the tests should be independent from the system and each other

### Integration test
* check that the functionality works in context of the system
* e.g. setting a gear in a car while driving

### End-to-End Test
* Run through the whole process

## Testing with Jest
* if my expectations are met: test passed
* npm start -> npm test  // npx jest
  * "no tests found" -> lets define some tests
  * to test "greet.js" -> create a file "greet.test.js"
* The test runs everytime something in the file changes, since it usually is set to --watch-all in the config

```js
test ("this is my test!", () =>{      // test is not a js function, it comes from jest
  const result = greet();
  expect(result).toBe("Hello Stranger");    // toBe is a "matcher", there exist many different ones
  })
```

```js
it("should return hello coach when given yair...", ()=>{  // "it" is same as "test" but nicer to read
  const result = greet("yair")
  expect(result).toBe("Hello yair")
})
```

```js
import {max} from "/max.js"

it("should return greater of integers", () => {
  const result = max(2, 5)
  expect(result).toBe(5)
})

```

### Steps to Test
1. set up situation
2. execute test
3. tidy up
