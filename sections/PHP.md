[Back to Home](../README.md)
# PHP

## Overview

Base for PHP guidelines is taken from [PSR-2 coding standards](http://www.php-fig.org/psr/psr-2), so if you are already familiar with those you should be golden here. You don’t have to adhere to every single rule necessarily but there are few we would like to highlight as important.
Keep in mind that some rules, especially for commenting, are not “written in the stone” and can be subject to a change based on framework and/or tools used.

## File manifest

1. Files are *UTF-8 without BOM*
1. *4 spaces* are used for indenting, *not tabs*
1. Files use *unix LF line ending*
1. Files are using only `<?php` and `<?=` opening tags
1. *One* file contains only *one* class or interface or trait
1. Namespaces and classes are following “autoloading” PSR

## Class naming and code structure

1. Class names are *PascalCase*
1. Method names, property names and variable names are *camelCase*
1. Constants are upper *SNAKE_CASE*
1. PHP keywords and constants (`true`, `false`, `null`) are in *lower case*
1. Method names contain *verb*

## Code structure for increased readability

1. *one* statement = *one* line of code
1. There is a blank line after namespace and block of use declarations
1. Opening braces for class and method go on the next line
1. Closing braces for class and method go on the next line after the body
1. Opening braces for control structures (if, for, foreach...) go on the same line
1. Closing braces for control structures go on the next line after the body
1. Opening parentheses for control structures don’t have a space after them
1. Closing parentheses for control structures don’t have a space before
1. Control structure keywords have a space after them, method and function calls do not
1. There is one space between the closing parenthesis and the opening brace for control structures
1. The structure body is indented once
1. Blank lines may be added to improve readability and to indicate related blocks of code

## Classes, Properties and Methods

1. The `extends` and `implements` keywords are declared on the same line as the class name
1. Lists of `implements` may be split across multiple lines, where each subsequent line is indented once. When doing so, the first item in the list is on the next line, and there is only one interface per line
1. Visibility is declared on all properties and method
1. `var` keyword MUST NOT be used to declare a property
1. Method names are declared with a space after the method name
1. In the argument list, there is NO space before each comma, and there is ONE space after each comma
1. Method arguments with default values go at the end of the argument list
1. Argument lists MAY be split across multiple lines, where each subsequent line is indented once. When doing so, the first item in the list is on the next line, and there is only one argument per line. When the argument list is split across multiple lines, the closing parenthesis and opening brace are placed together on their own line with one space between them.
1. When present, the `abstract` and `final` declarations precede the visibility declaration.
1. When present, the `static` declaration come after the visibility declaration.

## Best practices for comments

1. In switch structure there must be a comment such as `// no break` when fall-through is intentional in a non-empty case body
1. Method comments are descriptive and use `@param` and `@return` - optionally also `@throws` and `@see`
1. Class comments use `@package` - optionally `@version`, `@author`, `@license`, `@copyright`, `@link` (this a very broad subject and it can depend on a documentation tool used)

## Example

We will showcase a simple class _Car_, showing application of aforementioned rules. For more examples search for PSR coding standards [PSR-2](PSR-2).

```php
<?php

/**
* Part of the Acme package.
*
* NOTICE OF LICENSE
*
* DO WHAT THE FCUK YOU WANT TO PUBLIC LICENSE
* Version 2, December 2004
*
* Everyone is permitted to copy and distribute verbatim or modified
* copies of this license document, and changing it is allowed as long
* as the name is changed.
*
* DO WHAT THE FCUK YOU WANT TO PUBLIC LICENSE
* TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION
*
* @package    Acme
* @version    1.0.0
* @author     Sleighdogs GMBH
* @license    WTFPL
* @link       http://sld.gs
*/

namespace Acme\Models;

use Acme\Interfaces\VehicleInterface;
use Exception;

class Car extends Vehicle implements VehicleInterface
{

   /**
    * @var  Number of doors in sedan type
    */
   const SEDAN_DOOR_COUNT = 4;

   /**
    * Basic color code hash map
    * @var array
    */
   private static $basicColors = [
       'red'   => '#FF0000',
       'blue'  => '#0000FF',
       'green' => '#00FF00',
       'black' => '#000000',
       'white' => '#FFFFFF'
   ];

   /**
    * Chassis number
    * @var string
    */
   private $chassisNumber;

   /**
    * Human readable representation of a color
    * @var string
    */
   protected $color;

   /**
    * Car type
    * @var string
    */
   protected $type;

   /**
    * Manufacturer object
    * @var Acme\Models\Manufacturer
    */
   protected $manufacturer;

   /**
    * License plate
    * @var string
    */
   public $vehicleRegistrationPlate;

   /**
    * @param Manufacturer $manufacturer             Car manufacturer
    * @param string       $color                    Car color
    * @param string       $vehicleRegistrationPlate License plate
    * @param string       $chassisNumber            Car chassis number
    */
   public function __construct(
       Manufacturer $manufacturer,
       $color = null,
       $vehicleRegistrationPlate = null,
       $chassisNumber = null
   ) {
       $this->manufacturer = $manufacturer;

       $this->color = $color;

       $this->vehicleRegistrationPlate = $vehicleRegistrationPlate;

       $this->chassisNumber = $chassisNumber;
   }

   /**
    * Human readable color of a car
    * @return string
    */
   public function getColor()
   {
       return $this->color;
   }

   /**
    * Check if car is in certain color
    * @return boolean
    */
   public function isInColor($color, $includeHexValues)
   {
       if ($includeHexValues) {
           return $this->color === $color || (isset(self::$basicColors[$this->color]) && self::$basicColors[$this->color] === $color);
       } else {
           return $this->color === $color;
       }
   }

   /**
    * Shorthand function for hex color code of a car
    * @return string Color hex code (f.e. #FF0000)
    */
   public function getColorCode()
   {
       return self::getColorCodeStatic($this->color);
   }

   /**
    * Hex color code of a car
    * @see    self::$basicColors Available car colors
    * @throws Exception          Throws exceptions if color is not defined or not recognized
    * @param  string $color      Color name
    * @return string             Color hex code (f.e. #FF0000)
    */
   public static function getColorCodeStatic($color)
   {
       // Color is empty
       if (empty($color))
           throw new Exception('Undefined color');

       // Color is not in the array of acceptable colors
       if (!isset(self::$basicColors[$color]))
           throw new Exception('Unrecognizable color');

       return self::$basicColors[$color];
   }

   /**
    * Number of doors in a car
    * @return integer door count
    */
   public function getDoorCount()
   {
       $count = -1;
       $type = strtolower($this->type);

       switch (true) {
           case $type == 'sedan':
               $count = self::SEDAN_DOOR_COUNT;
               break;
           case $type == 'coupe':
               // no break
           case $type == 'convertible':
               $count = 2;
               break;
           case $type == 'combi':
               $count = 5;
               break;
       }

       if ($count == -1)
           throw new Exception('Unrecognizable car type');

       return $count;
   }

   /**
    * Returns the string representation of the Car object
    * @return string
    */
   public function __toString()
   {
       return (string) print_r(
           [
               'motorized?'     => $this->isMotorized() ? 'yes' : 'no',
               'color'          => $this->color,
               'license plate'  => $this->vehicleRegistrationPlate,
               'chassis number' => $this->chassisNumber,
               'door count'     => $this->getDoorCount()
           ],
           true
       );
   }

}

```
