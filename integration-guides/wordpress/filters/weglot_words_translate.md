# weglot\_words\_translate

{% hint style="info" %}
Since : 1.12
{% endhint %}

```php
<?php// File wp-content/themes/myTheme/functions.php​add_filter('weglot_words_translate', 'words_translate');​function words_translate($words){        $words[] = "Monday";       $words[] = "Tuesday";    $words[] = "Nice to meet you";           return $words;}
```

