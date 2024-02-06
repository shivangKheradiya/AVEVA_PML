# 5. ERROR HANDLING & BRANCHING

Run the following command in the command window to test some codes mentioned in the page.

```
SHOW !!RUNMACRO
```

## 5.1 ERROR HANDLING

Basic Syntax for Error Handaling is as follows,

```
NEW PIPE -- come code Which you feel may cause error
HANDLE (41, 8) 
 $p Need to be at a ZONE or below 
ELSEHANDLE (41, 12) 
 $p That name has already been used. Names must be unique 
ELSEHANDLE ANY 
 $p Another error has occurred 
ELSEHANDLE NONE 
 $p Everything OK. PIPE created 
ENDHANDLE
```

Select Empty Site in design moduel and run following commands,
Input
```
NEW PIPE
HANDLE (41, 8) 
 $p Error: Need to be at a ZONE or below 
ELSEHANDLE (41, 12) 
 $p Error: That name has already been used. Names must be unique 
ELSEHANDLE ANY 
 $p Error: Another error has occurred 
ELSEHANDLE NONE 
 $p Everything OK. PIPE created 
ENDHANDLE

$P Let's Create Zone And Remove Error
NEW ZONE
HANDLE ANY
  $p Error: Zone Can't be Created 
ELSEHANDLE NONE 
  $p Everything OK. ZONE created 
ENDHANDLE

NEW PIPE /MyPipe
HANDLE (41, 8) 
 $p Error: Need to be at a ZONE or below 
ELSEHANDLE (41, 12) 
 $p Error: That name has already been used. Names must be unique 
ELSEHANDLE ANY 
 $p Error: Another error has occurred 
ELSEHANDLE NONE 
 $p Everything OK. PIPE created 
ENDHANDLE

$P Let's Create One More Pipe having same name
NEW PIPE /MyPipe
HANDLE (41, 8) 
 $p Error: Need to be at a ZONE or below 
ELSEHANDLE (41, 12) 
 $p Error: That name has already been used. Names must be unique 
ELSEHANDLE ANY 
 $p Error: Another error has occurred 
ELSEHANDLE NONE 
 $p Everything OK. PIPE created 
ENDHANDLE
```

Output
```
Error: Need to be at a ZONE or below
Let's Create Zone And Remove Error
Everything OK. ZONE created
Everything OK. PIPE created
Let's Create One More Pipe having same name
Error: That name has already been used. Names must be unique
```

In Case Selected Site is not having write access, Output will be as follows
```
Error: Need to be at a ZONE or below
Let's Create Zone And Remove Error
Error: Zone Can't be Created
Error: Need to be at a ZONE or below
Let's Create One More Pipe having same name
Error: Need to be at a ZONE or below
```

## 5.2 BRANCHING

### 5.2.1 GOLABEL

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

In Above Exaple GoLable is triggred withing if condition and it's breaking the do look. GoLable statement can be used with individual Loop code & If else block as well.  