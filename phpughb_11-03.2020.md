# Was ist Preloading 
### Und wie funktioniert das?

---

# Wie wird PHP-Code ausgeführt?
1. Lexing
2. Parsing
3. Compilation
4. Interpretation

--- 
^ 
- Code String zu Token Stream
- In späterem Abschnitt verwendet

# Lexing oder Tokenizing
## Verwandelt einen Code-String zu eine Token-Stream
```php
<?php

$code = '<?php $a = 1 ?>';

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
^
- Manche Zeichen sind Tokens
- Beispiel ; : ? =

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

---
^
- Ist das Skript logisch?
- Baumartige Darstellung des Programmcodes

# Parsing
1. Grammatik Check (Validierung)
2. Bauen des AST (Abstract Syntax Tree)
   
```php
<?php

$code = <<<'EOL'
<?php 
    $a = 1;
EOL;

print_r(ast\parse_code($code, 70));
```

---
^
- 132 = Statement List
- Line 1

# AST
```php
ast\Node Object
(
    [kind] => 132
    [flags] => 0
    [lineno] => 1
    [children] => Array(
       
       













       
    )
)
```

---
^
- 517 = Assignment
- Line 2

# AST
```php
ast\Node Object
(
    [kind] => 132
    [flags] => 0
    [lineno] => 1
    [children] => Array(
        [0] => ast\Node Object(
        [kind] => 517
        [flags] => 0
        [lineno] => 2
        [children] => Array(








            [expr] => 1
        )
        )
    )
)
```

---
^
- 256 = Variable
- Line 2
- Wert "a"

# AST
```php
ast\Node Object
(
    [kind] => 132
    [flags] => 0
    [lineno] => 1
    [children] => Array(
        [0] => ast\Node Object(
        [kind] => 517
        [flags] => 0
        [lineno] => 1
        [children] => Array(
            [var] => ast\Node Object(
                [kind] => 256
                [flags] => 0
                [lineno] => 2
                [children] => Array(
                    [name] => a
                )
            )
            [expr] => 1
        )
        )
    )
)
```