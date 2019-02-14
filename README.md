# fCC Challenges: Quality Assurance with Chai  

https://learn.freecodecamp.org/information-security-and-quality-assurance/quality-assurance-and-testing-with-chai

## REF:  
 https://www.chaijs.com/  
 https://mochajs.org/  

## CHALLENGES:

### 1. Learn How JavaScript Assertions Work  
In `tests/1_unit-tests.js`, use `assert.isNull(value, [message])` or `assert.isNotNull(value, [message])` to make the tests pass.  
Ref: https://www.chaijs.com/api/assert/#method_isnull
 
```js
test('#isNull, #isNotNull', function(){
  assert.isNull(null, 'null is null');
  assert.isNotNull(1, '1 is not null');
});
```

### 2. Test if a Variable or Function is Defined  
In `tests/1_unit-tests.js`, use `assert.isDefined(value, [message])` or `assert.isUndefined(value, [message])` to make the tests pass.  
Ref: https://www.chaijs.com/api/assert/#method_isundefined  
```js
test('#isDefined, #isUndefined', function(){
  assert.isDefined( null, 'null is not undefined');
  assert.isUndefined( undefined, 'undefined IS undefined');
  assert.isDefined( 'hello', 'a string is not undefined' );
});
```

### 3. Use `assert.isOK` and `assert.isNotOK`  
In `tests/1_unit-tests.js`, use `assert.isOk(object, [message])` or `assert.isNotOk(object, [message])` to make the tests pass (.isOk(truthy) and .isNotOk(falsey) will pass).  
Ref: https://www.chaijs.com/api/assert/#method_isok  
```js
test('#isOk, #isNotOk', function(){
  assert.isNotOk( null, 'null is falsey');
  assert.isOk( "I'm truthy", 'a string is truthy');
  assert.isOk( true, 'true is truthy' );
});
```

### 4. Test for Truthiness  
In `tests/1_unit-tests.js`, use `assert.isTrue(value, [message])` or `assert.isNotTrue(value, [message])` to make the tests pass ( .isTrue(true) and .isNotTrue(everything else) will pass. .isFalse() and .isNotFalse() also exist).  
Ref: https://www.chaijs.com/api/assert/#method_istrue  
```js
test('#isTrue, #isNotTrue', function(){
  assert.isTrue( true, 'true is true');
  assert.isTrue( !!'double negation', 'double negation of a truthy is true');
  assert.isNotTrue({ value: 'truthy' }, 'A truthy object is NOT TRUE (neither is false...)' );
});
```

### 5. Use the Double Equals to Assert Equality  
In `tests/1_unit-tests.js`, use `assert.equal(actual, expected, [message])` and  `assert.notEqual(actual, expected, [message])` to make the tests pass. These methods compare objects using `==`.  
Ref: https://www.chaijs.com/api/assert/#method_equal  
```js
test('#equal, #notEqual', function(){ 
  assert.equal( 12, '12', 'numbers are coerced into strings with == ');
  assert.notEqual( {value: 1}, {value:1}, '== compares object references, NOT values');
  assert.equal( 6 * '2', '12', 'Number * String representation of number -> Number');
  assert.notEqual( 6 + '2', '12', 'Oops! Number + String -> concatenation' );
});
```
