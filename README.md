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
