# PHP Tutorial

An introduction to PHP based on <https://www.learn-php.org/> for COMP 333 Software
Engineering. Check out the official PHP documentation as well. It is really
good. <https://www.php.net/manual/en/langref.php>
Created by Sebastian Zimmeck (szimmeck@wesleyan.edu)

## 1. Hello World

Use the built-in `echo` language construct to print.

```php
    <?php $user = "Patti Smith"; ?>
    <html>
    <head></head>
    <body>
    Hello <?php echo $user; ?>
    </body>
    </html>
```

## 2. Variables

PHP is dynamically typed and does not require explicit type declarations. You
can define a PHP variable using the $ sign at the start of your variable name.
Use the `gettype` function to get the type of a variable. You can also use
common HTML syntax, e.g., to insert a break. Concatenate strings using the `.`
notation.

```php
<html>
<head></head>
<body>
<?php
    echo gettype($x = 1);
    echo "<br>";
    echo gettype($y = "a string");
    echo "<br>";
    echo gettype($z = True);
    echo "<br>";
    echo "Pat " . "Metheney";
?>
</body>
</html>
```

You can perform operations with variables (also note the comment style; it
differs from html).

```php
<html>
<head></head>
<body>
<?php
    $x = 1;
    $y = 2;
    $sum = $x + $y;
    echo $sum;       // prints out 3
?>
</body>
</html>
```

## 3. Loops and Conditionals

For loops are useful it we want to iterate over an array and refer to a member
of the array using a changing index. For example, let's say we have a list of
odd numbers. To print them out, we need to refer to each individually. The code
we write in the for loop can use the index `i`, which changes in every iteration
of the for loop.

```php
<html>
<head></head>
<body>
<?php
$odd_numbers = [1,3,5,7,9];
for ($i = 0; $i < count($odd_numbers); $i=$i+1) {
    $odd_number = $odd_numbers[$i];
    echo $odd_number . "\n";
}
?>
</body>
</html>
```

Here is an example of a while loop that is executed a total of 8 times until the
condition is reached.

```php
<html>
<head></head>
<body>
<?php
$counter = 0;

while ($counter < 10) {
    $counter += 1;
    if ($counter > 8) {
        echo "counter is larger than 8, stopping the loop.";
        break;
    }
    echo "Executing - counter is $counter.<br>";
}
?>
</body>
</html>
```

## 4. Functions

There are two types of functions --- library functions and user functions.
Library functions, such as `array_push` are part of the PHP library and can be
used by anyone. However, you may write your own functions and use them across
your code.

A function receives a list of arguments separated by commas. Every argument only
exists in the context of the function, meaning that they become variables inside
the function block, but are not defined outside of that function block.

```php
<html>
<head></head>
<body>
<?php
// define a function called `sum` that will
// receive a list of numbers as an argument.
function sum($numbers) {
    // initialize the variable we will return
    $sum = 0;

    // sum up the numbers
    // using a foreach loop
    foreach ($numbers as $number) {
        $sum += $number;
    }

    // return the sum to the user
    return $sum;
}

// call the sum function
echo sum([1,2,3,4,5,6,7,8,9,10]);
?>
</body>
</html>
```

## 5. PHP Working in Conjunction with SQL in a Web App Environment

This is where the real power of PHP comes in. Check the code samples on the
class website.
