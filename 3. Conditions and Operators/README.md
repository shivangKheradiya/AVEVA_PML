# 3. CONDITIONS AND OPERATORS

Run the following command in the command window to test some codes mentioned in the page.

```
SHOW !!RUNMACRO
```

## 3.1 Conditions (Iftrue, If, If Else, If ElseIf)

### 3.1.1 Iftrue

Input:
```
!x = iftrue( 3 equal 5 , 3 , 5 ) 
q var !x

!x = iftrue( 3 equal 3 , 3 , 5 ) 
q var !x
```
Output:
```
<REAL> 5

<REAL> 3
```

### 3.1.2 If

Input:
```
if ( 3 equal 3 ) then
    $P 3 equal to 3
endif
```
Output:
```
3 equal 3
```

### 3.1.3 If Else

Example 1:

Input:
```
if ( 3 equal 3 ) then
    $P 3 equal to 3
else
    $P 3 is not equal to 5
endif
```
Output:
```
3 equal to 3
```

Example 2:

Input:
```
if ( 3 equal 5 ) then
    $P 3 equal to 3
else
    $P 3 is not equal to 5
endif
```
Output:
```
3 is not equal to 5
```

### 3.1.4 If ElseIf

Example 1:

Input:
```
if ( 3 equal 3 ) then
    $P 3 equal to 3
elseIf( 5 equal 5 ) then
    $P 5 equal to 5
else
    $P 3 is not equal to 5
endif
```
Output:
```
3 equal to 3
```

Example 2:

Input:
```
if ( 3 equal 5 ) then
    $P 3 equal to 3
elseIf( 5 equal 5 ) then
    $P 5 equal to 5
else
    $P 3 is not equal to 5
endif
```
Output:
```
5 equal to 5
```

Example 3:

Input:
```
if ( 3 equal 5 ) then
    $P 3 equal to 3
elseIf( 5 equal 3 ) then
    $P 5 equal to 5
else
    $P 3 is not equal to 5
endif
```
Output:
```
3 is not equal to 5
```

## 3.2 Operators

Input:
```
!X = 5
!Y = 5
!Z = 6
!T = TRUE
!F = FALSE
```

### 3.2.1 Comparator Operators

|**Description**      |**PML 1**            |**PML 2**            |
|---------------------|---------------------|---------------------|
|**Equal**            | EQ                  | .EQ()               |
|Input                | `Q ( !X EQ !Y )    `| `Q VAR !X.EQ(!Z)   `|
|Output               | `true              `| `<BOOLEAN> FALSE   `|
|**NOT EQUAL**        | NEQ                 | .NEQ()              |
|Input                | `Q ( !X NEQ !Y )   `| `Q VAR !X.NEQ(!Z)  `|
|Output               | `false             `| `<BOOLEAN> TRUE    `|
|**LESS THAN**        | LT                  | .LT()               |
|Input                | `Q ( !X LT !Y )    `| `Q VAR !X.LT(!Z)   `|
|Output               | `false             `| `<BOOLEAN> TRUE    `|
|**LESS OR EQUAL**    | LE                  | .LEQ()              |
|Input                | `Q ( !X LE !Y )    `| `Q VAR !X.LEQ(!Z)  `|
|Output               | `true              `| `<BOOLEAN> TRUE    `|
|**GREATER THAN**     | GT                  | .GT()               |
|Input                | `Q ( !X GT !Y )    `| `Q VAR !X.GT(!Z)   `|
|Output               | `false             `| `<BOOLEAN> FALSE   `|
|**GREATER OR EQUAL** | GE                  | .GEQ()              |
|Input                | `Q ( !X GE !Y )    `| `Q VAR !X.GEQ(!Z)  `|
|Output               | `true              `| `<BOOLEAN> FALSE   `|

### 3.2.2 Logical Operators

|**Description**      |**PML 1**            |**PML 2**            |
|---------------------|---------------------|---------------------|
|**OR**               | OR                  | .OR()               |
|Input                | `Q ( !T OR !F )   ` | `Q VAR !T.OR(!F)   `|
|Output               | `true             ` | `<BOOLEAN> TRUE    `|
|**AND**              | AND                 | .AND()              |
|Input                | `Q ( !T AND !F )  ` | `Q VAR !T.AND(!F)  `|
|Output               | `false            ` | `<BOOLEAN> FALSE   `|
|**NOT**              | NOT                 | .NOT()              |
|Input                | `Q ( NOT !T )     ` | `Q VAR !T.NOT()    `|
|Output               | `false            ` | `<BOOLEAN> FALSE   `|

### 3.2.3 Arithmatic Operators

|**Description**      |**PML**              |
|---------------------|---------------------|
|**+**                | +                   |
|Input                | `Q ( !X + !Y )    ` |
|Output               | `10               ` |
|**-**                | -                   |
|Input                | `Q ( !X - !Y )    ` |
|Output               | `0                ` |
|**\***               | *                   |
|Input                | `Q ( !X * !Y )    ` |
|Output               | `25               ` |
|**/**                | /                   |
|Input                | `Q ( !X / !Y )    ` |
|Output               | `1                ` |

### 3.2.4 Concatenation Operators ( & )

Input
```
!concate = !x.string() & !y.string()
q var !concate
```
Output
```
<STRING> '55'
```