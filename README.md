# Is Javascript a pass-by-value, or a pass-by-reference?

 * In practice the answer is actually: ```'neither'```
 * Now, technically, ```Javascript is pass-by-value```.

Lets look at the simple example for primitive values

```javascript
function changeThisValue(param) {  
    param = 2;
}

var myNumber = 9;  
console.log(myNumber);  
changeThisValue(myNumber);  
console.log(myNumber);

// Output:
// 9
// 9
```

### But take a look at this code

```javascript
function changeThisValue(param) {  
    param.value = 2;
}

var obj = {value: 9};
console.log(obj.value);
changeThisValue(obj);
console.log(obj.value);

// Output:
// 9
// 2
```

So, ok, clearly it's pass-by-reference, 'NO'.. But why??

If it were pass-by-value, we would be unable to change the value of the ```passed-in object```, we would be changing a copy of that value inside changeThisValue().

Well, now that you're convinced ```Javascript is pass-by-reference```, look at this:

```javascript
function changeThisValue(param) {  
    param = {value: 2};
}

var obj = {value: 9};  
console.log(obj.value);  
changeThisValue(obj);  
console.log(obj.value);

// Output:
// 9
// 9
```
In this case, we've assigned a new object to ```param```.

In ```pass-by-reference```, one would expect ```obj``` to reflect this change, but it does not.

So, here's what's happening:

Javascript is actually passing a reference to obj by value. <b>(Say that again...?)</b>

When you call changeThisValue(obj), you're creating two (completely independent) references to the same object. Outside of the function, you have ```obj```, and inside the function, you have ```param```. They both ```refer the same object in memory```, but the reference variables themselves are independent.

>So, what's the answer? Technically (language internals), it's pass-by-value. In practice, I'd put it like this: Javascript is pass-by-reference for objects, 


### Another simple example

#### Pass by value

```js
let a = 1;
let b = a;
b = b + 2;
console.log(a, b); // 1 3
```
The first statement `let a = 1` defines a variable `a` initialized with the number `1`.

The second statement `let b = a` defines another variable `b` and initializes it with the `value of a` variable — which is passing by value. 

#### Pass by reference

```js
let a = [1];
let b = a;
b.push(2);
console.log(a, b); // [1, 2]  [1, 2]
```
When creating an object you’re given a `reference` to that `object`. If two variables hold the same reference, then `changing the object reflects in both variables`.
