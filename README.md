# code-samples
various neat tricks

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
var cache = item; //cache the value

function checkItem() {
  if(item === cache) { // item is the same as cache?
    setTimeout(checkItem, 250); //check value every 250ms
    console.log('no change');
    return; // start over
  }
  cache = item;
  console.log('changed');
}

function changeItem() {
  item = false;
}

checkItem(); 
setTimeout(changeItem(), 5000)
```
