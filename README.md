#js-assessment

#1. 

The function `bar()` will log the integer `13` because `bar()` is being called within the closure of `foo()`, after `this.a` has been assigned to `13`. Since `bar()` does not set a value for the property `a` within its own closure, the interpreter looks 'up' a scope until it finds a value for the property it is attempting to log. 

The function `foo()` is being called on the same scope where `a` was previously set to `7`, so it is overriding the previously set value. If `foo()` were altered not to change the value of `a` before calling `bar()`, the value logged would instead be `7`.

#2. 
```javascript
let arr = ["apple", "orange", "banana"];
let rx = /^a*b+/g;
  
arr.forEach((fruit) => {
  console.log(fruit.match(rx));
});

// logs:
// null
// null
// ["b"]
```

#3. 

The value of `foo.count` is still `0` because neither `foo()` nor the `for...in` loop alter the value of `foo.count`. `foo()` logs the argument it is given, and the `for...in` loop passes the value of `i` to `foo()`. 

#4.
```javascript
function Foo() {
  this.count = 0;
  this.increment = () => { 
    console.log('foo:', ++this.count)
  };
}

let foo = new Foo();

foo.count = 5;

for (let i = 0; i < 5; i++) {
  foo.increment();
}

console.log(foo.count); // equals 10
```
#5.
```javascript
var a = 0.1,
    b = 0.2,
    c = parseFloat((a + b).toFixed(1));

if (c === 0.3) {
  console.log("Math is fun!");
}
```

#6.

The variable `a` is truthy because `13` doesn't equal `undefined`, `0`, an empty string, `false` or `null`. However truthiness does not mean an expression loosely equals `true`. On a low level the loose equality operator first converts both values to a common type and then performs a strict comparion with `===`. An integer such as `13` won't equal `true` when the type conversion and strict comparison are performed.

#7.

The function performs a type check that will not work as the author intended.

If `null` is passed to `extend` the function will throw, because `typeof null` returns `'object'`, and `null.hasOwnProperty`
is not a function. To correct for this I would check to see that neither argument passed to `extend()` is `null`.

```javascript
var extend = function(obj, ext) {
  if (obj === null || ext === null) {
	  console.log('cannot extend null or extend from null');
	  return false;
  }
  if (typeof obj === 'object' && typeof ext === 'object') {
	  for (var i in ext) {
		  if(!obj.hasOwnProperty(i)) {
			  obj[i] = ext[i];
		  }
	  }
  return obj;
  }
};
```
