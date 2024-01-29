<!-- PHP syntax guide  -->
 enclose PHP code in <?php ... ?> tags 

<!-------------->
<!-- Comments: -->
<!-------------->

Single-line comment: // This is a single-line comment
Multi-line comment: /* This is a multi-line comment */

<!-------------->
<!-- Variables: -->
<!-------------->

Start with the $ symbol: $variableName
Case-sensitive: $name and $Name are different

<!-------------->
<!-- Data Types: -->
<!-------------->

String: $str = "Hello, World!";
Integer: $num = 123;
Float (decimal numbers): $floatNum = 3.14;
Boolean: $isTrue = true;
Array: $arr = array(1, 2, 3);
Null: $nullVar = null;

<!-------------->
<!-- Constants: -->
<!-------------->

Constants can be defined using the const keyword, or by using the define()-function. Once a constant is defined, it can never be changed or undefined.

When using the const keyword, only scalar (bool, int, float and string) expressions and constant arrays containing only scalar expressions are accepted. 

The value of a constant is accessed simply by specifying its name. Unlike variables, a constant is not prepended with a $. It is also possible to use the constant() function to read a constant's value if the constant's name is obtained dynamically. Use get_defined_constants() to get a list of all defined constants.

Defined using define(): define("PI", 3.14);

These are the differences between constants and variables:

Constants do not have a dollar sign ($) before them;
Constants may be defined and accessed anywhere without regard to variable scoping rules;
Constants may not be redefined or undefined once they have been set; and
Constants may only evaluate to scalar values or arrays.

<?php
// Simple scalar value
const CONSTANT = 'Hello World';

echo CONSTANT;

// Scalar expression
const ANOTHER_CONST = CONSTANT.'; Goodbye World';
echo ANOTHER_CONST;

const ANIMALS = array('dog', 'cat', 'bird');
echo ANIMALS[1]; // outputs "cat"

// Constant arrays
define('ANIMALS', array(
    'dog',
    'cat',
    'bird'
));
echo ANIMALS[1]; // outputs "cat"
?>

<!-------------->
<!-- Operators: -->
<!-------------->

1.Arithmetic Operator
+ = Addition
- = Subtraction
* = Multiplication
/ = Division
% = Modulo
** = Exponentiation

2.Assignment Operator
     = "equal to

3.Array Operator
    + = Union
    == = Equality
    === = Identity
    != = Inequality
    <> = Inequality
    !== =    Non-identity

4.Bitwise Operator
& = and 
^ = xor
| = not
<< = shift left
>> = shift right

5.Comparison Operator
==  = equal
=== = identical
!=  = not equal
!== = not identical
<>  = not equal
< = less than
<= less than or equal
> = greater than
>= = greater than or equal
<=> = spaceship operator

6.Execution Operator
 `` = backticks  

7.Error Control Operator
    @ = at sign

8.Incrementing/Decrementing Operator
    ++$a = PreIncrement
    $a++ = PostIncrement
    --$a = PreDecrement
    $a-- = Postdecrement

9.Logical Operator
    && = And
    || = Or
    ! = Not
    and = And
    xor = Xor
    or = Or

10.string Operator
    . =  concatenation operator
    .= concatenating assignment operator

11.Type Operator
    instanceof = instanceof

12.Ternary or Conditional operator
   ?: = Ternary operator

13.Null Coalescing Operator
    ??" = null coalescing 

14.Clone new Operator
    clone new = clone new

15.yield from Operator

    yield from = yield from

16.yield Operator
    yield = yield

17.print Operator
    print = print


<!-------------->
<!-- Conditional Statements: -->
<!-------------->

if, else if, else


if ($condition) {
    // code to execute if condition is true
} elseif ($anotherCondition) {
    // code to execute if another condition is true
} else {
    // code to execute if none of the conditions are true
}

<!-------------->
<!-- Loops: -->
<!-------------->

for, while, do-while, foreach


for ($i = 0; $i < 5; $i++) {
    // code to repeat
}

while ($condition) {
    // code to repeat while condition is true
}

do {
    // code to repeat at least once, then check condition
} while ($condition);

foreach ($array as $value) {
    // code to repeat for each element in the array
}


                <!-------------->
                <!-- Functions: -->
                <!-------------->


A function may be defined using syntax such as the following:

function greet($name) {
    echo "Hello, $name!";
}

greet("John");

<!-- Example #1 Passing arrays to functions -->

<?php
function takes_array($input)
{
    echo "$input[0] + $input[1] = ", $input[0]+$input[1];
}
?>

<!-- Example #2 Function Argument List with trailing Comma -->

<?php
function takes_many_args(
    $first_arg,
    $second_arg,
    $a_very_long_argument_name,
    $arg_with_default = 5,
    $again = 'a default string', // This trailing comma was not permitted before 8.0.0.
)
{
    // ...
}
?>

<!-- Example #3 Passing function parameters by reference -->

<?php
function add_some_extra(&$string)
{
    $string .= 'and something extra.';
}
$str = 'This is a string, ';
add_some_extra($str);
echo $str;    // outputs 'This is a string, and something extra.'
?>

<!-- Example #4 Use of default parameters in functions -->

<?php
function makecoffee($type = "cappuccino")
{
    return "Making a cup of $type.\n";
}
echo makecoffee();
echo makecoffee(null);
echo makecoffee("espresso");
?>

<!-- Example #5 Using non-scalar types as default values -->

<?php
function makecoffee($types = array("cappuccino"), $coffeeMaker = NULL)
{
    $device = is_null($coffeeMaker) ? "hands" : $coffeeMaker;
    return "Making a cup of ".join(", ", $types)." with $device.\n";
}
echo makecoffee();
echo makecoffee(array("cappuccino", "lavazza"), "teapot");?>



<!-------------->
<!-- Arrow Functions  -->
<!-------------->

Arrow functions were introduced in PHP 7.4 as a more concise syntax for anonymous functions.

Both anonymous functions and arrow functions are implemented using the Closure class.

Arrow functions have the basic form fn (argument_list) => expr.

Arrow functions support the same features as anonymous functions, except that using variables from the parent scope is always automatic.

When a variable used in the expression is defined in the parent scope it will be implicitly captured by-value. In the following example, the functions $fn1 and $fn2 behave the same way.

<!-- Example #1 Arrow functions capture variables by value automatically -->

<?php

$y = 1;
 
$fn1 = fn($x) => $x + $y;
// equivalent to using $y by value:
$fn2 = function ($x) use ($y) {
    return $x + $y;
};

var_export($fn1(3));
?>

The above example will output:

4

<!-- Example #3 Examples of arrow functions -->

<?php

fn(array $x) => $x;
static fn(): int => $x;
fn($x = 42) => $x;
fn(&$x) => $x;
fn&($x) => $x;
fn($x, ...$rest) => $rest;

?>


<!-------------->
<!-- Arrays: -->
<!-------------->


$colors = array("red", "green", "blue");
echo $colors[0]; // Outputs: red

// Associative Array
$person = array("name" => "John", "age" => 25);
echo $person["name"]; // Outputs: John


<!-------------->
<!-- Classes and Objects: -->
<!-------------->


class Dog {
    public $name;

    function bark() {
        echo "Woof!";
    }
}

$myDog = new Dog();
$myDog->name = "Buddy";
$myDog->bark();


<!-------------->
<!--Namespaces:-->
<!-------------->

Used to organize code and avoid naming conflicts.

namespace MyNamespace;

class MyClass {
    // class code
}

<!-------------->
<!--Traits:-->
<!-------------->

Reusable code in a fine-grained and consistent way.

trait Logger {
    public function log($message) {
        echo $message;
    }
}

class MyClass {
    use Logger;

    // other class code
}


<!-------------->
<!-- Anonymous Classes: -->
<!-------------->

Classes without a name, useful for one-time use.


$obj = new class {
    public function sayHello() {
        echo "Hello, World!";
    }
};

$obj->sayHello();

<!-------------->
<!-- Closures (Anonymous Functions): -->
<!-------------->

Functions without a name, useful for callbacks.


$multiply = function ($a, $b) {
    return $a * $b;
};

echo $multiply(5, 3); // Outputs: 15

<!-- Example #1 Anonymous function example -->

<?php
echo preg_replace_callback('~-([a-z])~', function ($match) {
    return strtoupper($match[1]);
}, 'hello-world');
// outputs helloWorld
?>

<!-- Example #2 Anonymous function variable assignment example -->

<?php
$greet = function($name) {
    printf("Hello %s\r\n", $name);
};

$greet('World');
$greet('PHP');
?>

<!-- Example #3 Inheriting variables from the parent scope -->

<?php
$message = 'hello';

// No "use"
$example = function () {
    var_dump($message);
};
$example();

// Inherit $message
$example = function () use ($message) {
    var_dump($message);
};
$example();

// Inherited variable's value is from when the function
// is defined, not when called
$message = 'world';
$example();

// Reset message
$message = 'hello';

// Inherit by-reference
$example = function () use (&$message) {
    var_dump($message);
};
$example();

// The changed value in the parent scope
// is reflected inside the function call
$message = 'world';
$example();

// Closures can also accept regular arguments
$example = function ($arg) use ($message) {
    var_dump($arg . ' ' . $message);
};
$example("hello");

// Return type declaration comes after the use clause
$example = function () use ($message): string {
    return "hello $message";
};
var_dump($example());
?>

<!-- The parent scope of a closure is the function in which the closure was declared (not necessarily the function it was called from). See the following example: -->

<!-- Example #4 Closures and scoping -->

<?php
// A basic shopping cart which contains a list of added products
// and the quantity of each product. Includes a method which
// calculates the total price of the items in the cart using a
// closure as a callback.
class Cart
{
    const PRICE_BUTTER  = 1.00;
    const PRICE_MILK    = 3.00;
    const PRICE_EGGS    = 6.95;

    protected $products = array();
    
    public function add($product, $quantity)
    {
        $this->products[$product] = $quantity;
    }
    
    public function getQuantity($product)
    {
        return isset($this->products[$product]) ? $this->products[$product] :
               FALSE;
    }
    
    public function getTotal($tax)
    {
        $total = 0.00;
        
        $callback =
            function ($quantity, $product) use ($tax, &$total)
            {
                $pricePerItem = constant(__CLASS__ . "::PRICE_" .
                    strtoupper($product));
                $total += ($pricePerItem * $quantity) * ($tax + 1.0);
            };
        
        array_walk($this->products, $callback);
        return round($total, 2);
    }
}

$my_cart = new Cart;

// Add some items to the cart
$my_cart->add('butter', 1);
$my_cart->add('milk', 3);
$my_cart->add('eggs', 6);

// Print the total with a 5% sales tax.
print $my_cart->getTotal(0.05) . "\n";
// The result is 54.29
?>


<!-------------->
<!-- Error Handling: -->
<!-------------->

Use try, catch, and throw for exception handling.


try {
    // code that might throw an exception
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}


<!-------------->
<!-- Interfaces: -->
<!-------------->

Define a blueprint for classes to implement.



interface MyInterface {
    public function myMethod();
}

class MyClass implements MyInterface {
    public function myMethod() {
        // implementation
    }
}

<!-------------->
<!-- Magic Methods: -->
<!-------------->

Special methods with double underscores (e.g., __construct, __get, __set).


class MagicClass {
    public function __construct() {
        // constructor
    }

    public function __get($name) {
        // magic getter
    }

    public function __set($name, $value) {
        // magic setter
    }
}

<!-------------->
<!-- Traits Composition: -->
<!-------------->

Combining multiple traits into a single class.


trait A {
    // trait A code
}

trait B {
    // trait B code
}

class MyClass {
    use A, B;
    // class code
}

<!-------------->
<!-- Generators: -->
<!-------------->

Simplifies the process of iterating over a set of data.


function myGenerator() {
    yield 1;
    yield 2;
    yield 3;
}

foreach (myGenerator() as $value) {
    echo $value;
}

<!-------------->
<!-- Late Static Binding: -->
<!-------------->

static:: is resolved at runtime based on the class where the method was called, not where it was defined.


class ParentClass {
    public static function whoAmI() {
        echo "I am the parent.";
    }
}

class ChildClass extends ParentClass {
    public static function whoAmI() {
        echo "I am the child.";
        parent::whoAmI(); // Calls the parent method
    }
}


<!-- Anonymous Classes: -->

Classes without a name, useful for one-time use.


$obj = new class {
    public function sayHello() {
        echo "Hello, World!";
    }
};

$obj->sayHello();

<!-------------->
<!-- Composer (Dependency Manager): -->
<!-------------->

Used to manage PHP project dependencies.


// composer.json
{
    "require": {
        "vendor/package": "1.0.0"
    }
}

<!-------------->
<!-- Namespaces and Autoloading: -->
<!-------------->

Organize code into namespaces and use autoloading to load classes automatically.


// autoload.php
spl_autoload_register(function ($class) {
    include 'classes/' . $class . '.class.php';
});


