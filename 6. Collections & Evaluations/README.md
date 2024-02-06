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
Input
```
```
Output
```
```

### 6.2.2 PML 2
Input
```
```
Output
```
```