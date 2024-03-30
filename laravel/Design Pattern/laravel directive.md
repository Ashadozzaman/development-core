## laravel directive

In Laravel, directives are special instructions or shortcuts provided by the Blade templating engine.
Directives in Blade are preceded by the @ symbol and provide functionality such as including subviews, looping through data, conditionally displaying content, extending layouts, and more.

1. `Define the Custom Directive:`
Within your service provider's boot() method, use the `Blade::directive()` method to define your custom directive. The method takes two parameters: the directive name and a callback function that returns the PHP code to be executed when the directive is encountered.

```
use Illuminate\Support\Facades\Blade;

public function boot()
{
    Blade::directive('uppercase', function ($expression) {
        return "<?php echo strtoupper({$expression}); ?>";
    });
}

```