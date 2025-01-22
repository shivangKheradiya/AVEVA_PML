# 8. Functions

Instade of using macros, It's always desirable to define the functions.

- Functions are stored typically within `pmllib` directory with `.pmlfnc` Extension.

- Function Name and File name must match.

## 8.1 Functions with No Return Type (Procedures)

Procedures doesn't have any type of retun value. It's similar to `void` in C#. But it's possible to have some arguement in Procedures.

Below is an example for the procedure with no input Arguments. Store below file within any `pmllib` directory and run `pml rehash all` command.

```
define function !!CEANDMEM()

    q ce
    q mem

endfunction
``` 

Input
```
-- Select any Element
!!CEANDMEM()
```

Below is an example for the procedure has one input Argument (Name).
```
define function !!CERENAME(!name is string)

    !!ce.name = !name

endfunction
``` 

Input
```
-- Select any Element
!!cerename(|/NewName|)
```

## 8.2 Functions with Return Types

It's possible to get desired form of retun value from the functions.

Below example of function returns an array represents the members of current element.

```
define function !!CEMEM() is ARRAY

    return !!ce.mem

endfunction
``` 

Input
```
-- Select any Element
q var !!CEMEM()
```

Below example of function returns an volume if box.
```
define function !!BOXVOLUME() is REAL

    if (!!ce.type.eq(|BOX|)) then
        return ( !!ce.Xlen * !!ce.ylen * !!ce.zlen )
    endif

    return 0

endfunction
``` 

Input
```
-- Select Box Element
q var !!BOXVOLUME()
```