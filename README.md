# code-samples
various neat tricks

### get value of object by path. Path can be nested. example: resolvePropDepth('name.first', obj)
```javascript
export function resolvePropDepth(path, obj) {
  return path.split('.').reduce(function (prev, curr) {
    return prev ? prev[curr] : null;
  }, obj || this);
}
```

### truncate string with max character count
```javascript
export function truncate(string, max) {
  return string.length > max ? string.substring(0, max) + '...' : string;
}
```

### flatten any depth of arrays or objects into a single array
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

### fizzbuzz

```javascript
  for (var num=1; num<=100; num++)
    (function(num){
      var string = "";
      // multiples of 3?
      if(num % 3 == 0){
        string += "fizz"
      }
      // multiples of 5?
      if(num % 5 == 0){
        string += "buzz"
      }
      console.log(string || num);
    })(num)
```

### join 2 arrays

```javascript
var animals = ['Cat', 'Dog', 'Mouse'];
var numbers = [1, 2, 3, 4];
var combined = [];

animals.forEach(function (ani) {
  var anibers = numbers.map(function (bers) {
    return ani + bers;
  });
  combined = combined.concat(anibers);
});
console.log(combined);
```
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

obj.on('thisChange', ()=> console.log('THIS changed'));
obj.trigger('thisChange');

obj.on('thatChange', ()=> console.log('THAT changed'));
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
