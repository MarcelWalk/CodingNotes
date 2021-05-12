# Go / Golang

## Variables

> Variables in Go **HAVE** to be used, else the compiler will throw a error!

### Defining Variables
We have 3 ways to define variables:

Definition and assignment in different lines:
```go
var x int
[...]
x = 42
```

Directly assign value to variable:
```go
var x int = 42
```

Dynamic assignemt of type, in this case the compiler will automatically coose the correct type:
```go
var x := 42
```

### Variable Blocks

Can be used to make code clearer / save some keywords:
```go
var(
    age int = 23
    firstName string = "Marcel"
    lastName string = "Walk"
)
```

### Converting to a different type

Converting numbers is relatively easy, just use `type(value)` to explictly converting `value` to `type`:
```go
var floatingNumber float32 = 3.14
var integerNumber int32 = int(floatingNumber)
```

Converting strings on the other hand is a bit more complex, the following code will search for the unicode number that the integer has:
```go
var someNumber int = 42
var myNumberAsUnicode string = string(someNumber)
```

The result of this conversion is that the `myNumberAsUnicode` variable will be a `*` since thats the character assigned to that number in the unicode table.

We can convert the `int` to a `string` correctly with the `strconv` module and the Itoa function (**I**nteger **to** **a**scii):
```go
import (
	"strconv"
)

func main() {
    var someNumber int = 42
    var correctlyConvertedInt string = strconv.Itoa(someNumber)
}
```

### Conventions
lowercase variables defined in the package are scoped to the package (only can be used within the package):
```go
[...]

myVar := "Scoped to the package"

func main() {
	
}
```

lowercase variables defined in a block are scoped to the block (only can be used within the block):
```go
[...]

func main() {
	myVar := "Scoped to the block (main function)"
}
```

uppercase variables defined in the package are global variables and can be accessed outside of the package:
```go
[...]

GLOBAL := "Can be accessed from the outside"

func main() {
	
}
```

Acronymns shoul'd be uppercase:
```go
HTTPRequest := "http://github.com"
parsedURL := "Some URL"
```