# code-samples
code samples for fun

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
