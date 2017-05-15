[Back to Home](README)
# GENERAL RULES

While many of best practices and rules are bound to a certain technology or language, there are some that apply pretty much everywhere.

## Naming system

Names of variables, classes, properties and functions have to make a sense, self-explanatory code is much easier to read than having variables like `$tmp1`, `$foo`, `$asd` etc. In general you should stick to this rule as much as you can but sometimes exceptions come into play as showcased in next rule.

## Consistent temporary names

Normally, the variables should be descriptive and contain one or more words. But, this doesn't necessarily apply to temporary variables. They can be as short as a single character.

It is a good practice to use consistent names for your temporary variables that have the same kind of role. Here are a few examples:

```php
<?php
// $i for loop counters
for ($i = 0; $i < 100; $i++) {
    // $j for the nested loop counters
    for ($j = 0; $j < 100; $j++) {

    }
}

// $k and $v in foreach
foreach ($some_array as $k => $v) {

}

// $q for SQL queries
$q = $this->getDoctrine()
          ->getRepository('ExampleBundle:User')
          ->createQueryBuilder('u')
          ->where('u.type = :type')
          ->setParameter('type', 'admin');

// $fp for file pointers
$fp = fopen('file.txt','w');
```

NOTE: this is just an example - you can freely use $a / $b / $c ... (or any other logical form) for loop counters, as long as it is used consistently.

## Consistent indentation

While indentation style may vary from language to language, always stick to one style per language / file type.

Practical Example of good indentation can be found [here](PHP#markdown-header-example) (applicable for PHP files).

## Avoid obvious comments

Commenting your code is fantastic; however, it can be overdone or just be plain redundant, as in following example:

```php
<?php
// get the country code
$country_code = get_country_code($_SERVER['REMOTE_ADDR']);

// if country code is US
if ($country_code == 'US') {
    // display the form input for state
    echo form_input_state();
}
```

## Group your code
More often than not, certain tasks require a few lines of code. It is a good idea to keep these tasks within separate blocks of code, with a space (or more spaces) between them. Adding a comment at the beginning of each block of code also emphasizes the visual separation.

```javascript
// setting default Messenger plugin options
Messenger.options = {
    extraClasses: 'messenger-fixed messenger-on-bottom messenger-on-right',
    theme: 'flat',
    messageDefaults: {
        hideAfter: 5,
        showCloseButton: true
    }
};

// adding custom validation method if validator plugin is loaded
if($.validator){
    $.validator.addMethod(
        "regex",
        function(_value, _element, _regexp) {
            var regExpObject = new RegExp(_regexp);
            return this.optional(_element) || regExpObject.test(_value);
        },
        "Please check your input."
    );
}
```

## DRY principle
DRY stands for *Don't repeat yourself*, it is also known as DIE ("Duplication is Evil"). DRY principle states that:

> Every piece of knowledge must have a single, unambiguous, authoritative representation within a system

When the DRY principle is applied successfully, a modification of any single element of a system does not require a change in other logically unrelated elements. Additionally, elements that are logically related all change predictably and uniformly, and are thus kept in sync.

To put it simply - if you are copy-pasting parts of your code without making any modifications to them, you are most likely breaking this rule.
