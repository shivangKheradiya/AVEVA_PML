# 7. Macros & Synonyms

## 7.1 Macros

Macros are called as procedures. The most common usecase is to perform certain predefined steps or actions. The steps or the actions required to be performed frequenctly are stored within a text files (with extension .txt, .pmlmac, .mac, No Extension).

Within macro file, it's possible to use functions, Objects, Commands and forms.

It's also possible to define input arguments in the macros. Based on the input values the macro can give the output. These type of macros are called as Parameterised Macro.

Syntax to run macro file
```
$M/PathToMaroFile.mac
```

To create new equipment with given name & Place it to certain position below mentioned pml macro can be used.
```
!NAME = $1
!E = $2
!N = $3
!U = $4

NEW EQUI $!NAME
POSITION E $!E N $!N U $!U
Q POSITION
```

Store the above code in notepad file at any suitable location, and see the output by running below input code.

Input
```
$M/C:\DB\NewEqui.mac |/MyNewEqui| 500 500 500
```

Output
```
Position E 500mm N 500mm U 500mm
```

If the macro file is dragged and drop in the command window than it will give error. Because parameters are not defined. To avoid such situation Below mentioned code syntax used to define default parameters.

Macro Code
```
$D1 = |/MyNewEquipment|
$D2 = 50
$D3 = 50
$D4 = 50

!NAME = $1
!E = $2
!N = $3
!U = $4

NEW EQUI $!NAME
POSITION E $!E N $!N U $!U
Q POSITION
```

Macros may have up to 9 parameters separated by space. If it's required to have sentence like arguement in the input,  $< before and a $> after is used.

Macro Code
```
$D1 = |/MyNewEquipment|
$D2 = 50
$D3 = 50
$D4 = 50
$D5 = |New Equipment|

!NAME = $1
!E = $2
!N = $3
!U = $4
!DESC = |$5|

NEW EQUI $!NAME
POSITION E $!E N $!N U $!U
!!CE.DESCRIPTION = !DESC

Q POSITION
Q Desc
```

Input
```
$M/C:\DB\NewEqui.mac |/MyNewEqui| 500 500 500 $<This is my Equipment$>
```

## 7.2 Synonyms

Longer commands can be stored with short abrivation called Synonyms.

Input
```
$SNewEqui=NEW EQUI NAME $S1 

NewEqui /NewEquipmentX
```

In above Example Synonyms `NewEqui` contains the one argument is defined using `$S1`. It is possible to loop through all the elements within the hierarchy and perform some action.

Input
```
$SDescEqui=Desc |Description changed| $/ next $/ DescEqui

DescEqui
```

Above Synonym will loop through all element and change it's description attribute.

It's possible to turned off and on with the $S- and $S+ syntax. Which is typically available within DBList file.

To delete the above defined Synonym, use below syntax.
```
$SDescEqui=
```

All Synonyms can be killed with `$sk` command.
