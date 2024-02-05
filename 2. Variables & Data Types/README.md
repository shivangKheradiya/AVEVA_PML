# 2. VARIABLES & DATA TYPES

## 2.1 Variable

Variable can be declared using following code,

Method 1: PML 1

`var !x 'Tommy'`

Method 2: PML 2

`!x = 'Tommy'`

Declaration of Empty variable

`!x = object string()`

To seet the Value of the Variable

`Q var !x`

## 2.2 Scope of Variable

### 2.2.1 **Local Variable:** 

It is represented with Single exclaimation symbol ( **!** ) before the variable Name. e.g.

`!x = 'Tommy'`

### 2.2.2 **Global Variable:** 

It is represented with Double exclaimation symbol ( **!!** ) before the variable Name. e.g.

```
!!x = 'Tommy'
Q VAR !!CE
```

## 2.3 Destroy the Variable

Delete method is used to delete the variable from the existing environment scope.

```
var !x 'Tommy'
!!x = 'Global Tommy'

!x.delete()
!!x.delete()
```

## 2.4 Data Types of Variable

### 2.4.1 **System Defined:** 

1. Real:

    Declaration: It declares unset/empty variable.
    
    `!x = object REAL()`

    Declaration & Initialization:

    `!x = 5`

2. String:

    Declaration: It declares unset/empty variable.
    
    `!x = object STRING()`

    Declaration & Initialization:

    `!x = 'Tommy'`

3. Boolean:

    Declaration: It declares unset/empty variable.
    
    `!x = object BOOLEAN()`

    Declaration & Initialization:

    `!x = true`

4. Array: It can hold variable of any datatype as an element of array. Multidimentional array defination is also possible. But Having different data types in array and Multidimentional array reduces the performance.

    Declaration: It declares unset/empty variable.

    `!x = object ARRAY()`

    Declaration & Initialization:

    ```
    !x[1] = 5
    !x[2] = 'Tommy'
    !x[3] = true
    !x[4] = object array()
    ```

### 2.4.2 **Built-in:**
    
1. Position: It's attribute made of basically 4 parameter.
    
    East: East directional distance of the element from origin. 
    
    North: East directional distance of the element from origin.
    
    Up: Up directional distance of the element from origin.
    
    Origin: It's reference element from which the distance is measured.

    e.g. Select any element having position attribute and execute below code,
    
    Input:
    ```
    !X = POSITION
    Q VAR !X
    ```
    Output:
    ```
    <POSITION> E 1825mm S 10030mm U 3600mm WRT /11QEB11BR003/B01
       EAST <REAL> 1825mm
       NORTH <REAL> -10030mm
       ORIGIN <DBREF> =1342195224/283833
       UP <REAL> 3600mm
    ```

2. Orientation: Based on the Euler's  angles denotion, Orientation is made up of Alpha, Beta, Gema and Origin parameters.

    e.g. Select any element having orientation attribute and execute below code,
    Input:
    ```
    !X = ORIENTATION
    Q VAR !X
    ```
    Output:
    ```
    <ORIENTATION> Y is W WRT /11QEB11BR003/B01 and Z is D WRT /11QEB11BR003/B01
       ALPHA <REAL> 180
       BETA <REAL> 0
       GAMMA <REAL> -90
       ORIGIN <DBREF> =1342195224/283833
    ```

### 2.4.3 **User-defined:** 
These are similar to Built-in variables, these are objects defined by users in Pml.Net or PML.

## 2.5 Type Casting
Type Casting to boolean,

Input:
```
!boolString = |true|
!bool = !boolString.boolean()
q var !bool
```
Output:
```
<BOOLEAN> TRUE
```

Type Casting to real,

Input:
```
!realString = |5|
!real = !realString.real()
q var !real
```
Output:
```
<REAL> 5
```

Type Casting to String,

Input:
```
!real = 5.555
!realString = !real.String('D2') -- For 2 digits
q var !realString

!bool = true
!boolString = !bool.String()
q var !boolString
```
Output:
```
<STRING> '5.55'
<STRING> 'TRUE'
```

## 2.6 Extra

### 2.6.1 .OBJECTTYPE()
following code can be used to know the object type,

Input:
```
!x = position
q var !x.objecttype()
```
Output:
```
<STRING> 'POSITION'
```

### 2.6.2 .METHODS()
following code can be used to know the methods available within the object

Input:
```
!X = POSITION
Q VAR !X.METHODS()
```
Output:
```
<ARRAY>
   [1]  <STRING> 'ANGLE(POSITION, POSITION)'
   [2]  <STRING> 'ARC(POSITION, POSITION)'
   [3]  <STRING> 'ARC3LINES(LINE, LINE, LINE, DIRECTION)'
   [4]  <STRING> 'ARCCENTRE(POSITION, POSITION, POSITION, DIRECTION, REAL)'
   [5]  <STRING> 'ARCFILLET(POSITION, POSITION, DIRECTION, REAL)'
   [6]  <STRING> 'ARCRADIUS(POSITION, POSITION, DIRECTION, REAL, BOOLEAN)'
   [7]  <STRING> 'ARCTHRU(POSITION, POSITION, DIRECTION)'
   [8]  <STRING> 'ARCTHRU(POSITION, POSITION, DIRECTION, REAL)'
   [9]  <STRING> 'ATTRIBUTE(STRING)'
   [10]  <STRING> 'ATTRIBUTES()'
   [11]  <STRING> 'COMPONENT(DIRECTION)'
   [12]  <STRING> 'DIRECTION(POSITION)'
   [13]  <STRING> 'DISTANCE(POSITION)'
   [14]  <STRING> 'DISTANCE(PLANE)'
   [15]  <STRING> 'DISTANCE(LINE)'
   [16]  <STRING> 'DISTANCE(ARC)'
   [17]  <STRING> 'EQ(POSITION)'
   [18]  <STRING> 'LINE(POSITION)'
   [19]  <STRING> 'LT(POSITION)'
   [20]  <STRING> 'MIDPOINT(POSITION)'
   [21]  <STRING> 'NEAR(POSITION, REAL)'
   [22]  <STRING> 'OFFSET(DIRECTION, REAL)'
   [23]  <STRING> 'PLANE(POSITION, POSITION)'
   [24]  <STRING> 'POSITION(STRING)'
   [25]  <STRING> 'POSITION(STRING, FORMAT)'
   [26]  <STRING> 'STRING()'
   [27]  <STRING> 'STRING(FORMAT)'
   [28]  <STRING> 'WRT(DBREF)'
```

### 2.6.3 ATTRIBUTE()
following code can be used to know more information about attribute.

Input:
```
!POS = object ATTRIBUTE('POSITION')
Q VAR !POS
Q VAR !POS.METHODS()
```
Output:
```
<ATTRIBUTE> ATTRIBUTE

<ARRAY>
   [1]  <STRING> 'ASSIGN(ATTRIBUTE)'
   [2]  <STRING> 'ATTRIBUTE()'
   [3]  <STRING> 'ATTRIBUTE(STRING)'
   [4]  <STRING> 'CATEGORY()'
   [5]  <STRING> 'CONNECTION()'
   [6]  <STRING> 'DEFAULTVALUE(ELEMENTTYPE)'
   [7]  <STRING> 'DESCRIPTION()'
   [8]  <STRING> 'ELEMENTTYPES()'
   [9]  <STRING> 'HASH()'
   [10]  <STRING> 'HIDDEN()'
   [11]  <STRING> 'HYPERLINK()'
   [12]  <STRING> 'ISPSEUDO()'
   [13]  <STRING> 'ISUDA()'
   [14]  <STRING> 'LENGTH()'
   [15]  <STRING> 'LIMITS(ELEMENTTYPE)'
   [16]  <STRING> 'LIMITSVALIDOPTIONAL(ELEMENTTYPE)'
   [17]  <STRING> 'NAME()'
   [18]  <STRING> 'NOCLAIM(ELEMENTTYPE)'
   [19]  <STRING> 'PROTECT()'
   [20]  <STRING> 'QUERYTEXT()'
   [21]  <STRING> 'TYPE()'
   [22]  <STRING> 'UNITS()'
   [23]  <STRING> 'VALID()'
   [24]  <STRING> 'VALIDVALUES(ELEMENTTYPE)'
```

### 2.6.4 .ATTRIBUTES()
Following code will help to know the all available attributes for any element,

Input:
```
!ATT = !!CE.ATTRIBUTES()
Q VAR !ATT
```

Output:
```
<ARRAY>
   [1]  <STRING> 'Name'
   [2]  <STRING> 'Type'
   [3]  <STRING> 'Lock'
   [4]  <STRING> 'Owner'
   [5]  <STRING> 'Position'
   [6]  <STRING> 'Orientation'
   [7]  <STRING> 'Desparam'
   [8]  <STRING> 'Built'
   [9]  <STRING> 'Shop'
   [10]  <STRING> 'Isohidden'
   [11]  <STRING> 'Spref'
   [12]  <STRING> 'Lstube'
   [13]  <STRING> 'Arrive'
   [14]  <STRING> 'Leave'
   [15]  <STRING> 'Oriflag'
   [16]  <STRING> 'Posflag'
   [17]  <STRING> 'Ispec'
   [18]  <STRING> 'Tspec'
   [19]  <STRING> 'Angle'
   [20]  <STRING> 'Radius'
   [21]  <STRING> 'Cref'
   [22]  <STRING> 'Csfbreak'
   [23]  <STRING> 'Tsfbreak'
   [24]  <STRING> 'Asfbreak'
   [25]  <STRING> 'Lsfbreak'
   [26]  <STRING> 'Spln'
   [27]  <STRING> 'Splt'
   [28]  <STRING> 'Mtoref'
   [29]  <STRING> 'Cmpx'
   [30]  <STRING> 'Ptno'
   [31]  <STRING> 'Ptntube'
   [32]  <STRING> 'Ptnbarray'
   [33]  <STRING> 'Jnumber'
   [34]  <STRING> 'Joiprefix'
   [35]  <STRING> 'Mtocomponent'
   [36]  <STRING> 'Mtotube'
   [37]  <STRING> 'Mtoxarray'
   [38]  <STRING> 'Spsp'
   [39]  <STRING> 'Dpfname'
   [40]  <STRING> 'Dpgridref'
   [41]  <STRING> 'Nwelds'
   [42]  <STRING> 'Dmtype'
   [43]  <STRING> 'Dmfarray'
   [44]  <STRING> 'Bselector'
   [45]  <STRING> 'MATN'
   [46]  <STRING> 'Rlock'
   [47]  <STRING> 'Rlinclude'
   [48]  <STRING> 'Rlexclude'
   [49]  <STRING> 'Hrelative'
   [50]  <STRING> 'Spkchg'
   [51]  <STRING> 'Deldsg'
   [52]  <STRING> 'Inprtref'
   [53]  <STRING> 'Ouprtref'
   [54]  <STRING> 'Aexcess'
   [55]  <STRING> 'Lexcess'
   [56]  <STRING> 'Loose'
   [57]  <STRING> ':ERAPPADETAIL'
   [58]  <STRING> ':ERADETAILVIEW'
   [59]  <STRING> ':ComosBaseOb'
   [60]  <STRING> ':ComosSClass'
   [61]  <STRING> ':ComosName'
   [62]  <STRING> ':ComosCRefNo'
   [63]  <STRING> ':ComosStatus'
   [64]  <STRING> ':ComosUID'
   [65]  <STRING> ':R2REF'
   [66]  <STRING> ':R2TUBIREF'
   [67]  <STRING> ':R2UTIL'
   [68]  <STRING> ':POWAREANAME'
   [69]  <STRING> ':POWDTEXT'
   [70]  <STRING> ':POWMATERIAL'
   [71]  <STRING> ':POWCOMPPARTS'
   [72]  <STRING> ':POWCOMPTYPE'
   [73]  <STRING> ':POWOLDREFE'
   [74]  <STRING> ':POWWMAT'
   [75]  <STRING> ':SH_PIPE_SCH'
   [76]  <STRING> ':SH-MTO-TYPE'
   [77]  <STRING> ':SH-MTO-DESC'
   [78]  <STRING> ':SH-MTO-QTY'
   [79]  <STRING> ':SH-MTO-LENGTH'
   [80]  <STRING> ':SH-MTO-WEIGHT'
   [81]  <STRING> ':SH-MTO-REMARK'
   [82]  <STRING> ':SH-MTO-MATERIAL'
   [83]  <STRING> ':ISOSHIPCOORD'
   [84]  <STRING> ':CutLength'
   [85]  <STRING> ':PFILoose'
   [86]  <STRING> ':PFILExcess'
   [87]  <STRING> ':PFIAExcess'
   [88]  <STRING> 'MEMBERS'
```