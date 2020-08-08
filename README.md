# code-samples
various neat tricks

### get value of object by path. Path can be nested. example: resolvePropDepth('name.first', obj)
```javascript
function resolvePropDepth(path, obj) {
  return path.split(".").reduce((prev, curr) => {
    return prev ? prev[curr] : null;
  }, obj);
}
```
example: [https://codepen.io/novym/pen/ExKarww](https://codepen.io/novym/pen/ExKarww)


### truncate string with max character count
```javascript
export function truncate(string, max) {
  return string.length > max ? string.substring(0, max) + '...' : string;
}
```
example: [https://codepen.io/novym/pen/yYGgre](https://codepen.io/novym/pen/yYGgre)

### flatten any depth of arrays, objects, or primitives into a single array with any amount of arguments
```javascript
export function flatten() {
  const flat = [];
  for (let i = 0; i < arguments.length; i++) {
    if (arguments[i] instanceof Array) {
      flat.push(...flatten(...arguments[i]));
    } else if (arguments[i] instanceof Object) {
      flat.push(...flatten(...Object.values(arguments[i])));
    } else {
      flat.push(arguments[i]);
    }
  }

  return flat;
}
```
example: [https://codepen.io/novym/pen/ZPdyBK](https://codepen.io/novym/pen/ZPdyBK)

### fizzbuzz

```javascript
 function fizzBuzz() {
   for (let num = 1; num <= 100; num++)
    (function(num) {
      let string = "";
      // multiples of 3?
      if (num % 3 == 0){
        string += 'fizz'
      }
      // multiples of 5?
      if (num % 5 == 0){
        string += 'buzz'
      }
      
      if (num % 7 == 0) {
        string += 'bazz'
      }
      
      console.log(string || num);
    })(num)
 } 

 fizzBuzz();
```
example: [https://codepen.io/novym/pen/MKRzRy](https://codepen.io/novym/pen/MKRzRy)

### zip 2 arrays

```javascript
function zip(array1, array2) {
  let zipped = [];
  
  array1.forEach(itemA => {
    const joined = array2.map(itemB => {
      return itemA + itemB;
    });
    
    zipped = [...zipped, ... joined];
  });
  
  return zipped
}
```
example: [https://codepen.io/novym/pen/jOqEdRV](https://codepen.io/novym/pen/jOqEdRV)


### watch for variable change
```javascript
var item = 2; // init value
var CACHE = item; //cache the value

function checkItem() {
  if(item === CACHE) { // item is the same as cache?
    setTimeout(checkItem, 250); //check value every 250ms
    document.write('<p style="color: red">'+ item +'</p>')
    return; // start over
  }
  CACHE = item;
  document.write('<p style="color: green">'+ item +'</p>');
}

checkItem();

function changeItem() {
  item = false;
}

setTimeout(changeItem, 3000);
```
example: [https://codepen.io/novym/pen/QXdBez](https://codepen.io/novym/pen/QXdBez)

### Group 2 collections by id
```javascript
const groupFamily = (parents, children) =>
  parents.map(adult => (
    {
      ...adult, 
      children: [...children.filter(child => adult.id === child.parentId)]
    }
  )).filter(adult => adult.children.length);
```
example: [https://codepen.io/novym/pen/RqYVXx](https://codepen.io/novym/pen/RqYVXx)

### read file line by line and test if numbers are even or odd

```javascript
var readStream = require('fs').createReadStream(process.argv[2]);
var readlines = require('readline').createInterface({
  input: readStream
});

readlines.on('line', function (line) {
  if (line%2 === 0) {
      console.log(1);
    } else {
      console.log(0);
    }
});

readlines.on('error', function(error) {
  console.log(error);
});
```

### addEvent listener mixin
```javascript
const obj = addEventing({ id: 1, type: 'inherited' });

obj.on('thisChange', () => console.log('THIS changed'));
obj.trigger('thisChange');

obj.on('thatChange', () => console.log('THAT changed'));
obj.trigger('thatChange');


function addEventing(object) {
  object.events = object.events || [];
  object.on = function(event, callback) {
    object.events.push({ eventName: event, action: callback });
  };

  object.trigger = function(event) {
    object.events.forEach(eventObj => {
      eventObj.eventName === event ? eventObj.action() : null;
    });
  };

  return object;
}
```
