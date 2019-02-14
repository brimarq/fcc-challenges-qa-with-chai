# fCC Challenges: Quality Assurance with Chai  

https://learn.freecodecamp.org/information-security-and-quality-assurance/quality-assurance-and-testing-with-chai

## REF:  
 https://www.chaijs.com/  
 https://mochajs.org/  

## CHALLENGES:

### 1. Learn How JavaScript Assertions Work  
Use assert.isNull() or assert.isNotNull() to make the tests pass.  

In `tests/1_unit-tests.js`:  
```js
test('#isNull, #isNotNull', function(){
  // .isNull(value, [message]) 
  // .isNotNull(value, [message]) 
  // https://www.chaijs.com/api/assert/#method_isnull 
  assert.isNull(null, 'null is null');
  assert.isNotNull(1, '1 is not null');
});
```
