---
layout: post
title: New Zend certification - Zend Certified PHP Developer
---

### The first batch of ZCPD (Zend Certified PHP Developer) exam

#### First things first
__Zend Certified PHP Developer__, is the new version of __Zend Certified Engineer__ exam based on PHP 5.5

#### The old exams
Every PHP developer that has already been submitted to the older versions of the exam, notice that all the ZCE exams have almost the same structure:

* Questions about PHP.ini
* Questions about array
* Questions about String
* Questions about MySQL extensions
* Questions about XML
* Questions about streams

And all of this follow almost the same examples of question below:

* Open question

```
What's the name of the function to search a key in a given array?

_________________________________

```

* Single/Multiple choice

```
How should be a XML file? (choose 2)

[ ] Well formed
[ ] Valid
[ ] Should have a DTD
[ ] Should have a validator
[ ] All above
```

It's kind anoying since the questions are not really related to a _PHP developer daily job_, but with a _Study Book/Guide_ to the exam actually.

There are some challenging questions as well about _security_, _code analysis_, even _Spl_ ... but they are not enought compared to questions like the example.

#### First impressions

Once you start the _new_ exam, you can slightly feel the diference related to the questions...

Now, the questions are __PHP developer daily bases__ questions... they are more logic, challenging, and not only about PHP.

We are talking about a real __PHP Engineer__ exam (and now, they remove the engineer from the name), we are talking about an exam that covers all the PHP ecosystem.

Questions about: 
* PHP.ini
* The language by it self
* DOM
* Infrastructure
* HTTP
* Database in general
* OOP - Yes Object Oriented PROGRAMMING!
* Design Patterns

As you can see, now the exam can cover since _String operators_, going through DOM manipulation to an Observer Pattern... and that is exactly what happens!

#### Is the exam getting __seniority__ as the PHP developers are?

When you open your exam, you will still getting questions as:
```
Which function can be used to get the length of a given string?

(a) string_length
(b) strlength
(c) strlen
(d) String.length
(e) None of above
```

But, as expected this is just to make you confortable with the exam... Zend don't want people getting affraid and going out of the exam room screaming.
Well, jokes aside, the quality of the exam has improved __A LOT__.

Now, the developer will find questions that will make him spend the clock time to answer...
For some people, that really use PHP as your daily tool, it can be an easy thing... but for new developers, it is a huge challenge and a huge knowledge to get!

Sample:

```
Which Spl interface can be used alongside with SplObserver to implement the Observer Pattern?

________________________

```

And as you can see, it's an Open question... no Options to guess!

E can get more complex samples, as code samples:

```php
Which classes should be declared as abstract?

class A extends D {
 public function myFunctionY() {}
}

class B {
 public abstract function myFunctionY();
}

class C extends B {
 public function myFunctionZ() {}
}

class D extends B  {
 public function myFunctionX() {}
}

(a) A,B,C,D
(b) B,C,D
(c) C,D
(d) B,D
(e) B
```

As I said, for a Senior PHP developer, the answer is obvious... in this case, the developer really need to know OOP, and that's a kind of tricky question of the exam.

Even tricks based on the new version of the PHP, 5.5

```php
What's the output of the following code.

<?php
namespace MyAwesomeFramework\MyAwesomeExceptions;

class MyException(){ 
	public function getMessage() {
		return self::class;
	}
}

function inverse($x) {
    if ( ! $x) {
        throw new Exception('Division by zero.');
    }
    return 1/$x;
}

try {
    echo inverse(0) . "\n";
} catch (Exception $e) {
    echo 'Caught exception: ',  $e->getMessage(), "\n";
} catch (MyException $e) {
    echo 'Caught exception: ',  $e->getMessage(), "\n";
} finally {
    echo "First finally.\n";
}

(a) Caught exception: Exception First finaly
(b) Caught exception: MyException First finaly
(c) Caught exception: MyAwesomeFramework\MyAwesomeExceptions\MyException First finaly
(d) Caught exception: First finaly
(e) Fatal error
```

And it's just the beginning of the exam.

#### Ok, what's the content of the exam?

The exam covers the following contents:


__ PHP Basics__

* Operators
* Variables
* Control Structures
* Language Constructs and Functions
* Namespaces
* Extensions
* Config
* Performance/bytecode caching


__Functions__

* Arguments
* Variables
* References
* Returns
* Variable Scope
* Anonymous Functions, closures


__Data format and Types__

* XML Basics
* SimpleXML
* XML Extension
* Webservices Basics
* SOAP
* JSON
* DateTime
* DOMDocument


__Web Features__

* Sessions
* Forms
* GET and POST data
* Cookies
* HTTP Headers
* HTTP Authentication
* HTTP Status Codes *


__I/O__

* Files
* Reading
* Writing
* File System Functions
* Streams
* Contexts


__Object oriented programming__

* Instantiation
* Modifiers/Inheritance
* Interfaces
* Exceptions
* Autoload
* Reflection
* Type Hinting
* Class Constants
* Late Static Binding
* Magic (_*) Methods
* Instance Methods & Properties
* SPL
* Traits


__Security__

* Configuration
* Session Security
* Cross-Site Scripting
* Cross-Site Request Forgeries
* SQL Injection
* Remote Code Injection
* Email Injection
* Filter Input
* Escape Output
* Encryption, Hashing algorithms
* File uploads
* PHP Configuration
* Password hashing API


__String and patterns__

* Quoting
* Matching
* Extracting
* Searching
* Replacing
* Formatting
* PCRE
* NOWDOC
* Encodings


__Databases and SQL__

* SQL
* Joins
* Prepared Statements
* Transactions
* PDO


__Arrays__

* Associative Arrays
* Array Iteration
* Array Functions
* SPL, Objects as arrays
* Casting

```
As you can see, it's almost the same table of contents of version 5.3.
The differences are: The quality of questions
```

#### PHP 5.5, your features

The features are the moast important thing, since the exam is based on PHP 5.5.
But, in general they are not too much compared to the whole php context and ecosystem at all, covered by the exam.

So, let's talk about the new features.

###### Finally

Finally allows developers run code at the end of try and catch blocks, regardless of whether an exception was thrown or not, before the normal execution flow resumes.

Without the finally keyword, developers were sometimes be forced to repeat code within both the try and catch blocks to handle cleanup tasks. For example:
```php
<?php
function someDbOperation() {
    $resource = mysqli(/* ... */);
    try {
        $result = getSomeResult($resource, /* ... */);

        mysqli_close($resource);

        return $result;
    }
    catch (Exception $e) {
    	mysqli_close($resource);

        log($e->getMessage());

        throw $e;
    }
}
```
With the finally keywork, we can eliminate the duplicated code:
```php
function someDbOperation() {
    $resource = mysqli(/* ... */);
    try {
        $result = getSomeResult($resource, /* ... */);

        return $result;
    }
    catch (Exception $e) {
        log($e->getMessage());

        throw $e;
    } finally {
    	mysqli_close($resource);
    }
}
```

###### Array and String Dereferencing
Array and string can be dereferenced using array access syntax:
```php
<?php
// array dereferencing
echo ["Manolo", "Que", "Irado"][0]; // "Manolo"
 
// string dereferencing
echo "Manolo"[3]; // "n"

// Some cool stuff
echo ":;!@#$%^&*()abcdefshijkm"[mt_rand(0, 16)];
```

###### Generators
Generators are one of the most expected new features. They provide a way to _iterate_, without having to write a class implementing the Iterator interface. Implement the Iterator interface requires a substantial amount of boilerplate code; to be able to avoid this, generators can significantly reduce the size and complexity of code.

__A generator is much like a function, but instead of returning a single value, a generator can produce any number of values​ with the ​_yield_ keyword.__

Sample:
```php
<?php
function xrange($start, $end) {
    for ($i = $start; $i < $end; $i ++) {
        yield $i;
    }
}

foreach (xrange(0, 666666) as $number) {
	echo $number.PHP_EOL;
}
```

###### Class Name Resolution
Since PHP 5.3 and __namespaces__, it's common to use extensive and descritive namespaces to organize the code.
And with this, we increased the difficult to get a full-qualified class name as a String.
```php
<?php
use MyAwesomeNamespace\MyAwesomeClass;
 
$reflection = new \ReflectionClass(MyAwesomeClass::class); // Simple!
```

###### Password Hashing
Password hashing API is one of the most important and useful features of PHP 5.5.

The API introduces two new functions, __password_hash()__ and __password_verify()__.

Calling __password_hash($password, PASSWORD_DEFAULT)__ will give you a hash using bcrypt and salting handled automatically. Verifying the password is easy as checking the result of __password_verify($password, $hash)__.

The API uses bcrypt by default, but new algorithms may be introduced to provide even more secure methods of hashing. Developers can specify their own bcrypt work factor to adjust the strength of the hashes produced, and can also use their own salts instead of the automatic salt generation (the manual discourages this).

###### empty
Now, the __empty__ construct can be used with function calls and expressions
```php
empty( myFunction() );
empty( $object->someMethod() );
```

###### foreach
Now, it's possible to use the _list_ constructor with a foreach loop
```php
$userList = [
	["Manolo", "Developer"],
	["Manola", "Project Manager"]
];

foreach ($userList as list($name, $position)) {
	echo "{$name} is a {$position}".PHP_EOL;
}
```

And that's are the moast significant improvements of the 5.5 versions.

###### Where are all the possible new features?
You can check this two links:

* [PHP 5.5 Features ](http://php.net/manual/en/migration55.new-features.php "PHP 5.5. Features")
* [PHP 5.5 Functions ](http://php.net/manual/en/migration55.new-functions.php "PHP 5.5. Functions")

#### Conclusions... conclusions ?

No! Bullets.


###### The exam

* The exam changes were substantially necessary to give more quality professionals to the IT market
* PHP is not only a programming language, it's a complete ecosystem with Security, Infrastructure, Storage, DOM, Patterns and the other 100000 PHP related subjects
* Developer should be challenged within logical questions
* That's a __must do__ exam to all PHP developers!
* It reflects a PHP developer's daily basis routine
* In the end, it is a personal satisfaction that has no description

###### PHP 5.5

* As any other PHP versions, the improvements are huge
* As any other PHP versions, the improvements help the code development a lot
* PHP 5.5 introduced an awesome Password Hashing API
* Generators came to be your best friend
* Array/String dereferencing came to make the code even more lean
* Yes... we do have some news for GD library... but it doesn't even matter when we do have new cURL and Sockets functions