# 9. Objects

PML Objects are similar to the classes defined in the `C#` language. PML Objects can have constructor and Classes can hold methods defination as well. It's possible to impliment more object oriented concept using PML objects.

- PML Objects should be stored within `PMLLIB` directory ( with extension `.pmlobj`) similar to the functions.
- PML Object Name and File Name must match.
- PML Object will have default constructor (method) with the same name of the object.

Syntax
```
define object FileName
    member .StringMember is String
    member .RealMember   is Real
    member .BoolMember   is Boolean
    member .ArrayMember  is Array
endobject

-- Default Constructor
define method .FileName()
endmethod

-- Method A
define method .ObjectMethodA()
    q var !this.RealMember
endmethod

-- Method B
define method .ObjectMethodB()
endmethod
```

Above Syntax basically indicates below points,
- FileName should be replaced with the name of the file.
- File must be stored within `PMLLIB` directory with (`.pmlobj`) extension.
- FileName Should not contain any space or special Characters.
- Default constructure is a method has name same as name of the file.
- Object can have more than one methods or No methods.
- Members described within any Object defination block are also object e.g. StringMember is String object type. Similartly any other custom object can be a member within any Object defination block.
- Members Can be Accessed within the Objects as well as the location where the Instance of the object is created. 

Below is the use case for above described object,
```
!FileNameObj = object FileName()
q var !FileNameObj.StringMember
q var !FileNameObj.RealMember
q var !FileNameObj.BoolMember
q var !FileNameObj.ArrayMember

-- Value Assignment in the object
!FileNameObj.StringMember = |This is FileName Object|
!FileNameObj.RealMember = 100
!FileNameObj.BoolMember = FALSE
!FileNameObj.ArrayMember[1] = |First Array Object|

q var !FileNameObj.StringMember
q var !FileNameObj.RealMember
q var !FileNameObj.BoolMember
q var !FileNameObj.ArrayMember

-- Use Case For the Methods
!FileNameObj.ObjectMethodA()
```

Forms, Classes Defined in .Net, AVEVA InBuilt Data Types, System Defined Data Types or Object Types are considered as an object.

Methods To know Object type of the Variable or Object,
- Whenever any variable is queried using `Q var !varName`, then in the output will be starting like `<ObjecType>`.
- A Query Syntax can be used `q var !varName.ObjectType()`. Output will give the object type of the variable as `<STRING>` 