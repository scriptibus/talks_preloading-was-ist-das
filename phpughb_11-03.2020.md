# Was ist Preloading 
### Und wie funktioniert das?

---

# Wie wird PHP-Code ausgeführt?
1. Lexing
2. Parsing
3. Compilation
4. Interpretation

--- 

# Lexing oder Tokenizing
## Verwandelt einen Code-String zu eine Token-Stream
  
```php
<?php

// Code-String
$code = '<?php $a = 1 ?>';

// Holen der Tokens
$tokens = token_get_all($code);

foreach ($tokens as $token) {
    if (is_array($token)) {
        echo "Line {$token[2]}: ", token_name($token[0]), " ('{$token[1]}')", PHP_EOL;
    } else {
        var_dump($token);
    }
}
```

---

# PHP-Code
```php
<?php $a = 1 ?>
```

# Token-Stream
```
Line 1: T_OPEN_TAG ('<?php ')
Line 1: T_VARIABLE ('$a')
Line 1: T_WHITESPACE (' ')
string(1) "="
Line 1: T_WHITESPACE (' ')
Line 1: T_LNUMBER ('1')
Line 1: T_WHITESPACE (' ')
Line 1: T_CLOSE_TAG ('?>')
```