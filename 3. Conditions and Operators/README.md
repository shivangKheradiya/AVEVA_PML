# 3. CONDITIONS AND OPERATORS

Run the following command in the command window to test the codes mentioned in the page.

`SHOW !!RUNMACRO`

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

### 3.1.2 If Else

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

### 3.1.3 If ElseIf

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


