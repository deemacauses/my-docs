# Polymorphism vs Abstraction

## Polymorphism

It is important concept in the world of object-oriented programming which refers to the ability to process objects differently based on their data types.
For example, this _Publication_ class defines a set of common behavior that any publication might need.

```php
class Publication {
    public $title;
    public $author;
    public $publish_date;

    public function __construct($title, $author, $publish_date) {
        $this->title = $title;
        $this->author = $author;
        $this->publish_date = $publish_date;
    }

    public function message() {
        return "Title: $this->title By: $this->author $this->publish_date";
    }
}
```

Now let's consider more specific types of publication, like `Blog_Post`:

```php
class Blog_Post extends Publication {
    public function __construct($title, $author, $publish_date, $URL) {
        parent::__construct($title, $author, $publish_date);
        $this->URL = $URL;
    }

    public function message() {
        $blog_post_message = parent::message();
        return "$blog_post_message $this->URL";
    }
}
```

`Blog_Post` use the `extends` clause to extend the general definition of Publication to include additional behavior.

```php
$for_against_let = new Blog_Post(
    "For and Against Let", "Kyle Simpson", "October 27, 2014",
    "https://davidwalsh.name/for-and-against-let"
);

echo $for_gainst_Let->message();
// Title: For and Against Let By: Kyle Simpson October 27, 2014
// https://davidwalsh.name/for-and-against-let
```

Notice that child class instance have `message()` method form the parent Publication class.
This overridden child class `message()` method call `parent::message()` to invoke the inherited version of the `message()` method.

As you can see, we've changed the behavior of the `message()` method by overriding.
So, Both inherited and overridden methods called _polymorphism_.

## Abstraction

It is a concept in which a class has methods without implementation.
The idea is to have a template and let the child class that inherits the parent class implement the method.

```php
abstract class Publication {
    public $title;
    public $author;
    public $publish_date;

    public function __construct($title, $author, $publish_date) {
        $this->title = $title;
        $this->author = $author;
        $this->publish_date = $publish_date;
    }

    // Abstract Method
    public function message();
}
```

```php
class Blog_Post extends Publication {
    public function __construct($title, $author, $publish_date, $URL) {
        parent::__construct($title, $author, $publish_date);
        $this->URL = $URL;
    }

    // Implementing Abstract Method Of Parent Class
    public function message() {
        return "Title: $this->title By: $this->author $this->publish_date";
    }
}
```

```php
$for_against_let = new Blog_Post(
    "For and against let", "Kyle Simpson", "October 27, 2014",
    "https://davidwalsh.name/for-and-against-let"
);

echo $for_against_let->message();
// Title: For and Against Let By: Kyle Simpson October 27, 2014
// https://davidwalsh.name/for-and-against-let
```
