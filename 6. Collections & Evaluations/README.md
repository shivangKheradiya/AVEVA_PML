# 6. COLLECTIONS & EVALUATIONS

Output mentioned in this page may very depending on enviroment setup.

## 6.1 COLLECTIONS

### 6.1.1 PML 1
Select any element from the explore and give following commands,

Syntax
```
var !VariableName COLLECT all <Select> with <where> for <from> /Referenece
```
Input
```
var !sites collect all sites
q var !sites
```
Output
```
<ARRAY>
   [1]  <STRING> '=67127161/1'
   [2]  <STRING> '=67127161/169'
   [3]  <STRING> '=67127161/285'
   [4]  <STRING> '=67127156/1556'
   [5]  <STRING> '=67127156/7765'
   [6]  <STRING> '=67127156/11142'
   [7]  <STRING> '=67127156/11586'
   [8]  <STRING> '=67127156/13830'
   [9]  <STRING> '=67127156/14082'
   [10]  <STRING> '=67127156/14108'
   [11]  <STRING> '=67135348/2415'
   [12]  <STRING> '=67135348/5840'
   [13]  <STRING> '=67135348/5902'
   [14]  <STRING> '=1275089552/1'
   [15]  <STRING> '=1275089552/2'
```

Select A site and Execute the below command
```
var !zone collect all zone for ce
-- Below syntax will collect all zones with description having 'XX Zone' string
var !Azone collect all zone with matchwild(desc, |*XX Zone*|) for ce
$p Zone Output
q var !zone
$p AZone Output
q var !Azone
```

Below menioned output may vary based on your Site/ Zone Hierarchy and data,
Output
```
Zone Output

<ARRAY>
   [1]  <STRING> '=23705/577'
   [2]  <STRING> '=23705/239'

AZone Output

<ARRAY> - Unset and Empty
```

### 6.1.2 PML 2

The collection is created as an object. So, It's more object oriented approach.

Input
```
!zoneCollection     = object COLLECTION()
!elementTypes       = |ZONE|
!zoneCollection.types(!elementTypes.split())
!zoneCollection.scope(!!ce)

!zone = !zoneCollection.results()

!expression = object EXPRESSION(|matchwild(desc, '*XX Zone*')|)
!zoneCollection.filter(!expression)

!Azone = !zoneCollection.results()

$p Zone Output
q var !zone
$p AZone Output
q var !Azone
```
Output
```
Zone Output

<ARRAY>
   [1]  <DBREF> =23705/577
   [2]  <DBREF> =23705/239

AZone Output

<ARRAY> - Unset and Empty
```

## 6.2 EVALUATIONS

### 6.2.1 PML 1

This syntax is valid for only PML 1 Collection Array or Array Contains DbRef as String object.

Syntax
```
var !outputArray evaluate <Attribute/ Expression> for ALL <ElementTypes> with <Expression> from <DbRefStringArray> 
```

Input
```
-- Select Site /SITE-PIPING-AREA01
var !zone collect all for ce
-- Evaluating name and position of All Zones within CE
var !zoneNames evaluate NAME for ALL Zone from !zone 

-- Update zone East position which you wish to see in output e.g. /ZONE-PIPING-AREA01 Position E 5mm N 0mm U 0mm
var !zonePositions evaluate Position for ALL Zone from !zone
var !zonePosE2Times evaluate ( position[1] * 2 ) for ALL Zone from !zone 
var !zonePosE2TimesX evaluate ( position[1] * 2 ) for ALL Zone with Matchwild(name, |*AREA03*|) from !zone 
q var !zoneNames
q var !zonePositions
q var !zonePosE2Times
q var !zonePosE2TimesX
```

Output
```
<ARRAY>
   [1]  <STRING> '/ZONE-PIPING-AREA01'

<ARRAY>
   [1]  <STRING> 'E 5mm N 0mm U 0mm'

<ARRAY>
   [1]  <STRING> '10mm'

<ARRAY> - Unset and Empty
```

### 6.2.2 PML 2

This syntax is valid for only PML 2 Collection Array or Array Contains DbRef objects. And outputArray can be of any object type depending on the expression used in Block Statement.

Syntax
```
!block            = object BLOCK(|!collectionArray[!evalIndex].<Attribute/Expression>|) 
!outputArray      = !collectionArray.evaluate(!block) 
```

Input
```
!zone             = !!collectAllfor(|ZONE|, ||, !!ce)
!blockName        = object BLOCK(|!zone[!evalIndex].name|)
!blockPos         = object BLOCK(|!zone[!evalIndex].Position|)
!blockPos2        = object BLOCK(|!zone[!evalIndex].Position.east * 2|)

!zoneNames        = !zone.evaluate(!blockName)

-- Update zone East position which you wish to see in output e.g. /ZONE-PIPING-AREA01 Position E 5mm N 0mm U 0mm
!zonePositions    = !zone.evaluate(!blockPos)
!zonePosE2Times   = !zone.evaluate(!blockPos2)

q var !zoneNames
q var !zonePositions
q var !zonePosE2Times
```

Output
```
<ARRAY>
   [1]  <STRING> '/ZONE-PIPING-AREA01'

<ARRAY>
   [1]  <POSITION> E 5mm N 0mm U 0mm WRT /SITE-PIPING-AREA01

<ARRAY>
   [1]  <REAL> 10mm
```