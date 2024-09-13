# PHP Static Analysis Attributes

Since the release of PHP 8.0 more and more libraries, frameworks and tools have been updated to use attributes instead of annotations in PHPDocs.

However, static analysis tools like PHPStan or Psalm or IDEs like PhpStorm or VS Code have not made this transition to attributes and they still rely on annotations in PHPDocs for a lot of their functionality.

This library aims to provide a set of PHP attributes which could replace the most commonly used annotations accepted by these tools and will aim to provide related repositories with the extensions or plugins that would allow these attributes to be used in these tools.

In particular, these repositories are:

- [PHP Attributes](https://github.com/php-static-analysis/attributes)
- [PHPStan extension](https://github.com/php-static-analysis/phpstan-extension)
- [Psalm plugin](https://github.com/php-static-analysis/psalm-plugin)
- [RectorPHP rules to migrate annotations to attributes](https://github.com/php-static-analysis/rector-rule)

## Example

In order to show how code would look with these attributes, we can look at the following example. This is how a class looks like with the current annotations:

```php
<?php

class ArrayAdder
{
    /** @var array<string>  */
    private array $result;

    /**
     * @param array<string> $array1 the first array
     * @param array<string> $array2 the second array
     * @return array<string>
     */
    public function addArrays(array $array1, array $array2): array
    {
        $this->result = $array1 + $array2;
        return $this->result;
    }
}
```

And this is how it would look like using the new attributes:

```php
<?php

use PhpStaticAnalysis\Attributes\Type;
use PhpStaticAnalysis\Attributes\Param;
use PhpStaticAnalysis\Attributes\Returns;

class ArrayAdder
{
    #[Type('array<string>')]
    private array $result;

    #[Param(array1: 'array<string>')] // the first array
    #[Param(array2: 'array<string>')] // the second array
    #[Returns('array<string>')]
    public function addArrays(array $array1, array $array2): array
    {
        $this->array = $array1 + $array2;
        return $this->array;
    }
}
```

## List of implemented attributes

These are the available attributes and their corresponding PHPDoc annotations:

| Attribute                                                                                                         | PHPDoc Annotations                   |
|-------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| [Assert](https://github.com/php-static-analysis/attributes/blob/main/doc/Assert.md)                               | `@assert`                            |
| [AssertIfFalse](https://github.com/php-static-analysis/attributes/blob/main/doc/AssertIfFalse.md)                 | `@assert-if-false`                   |
| [AssertIfTrue](https://github.com/php-static-analysis/attributes/blob/main/doc/AssertIfTrue.md)                   | `@assert-if-true`                    |
| [DefineType](https://github.com/php-static-analysis/attributes/blob/main/doc/DefineType.md)                       | `@type`                              |
| [Deprecated](https://github.com/php-static-analysis/attributes/blob/main/doc/Deprecated.md)                       | `@deprecated`                        |
| [Immutable](https://github.com/php-static-analysis/attributes/blob/main/doc/Immutable.md)                         | `@immutable`                         |
| [ImportType](https://github.com/php-static-analysis/attributes/blob/main/doc/ImportType.md)                       | `@import-type`                       |
| [Impure](https://github.com/php-static-analysis/attributes/blob/main/doc/Impure.md)                               | `@impure`                            |
| [Internal](https://github.com/php-static-analysis/attributes/blob/main/doc/Internal.md)                           | `@internal`                          |
| [IsReadOnly](https://github.com/php-static-analysis/attributes/blob/main/doc/IsReadOnly.md)                       | `@readonly`                          |
| [Method](https://github.com/php-static-analysis/attributes/blob/main/doc/Method.md)                               | `@method`                            |
| [Mixin](https://github.com/php-static-analysis/attributes/blob/main/doc/Mixin.md)                                 | `@mixin`                             |
| [Param](https://github.com/php-static-analysis/attributes/blob/main/doc/Param.md)                                 | `@param`                             |
| [ParamOut](https://github.com/php-static-analysis/attributes/blob/main/doc/ParamOut.md)                           | `@param-out`                         |
| [Property](https://github.com/php-static-analysis/attributes/blob/main/doc/Property.md)                           | `@property` `@var`                   |
| [PropertyRead](https://github.com/php-static-analysis/attributes/blob/main/doc/PropertyRead.md)                   | `@property-read`                     |
| [PropertyWrite](https://github.com/php-static-analysis/attributes/blob/main/doc/PropertyWrite.md)                 | `@property-write`                    |
| [Pure](https://github.com/php-static-analysis/attributes/blob/main/doc/Pure.md)                                   | `@pure`                              |
| [RequireExtends](https://github.com/php-static-analysis/attributes/blob/main/doc/RequireExtends.md)               | `@require-extends`                   |
| [RequireImplements](https://github.com/php-static-analysis/attributes/blob/main/doc/RequireImplements.md)         | `@require-implements`                |
| [Returns](https://github.com/php-static-analysis/attributes/blob/main/doc/Returns.md)                             | `@return`                            |
| [SelfOut](https://github.com/php-static-analysis/attributes/blob/main/doc/SelfOut.md)                             | `@self-out` `@this-out`              |
| [Template](https://github.com/php-static-analysis/attributes/blob/main/doc/Template.md)                           | `@template`                          |
| [TemplateContravariant](https://github.com/php-static-analysis/attributes/blob/main/doc/TemplateContravariant.md) | `@template-contravariant`            |
| [TemplateCovariant](https://github.com/php-static-analysis/attributes/blob/main/doc/TemplateCovariant.md)         | `@template-covariant`                |
| [TemplateExtends](https://github.com/php-static-analysis/attributes/blob/main/doc/TemplateExtends.md)             | `@extends` `@template-extends`       |
| [TemplateImplements](https://github.com/php-static-analysis/attributes/blob/main/doc/TemplateImplements.md)       | `@implements` `@template-implements` |
| [TemplateUse](https://github.com/php-static-analysis/attributes/blob/main/doc/TemplateUse.md)                     | `@use` `@template-use`               |
| [Throws](https://github.com/php-static-analysis/attributes/blob/main/doc/Throws.md)                               | `@throws`                            |
| [Type](https://github.com/php-static-analysis/attributes/blob/main/doc/Type.md)                                   | `@var` `@return` `@type`             |

## PhpStorm Support
A plugin that fully supports these attributes will need to be created. Until this is ready you can get partial support by installing PHPStan, our PHPStan extension and enabling PHPStan support in PhpStorm (as described [here](https://www.jetbrains.com/help/phpstorm/using-phpstan.html)). You will then be able to see errors and messages related to these attributes in your code.

Alternatively install Psalm, our Psalm extension and enable Psalm support in PhpStorm (as described [here](https://www.jetbrains.com/help/phpstorm/using-psalm.html))

## VS Code Support
An extension that fully supports these attributes will need to be created. Until this is ready you can get partial support by installing PHPStan, our PHPStan extension and a VS Code extension that supports PHPStan (for example [this one](https://github.com/SanderRonde/phpstan-vscode)). When you enable the extension you will be able to see errors and messages related to these attributes in your code.

Alternatively install Psalm, our Psalm extension and a VS Code extension that supports Psam (for example [this one](https://github.com/psalm/psalm-vscode-plugin))

## Sponsor this project

If you would like to support the development of this project, please consider [sponsoring me](https://github.com/sponsors/carlos-granados)
