# 4. LOOPS

Run the following command in the command window to test some codes mentioned in the page.

```
SHOW !!RUNMACRO
```

## 4.1 DO

### 4.1.1 DO BREAK

Input
```
!value = 1
do
  if(!value.gt(5)) then
    break
  endif 
  q var !value
  !value = !value + 1
enddo
```

Output
```
<REAL> 1

<REAL> 2

<REAL> 3

<REAL> 4

<REAL> 5
```

### 4.1.2 DO BREAK IF

Input
```
!value = 1
do
  break if(!value.gt(5))
  q var !value
  !value = !value + 1
enddo
```

Output
```
<REAL> 1

<REAL> 2

<REAL> 3

<REAL> 4

<REAL> 5
```

### 4.1.3 DO TO

Input
```
do !int to 5
  q var !int  
enddo
```

Output
```
<REAL> 1

<REAL> 2

<REAL> 3

<REAL> 4

<REAL> 5
```

### 4.1.4 DO FROM TO

Input
```
do !int from 5 to 10
  q var !int
enddo
```

Output
```
<REAL> 5

<REAL> 6

<REAL> 7

<REAL> 8

<REAL> 9

<REAL> 10
```

### 4.1.5 DO SKIF IF

Input
```
do !int from 5 to 10
  skip if (!int.eq(7))
  q var !int
enddo
```

Output
```
<REAL> 5

<REAL> 6

<REAL> 8

<REAL> 9

<REAL> 10
```

### 4.1.6 DO FROM TO BY

Input
```
do !int from 5 to 10 BY 2
  q var !int
enddo
```

Output
```
<REAL> 5

<REAL> 7

<REAL> 9
```

### 4.1.7 DO INDICES

Input
```
!X[1] = 5
!X[3] = 6
!X[4] = 8

do !idx indices !X
  q var !idx
enddo
```

Output
```
<REAL> 1

<REAL> 3

<REAL> 4
```

### 4.1.8 DO INDEX

Input
```
!X[1] = 5
!X[3] = 6
!X[4] = 8

do !idx index !X
  q var !idx
enddo
```

Output
```
<REAL> 1

<REAL> 3

<REAL> 4
```

### 4.1.9 DO VALUE

Input
```
!X[1] = 5
!X[3] = 6
!X[4] = 8

do !val values !X
  q var !val
enddo
```

Output
```
<REAL> 5

<REAL> 6

<REAL> 8
```

### 4.1.10 DO GOLABLE

This topic is a part of conditional branching as well.

Input
```
!X[1] = 5
!X[3] = 6
!X[4] = 8

do !idx indices !X
  q var !idx
  if (!idx.eq(3)) then
    golabel /LetsFinishLoop
  endif
enddo
label /LetsFinishLoop
$p index 4 is printed outside loop
```

Output
```
<REAL> 1

<REAL> 3
4 is printed outside loop
```