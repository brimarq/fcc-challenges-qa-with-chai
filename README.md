# fCC Challenges: Quality Assurance with Chai  

https://learn.freecodecamp.org/information-security-and-quality-assurance/quality-assurance-and-testing-with-chai

## REF:  
 [ChaiJS website](https://www.chaijs.com/)  
 [MochaJS website](https://mochajs.org/)  
 [Chai assert API](https://www.chaijs.com/api/assert/)  
 [Zombie.js](https://zombie.js.org/) 

___
## CHALLENGES:  

### Unit Tests (#1 - 18)  
Use the following `assert` methods to get the tests in `tests/1_unit-tests.js` to pass.

### 1. Learn How JavaScript Assertions Work  
`.isNull(value, [message])`  
Asserts that `value` is `null`.  

`.isNotNull(value, [message])`  
Asserts that `value` is ***not*** `null`.      
```js
test('#isNull, #isNotNull', function(){
  assert.isNull(null, 'null is null');
  assert.isNotNull(1, '1 is not null');
});
```

### 2. Test if a Variable or Function is Defined  
`.isDefined(value, [message])`  
Asserts that `value` is not [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined).  

`.isUndefined(value, [message])`   
Asserts that `value` is [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined).     
```js
test('#isDefined, #isUndefined', function(){
  assert.isDefined( null, 'null is not undefined');
  assert.isUndefined( undefined, 'undefined IS undefined');
  assert.isDefined( 'hello', 'a string is not undefined' );
});
```

### 3. Use `assert.isOK` and `assert.isNotOK`  
`.isOk(object, [message])`   
Asserts that `object` is [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy).  

`.isNotOk(object, [message])`  
Asserts that `object` is [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy).   
```js
test('#isOk, #isNotOk', function(){
  assert.isNotOk( null, 'null is falsey');
  assert.isOk( "I'm truthy", 'a string is truthy');
  assert.isOk( true, 'true is truthy' );
});
```

### 4. Test for Truthiness  
`.isTrue(value, [message])`   
Asserts that `value` is `true`.  

`.isNotTrue(value, [message])`   
Asserts that `value` is ***not*** `true`.  

Conversely, assert also has `.isFalse()` and `.isNotFalse()` methods that assert value is false/not false.  
```js
test('#isTrue, #isNotTrue', function(){
  assert.isTrue( true, 'true is true');
  assert.isTrue( !!'double negation', 'double negation of a truthy is true');
  assert.isNotTrue({ value: 'truthy' }, 'A truthy object is NOT TRUE (neither is false...)' );
});
```

### 5. Use the Double Equals to Assert Equality  
`.equal(actual, expected, [message])`   
Asserts [non-strict equality (==)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Equality) of `actual` and `expected`.  

`.notEqual(actual, expected, [message])`   
Asserts [non-strict inequality (!=)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Inequality) of `actual` and `expected`.

If `actual` and `expected` are not of the same type, JavaScript attempts to convert the operands to an appropriate type for the comparison.    
```js
test('#equal, #notEqual', function(){ 
  assert.equal( 12, '12', 'numbers are coerced into strings with == ');
  assert.notEqual( {value: 1}, {value:1}, '== compares object references, NOT values');
  assert.equal( 6 * '2', '12', 'Number * String representation of number -> Number');
  assert.notEqual( 6 + '2', '12', 'Oops! Number + String -> concatenation' );
});
```

### 6. Use the Triple Equals to Assert Strict Equality  
`.strictEqual(actual, expected, [message])`    
Asserts [strict equality (===)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Identity) of `actual` and `expected`.  

`.notStrictEqual(actual, expected, [message])`   
Asserts [strict inequality (!==)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Nonidentity) of `actual` and `expected`.  

As strict equality/strict inequality compares value *and* type of each operand, no type coercion is done.  
```js
test('#strictEqual, #notStrictEqual', function(){
  assert.notStrictEqual( 6, '6', '=== checks value AND type' );
  assert.strictEqual( 6, 3*2 );
  assert.strictEqual( 6 * '2', 12 );
  assert.notStrictEqual( [1, 'a', {} ], [1, 'a', {}], '=== compares object references, NOT values' );
});
```

### 7. Assert Deep Equality with `.deepEqual` and `.notDeepEqual`  
`.deepEqual(actual, expected, [message])`   
Asserts that `actual` is deeply equal to `expected`.  

`.notDeepEqual(actual, expected, [message])`  
Asserts that `actual` is ***not*** deeply equal to `expected`.  
```js
test('#deepEqual, #notDeepEqual', function(){
  assert.deepEqual( { a: '1', b: 5 } , { b: 5, a: '1' }, "keys order doesn't matter" );
  assert.notDeepEqual( { a: [5, 6] }, { a: [6, 5] }, "array elements position does matter !!" );
});
```
NOTE: the "deep equality" comparison used here employs [chai's deep-eql](https://github.com/chaijs/deep-eql), which behaves differently than simple strict/non-strict equality operators. It checks an object's keys recursively, until it finds primitives to check for referential equality, using strict equality for non-traversable nodes according to [Object.is](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is): 
```js
assert.deepEqual( { a: '1', b: 5 } , { b: 5, a: '1' } ); // pass (a === a)
assert.deepEqual( { a: '1', b: 5 } , { b: 5, a: 1 } ); // fail (a !== a)
```

### 8. Compare the Properties of Two Elements   
`.isAbove(valueToCheck, valueToBeAbove, [message])`   
Asserts `valueToCheck` is strictly greater than (`>`) `valueToBeAbove`.  

`.isAtMost(valueToCheck, valueToBeAtMost, [message])`   
Asserts `valueToCheck` is less than or equal to (`<=`) `valueToBeAtMost`.    
```js
test('#isAbove, #isAtMost', function() {
  assert.isAtMost('hello'.length , 5);
  assert.isAbove(1, 0);
  assert.isAbove(Math.PI, 3);
  assert.isAtMost(1 - Math.random(), 1);
});
```

### 9. Test if One Value is Below or At Least as Large as Another  
`.isBelow(valueToCheck, valueToBeBelow, [message])`  
Asserts `valueToCheck` is strictly less than (`<`) `valueToBeBelow`.  

`.isAtLeast(valueToCheck, valueToBeAtLeast, [message])`  
Asserts `valueToCheck` is greater than or equal to (`>=`) `valueToBeAtLeast`.     
```js
test('#isBelow, #isAtLeast', function() {
  assert.isAtLeast('world'.length , 5);
  assert.isAtLeast(2*Math.random(), 0);
  assert.isBelow(5 % 2, 2);
  assert.isBelow(2/3, 1);
});
```

### 10. Test if a Value Falls within a Specific Range    
`.approximately(actual, expected, delta, [message])`   
Asserts that the target is equal `expected`, to within a +/- `delta` range. Use the minimum range to make the tests always pass. The `delta` should be < 1.  
```js
test('#approximately', function() {
  assert.approximately(weirdNumbers(0.5), 1, 0.5); // In this case, delta = (1 - 0.5)
  assert.approximately(weirdNumbers(0.2), 1, 0.8); // In this case, delta = (1 - 0.2)
});
```

### 11. Test if a Value is an Array   
`.isArray(value, [message])`   
Asserts that `value` is an array.     

`isNotArray(value, [message])`  
Asserts that `value` is ***not*** an array.     
```js
test('#isArray, #isNotArray', function() {
  assert.isArray('isThisAnArray?'.split(''), 'String.prototype.split() returns an Array');
  assert.isNotArray([1,2,3].indexOf(2), 'indexOf returns a number.');
});
```

### 12. Test if an Array Contains an Item  
`.include(haystack, needle, [message])`   
Asserts that `haystack` includes `needle`. Can be used to assert the inclusion of a value in an array, a substring in a string, or a subset of properties in an object. Uses strict equality (===).  

`.notInclude(haystack, needle, [message])`  
Asserts that `haystack` does not include `needle`. Can be used to assert the absence of a value in an array, a substring in a string, or a subset of properties in an object. Uses strict equality (===).  
```js
test('Array #include, #notInclude', function() {
  assert.notInclude(winterMonths, 'jul', "It's summer in july...");
  assert.include(backendLanguages, 'javascript', 'JS is a backend language !!');
});
```

### 13. Test if a Value is a String  
`.isString(value, [message])`   
Asserts that `value` is a string.  

`.isNotString(value, [message])`  
Asserts that value is ***not*** a string.    
```js
test('#isString, #isNotString', function() {
  assert.isNotString(Math.sin(Math.PI/4), 'a float is not a string');
  assert.isString(process.env.PATH, 'env vars are strings (or undefined)');
  assert.isString(JSON.stringify({type: 'object'}), 'a JSON is a string');
});
```

### 14. Test if a String Contains a Substring    
`.include()` and `.notInclude()` work for strings, too. They assert that the actual string contains the expected substring.         
```js
test('String #include, #notInclude', function() {
  assert.include('Arrow', 'row', "Arrow contains row...");
  assert.notInclude('dart', 'queue', "But a dart doesn't contain a queue");
});
```

### 15. Use Regular Expressions to Test a String    
`.match(value, regexp, [message])`  
Asserts that `value` matches the regular expression `regexp`.  

`.notMatch(value, regexp, [message])`  
Asserts that `value` does not match the regular expression `regexp`.  
```js
test('#match, #notMatch', function() {
  var regex =  /^#\sname\:\s[\w\s]+,\sage\:\s\d+\s?$/;
  assert.match(formatPeople('John Doe', 35), regex);
  assert.notMatch(formatPeople('Paul Smith III', 'twenty-four'), regex);
});
```

### 16. Test if an Object has a Property  
`.property(object, property, [message])`  
Asserts that `object` has a direct or inherited property named by `property`.  

`.notProperty(object, property, [message])`  
Asserts that `object` does ***not*** have a direct or inherited property named by `property`.         
```js
test('#property, #notProperty', function() {
  assert.notProperty(myCar, 'wings', 'A car has not wings');
  assert.property(airlinePlane, 'engines', 'planes have engines');
  assert.property(myCar, 'wheels', 'Cars have wheels');
});
```

### 17. Test if a Value is of a Specific Data Structure Type  
`.typeOf(value, name, [message])`  
Asserts that `value`'s type is `name`, as determined by [Object.prototype.toString](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString#Description).  

`.notTypeOf(value, name, [message])`   
Asserts that `value`'s type is ***not*** `name`, as determined by [Object.prototype.toString](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString#Description).  

The `name` argument in both of the above is of type: String.          
```js
test('#typeof, #notTypeOf', function() {
  assert.typeOf(myCar, 'object');
  assert.typeOf(myCar.model, 'string');
  assert.notTypeOf(airlinePlane.wings, 'string');
  assert.typeOf(airlinePlane.engines, 'array');
  assert.typeOf(myCar.wheels, 'number');
});
```

### 18. Test if an Object is an Instance of a Constructor    
`.instanceOf(object, constructor, [message])`   
Asserts that `object` is an instance of `constructor`.  

`.notInstanceOf(object, constructor, [message])`   
Asserts that `object` is ***not*** an instance of `constructor`.  
  
```js
test('#instanceOf, #notInstanceOf', function() {
  assert.notInstanceOf(myCar, Plane);
  assert.instanceOf(airlinePlane, Plane);
  assert.instanceOf(airlinePlane, Object, 'everything is an Object');
  assert.notInstanceOf(myCar.wheels, String );
});
```

### Functional Tests (#19 - 24)  
Get the tests in `tests/2_functional-tests.js` to pass.

### 19. Run Functional Tests on API Endpoints using Chai-HTTP  
Assert that `res.status == 200` and `res.text == 'hello Guest'`.

```js
// If no name is passed, the endpoint responds with 'hello Guest'.
test('Test GET /hello with no name', function(done) { // Don't forget the callback...
  chai.request(server) // 'server' is the Express App
  .get('/hello') // http_method(url). NO NAME in the query !
  .end(function(err, res) { // res is the response object
    // Test the status and the text response (see the example above). 
    // Please follow the order -status, -text. We rely on that in our tests.
    // It should respond 'Hello Guest'
    assert.equal(res.status, 200);
    assert.equal(res.text, 'hello Guest');
    done(); // Always call the `done()` callback when finished.
  });
});
```
### 20. Run Functional Tests on API Endpoints using Chai-HTTP (II)  
Send your name in the query and test the `.status` and `.text` in the response.   

```js
test('Test GET /hello with your name', function(done) { // Don't forget the callback... 
  chai.request(server) // 'server' is the Express App
  .get('/hello?name=Brian') /** <=== Put your name in the query **/ 
  .end(function(err, res) { // res is the response object
    // Test the status and the text response. Follow the test order like above.
    assert.equal(res.status, 200);
    assert.equal(res.text, 'hello Brian'/** <==  Put your name here **/);
    done(); // Always call the 'done()' callback when finished.
  });
});
```

### 21. Run Functional Tests on an API Response using Chai-HTTP (III) - PUT method  
In the next example we'll see how to send data in a request payload (body).  
We are going to test a PUT request. The '/travellers' endpoint accepts a JSON object taking the structure:
```
{surname: [last name of a traveller of the past]}
```
The route responds with:   
```
{name: [first name], surname:[last name], dates: [birth - death years]}
```
See the server code for more details.  
Send `{surname: 'Colombo'}`. Replace assert.fail() and make the test pass.  
Check for 1) `status`, 2) `type`, 3) `body.name`, 4) `body.surname`  
Follow the assertion order above, We rely on it.

```js
test('send {surname: "Colombo"}',  function(done) {
  // we setup the request for you...
  chai.request(server)
  .put('/travellers')
  /** send {surname: 'Colombo'} here **/
  .send({surname: 'Colombo'})
  .end(function(err, res) { 
    /** your tests here **/
    assert.equal(res.status, 200);
    assert.equal(res.type, 'application/json');
    assert.equal(res.body.name, 'Cristoforo'); 
    assert.equal(res.body.surname, 'Colombo');
    done(); // Never forget the 'done()' callback...
  });
});
```

### 22. Run Functional Tests on API Response using Chai-HTTP (IV) - PUT method  
This exercise is similar to the preceding one. Look at it for the details.  
Send {surname: 'da Verrazzano'}. Replace assert.fail() and make the test pass.  
Check for 1) `status`, 2) `type`, 3) `body.name`, 4) `body.surname`  
Follow the assertion order above, We rely on it.  

```js
test('send {surname: "da Verrazzano"}', function(done) {
  /** place the chai-http request code here... **/
  chai.request(server)
  .put('/travellers')
  .send({surname: "da Verrazzano"})
  .end(function(err, res) {
    /** place your tests inside the callback **/
    assert.equal(res.status, 200);
    assert.equal(res.type, 'application/json');
    assert.equal(res.body.name, 'Giovanni'); 
    assert.equal(res.body.surname, 'da Verrazzano');
    done();
  });
});
```

### 23. Run Functional Tests using a Headless Browser  
In the next challenges we are going to simulate the human interaction with a page using a device called 'Headless Browser'.  

A headless browser is a web browser without a graphical user interface. These kind of tools are particularly useful for testing web pages as they are able to render and understand HTML, CSS, and JavaScript the same way a browser would.  

For these challenges we are using Zombie.JS. It's a lightweight browser which is totally based on JS, without relying on additional binaries to be installed. This feature makes it usable in an environment such as Glitch. There are many other (more powerful) options.  

Look at the examples in the code for the exercise directions Follow the assertions order, We rely on it.  

```js

```

https://leeward-fear.glitch.me