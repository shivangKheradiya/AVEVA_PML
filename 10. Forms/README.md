# 10. Forms

- [Basic Understanding And Syntax](#basic-understanding-and-syntax)
- [Syntax of Form & Callbacks](#syntax-of-form-&-callbacks)
- [Gadget Positioning Using Paths](#gadget-positioning-using-paths)
- [Docking and Anchoring](#docking-and-anchoring)
- [Gadgets Implimentation](#gadgets-implimentation)
    - [Paragraph Gadget](#paragraph-gadget)
    - [Button Gadget](#button-gadget)
    - [Text Entry Gadget](#text-entry-gadget)
    - [Textpane Gadget](#textpane-implimentation)
    - [Radio Gadget](#radio-gadget)
    - [Toggle Gadget](#toggle-gadget)
    - [Slider Gadget](#slider-gadget)
    - [Option Gadget](#option-gadget)
    - [List Gadget](#list-gadget)
    - [Line Gadget](#line-gadget)
    - [Frame Gadget](#frame-gadget)
    - [Alpha View Gadget](#alpha-view-gadget)
    - [Area View Gadget](#area-view-gadget)
    - [Plot View Gadget](#plot-view-gadget)
    - [3D Graphics/ Canvas/ Volume View](#3d-graphics/-canvas/-volume-view)
    - [Alert Gadget](#alert-gadget)
    - [Progress Bar Gadget](#progress-bar-gadget)
- [Tooltip & pixmap](##tooltip-&-pixmap)
- [Menu Gadget](##menu-gadget)
    - [bar menu](#bar-menu)
    - [popup menu](#popup-menu)
    - [Adding menu](#adding-menu)
- [FileBrowser](##file-browser)
- [TreeView](##tree-view)

## Basic Understanding And Syntax

Key Points to remember;
- Forms are global object(Extension of the Objects). So, All the features available within objects are possible to used in forms. 
- Forms must be stored within `PMLLIB` directory with (`.pmlfrm`) extension.
- To reload form `pml reload form !!FormName` command is used.
- `FormFile` must has the same name as the name of the form defined in the PML. and `FormName` Should not contain any space or special Characters.
- Horizontal dimention (Width) are considered in terms of the number of character from the top left corner of the form.
- Vertical dimention (Height) are considered in terms of a line height from the top left corner of the form.

## Syntax of Form & Callbacks

Callbacks can be used for one of the following thing;
- Command execution
- Run a function
- Run a Method
- Execute a Special Callback assigned on Gadget/ Forms

```
setup form !!SampleCallback 
    !this.formTitle = |Callback Sample Form| 
    !this.initCall = |!this.init()| 
    !this.firstShownCall = |!this.firstShown()| 
    !this.okCall = |!this.okCall()| 
    !this.cancelCall = |!this.cancelCall()| 
    !this.quitCall = |!this.quitCall()| 
    !this.killingCall = |!this.killCall()| 
    button .ok | OK | OK 
    button .cancel |Cancel| at x20 CANCEL 
exit

-- Constructuor calls when Form Loaded and must match the name of the form or file
define method .SampleCallback() 
    $p Constructor Called 
endmethod

-- Init Method Calls everytime when the form is shown 
define method .init() 
    $p Initialise Method 
endmethod

-- FirstShown Method calls when the first time form is shown/ activated
define method .firstShown() 
    $p First Shown Method 
endmethod

-- OkCall Method calls when any button gedget with OK defination
define method .okCall() 
    $p OK Method 
endmethod

-- CancelCall Method calls when any button gedget with CANCEL defination
define method .cancelCall() 
    $p Cancel Method 
endmethod

-- QuitCall Method calls when close button clicked
define method .quitCall() 
    $p Quit Method 
endmethod

-- KillCall Method calls when form is killed or Reloaded
define method .killCall() 
    $p Kill Method 
endmethod
```

Follow below mentioned step to test the form,

- Save the above code within `pmllib` with file name `SampleCallback.pmlfrm`.
- Run `pml rehash all` or `pml reload form !!SampleCallback` command.
- Run `show !!SampleCallback` command.
- Test the opend form & Obsurve the commandline output to verify the behavior of the form.
- Run `hide !!SampleCallback` command or `kill !!SampleCallback` command.

*Constructor > Init > FirstShown > Quit > Cancle*

## Gadget Positioning Using Paths

Gadget Path are used with some main keywords 
 
 - PATH : Right / Left / Up / Down
 - HDIST or VDIST : number
 - HALIGN : Left / Right / Centre or VALIGN : Top/ Bottom / Centre.

```
setup form !!GadGetUsingPath resize
    Button .bu1 width 10 height 2
    path down
    vdist 2
    halign left
    Button .bu2 width 40 height 2
    vdist 2
    halign right
    Button .bu3 width 20 height 3
    path right
    valign bottom
    hdist 2
    valign top
    Button .bu4 width 10 height 4
exit

define method .GadGetUsingPath() 
    
endmethod
```

## Docking and Anchoring

if anyone of the following things are found in the syntaxgraph of the Gadget then, it's possible to use the functionality.

- Anchoring ( <fganch> ) : Positions the edge of the eadget relative to the corrosponding edge of it's container.
- Dock ( <fgdock> ) : Fills the available space in a certain direction. `dock fill` will fill the full space of parent container. 

```
setup form !!DockAnchor
    frame .f1 dock fill
        list .l1 anchor all width 10 height 5
        Button .b1 anchor r+b at xmax.l1 - 0.5 - 2 * size  ymax.l1 + 0.25
        Button .b2 anchor r+b at xmax.l1 - size  ymax.l1 + 0.25
    exit
exit

define method .DockAnchor() 
    
endmethod
```

## Gadgets Implimentation

### Paragraph Gadget

Paragraph Text's Possible Implimentations:
- Paragraph Text with/ without background
- Image Paragraph (Pixmap)

```
setup form !!ParagraphGadget
    !this.formTitle = |Paragraph Gadget Form|
    para .p1 text |Sample Text Paragraph| width 50
    Halign Left
    path down
    para .p2 background 3 text |Text Paragraph| width 50
    para .p3 pixmap width 150 height 50
    para .p4 text || width 50
exit

define method .ParagraphGadget() 
    !this.p4.val = |This Text is set by constructor|
    !this.p3.addPixmap(|C:\PngFilePath.png|)
endmethod
```

### Button Gadget

Button's Possible Implimentations:
- Button with/ without Background
- Button as LinkLabel
- Toggle Button with/ without Background

```
setup form !!ButtonGadget
    !this.formTitle = |Button Gadget Form|
    button .b1 |Test Button 1| width 50
    Halign Left
    path down
    button .b2 |Test Button 2| background 3  width 50
    button .b3 LINKLabel |Test Link Label Button 3| width 50
    button .b4 toggle |Test Toggle Button 4| width 50 call |!this.activeButton5()|
    button .b5 toggle |Test Toggle Button 5| background 3  width 50
    member .but5Active is boolean 
exit

define method .ButtonGadget() 
    !this.but5Active = true
endmethod

define method .activeButton5() 
    if (!this.but5Active) then
        !this.but5Active = false
        !this.b5.active = false
    else
        !this.but5Active = true
        !this.b5.active = true
    endif
endmethod
```

### Text Entry Gadget

Text Entry Gadget's Possible Implimentations:
- String Values
- Numeric Values
- Numeric Round Values
- Password Case Values
- Non Editable Values
  
```
setup form !!TextEntryGadget
    !this.formTitle = |Text Entry Gadget Form|
    text .t1 |String        | width 50 is string
    Halign Left
    path down
    text .t2 |Numbers       | width 50 is real format !!realfmt
    text .t3 |Round Numbers | width 50 is real format !!integerfmt
    text .t4 |Passwords     | width 50 NOE is string
    text .t5 |Non Editable  | width 50 is string
exit

define method .TextEntryGadget()
    !this.t5.val = |Fixed Text|
    !this.t6.setEditable(False)
endmethod
```

### Textpane Gadget

Textpane is used to write some code or notes within PML Form. It stores the Data in form of an Array.

```
setup form !!TextpaneGadget
    !this.formTitle = |Textpane Gadget Form|
    text .t1 call |!this.append()| width 30 is STRING
    button .but1 linklabel |Append Line| at xmax.t1 + 0.5 y 0 call |!this.appendLine()| wid 10
    textpane .tp1 |Text Pad| at x 0 y1 wid 45 hei 7
exit

define method .TextpaneGadget() 
    !text = object array()
    !this.tp1.val = !text 
endmethod

define method .appendLine() 
    !text = !this.tp1.val
    !text.append( !this.t1.val )
    !this.tp1.val = !text
endmethod

define method .append() 
    $p Append method is triggered
endmethod
```

### Option Gadget

```
setup form !!OptionsGadget resize
  !this.formTitle = |Options Gadget Form| 
  path down 
  option .op1 |Normal - Dtext Only    | width 10
  combo  .op2 |Combo  - Dtext & Rtext | width 10
  option .op3 |Pixmap - Dtext Gif     | pixmap width 100 height 50
exit

define method .OptionsGadget() 
  !dtext = |Red Yellow| 
  !this.op1.dtext = !dtext.split() 
  !this.op2.dtext = !dtext.split() 
  do !n index !this.op1.dtext 
    !files[!n] = |/c:\PathForGif\| & !n & |.gif| 
  enddo
  !this.op3.dtext = !files
  !this.op3.rtext = !dtext.split() 
  !this.op2.callback = |!this.setOpt(| 
endmethod

define method .setOpt(!gad is gadget, !event is STRING)
  q var !event
  q var !gad
  if !event.eq('SELECT') then
    !this.op3.val = !this.op2.val.real()
  endif
endmethod
```

Key Points to Remember,
- `q var !!OptionExample.opt3.selection()` Gives the Rtext Value
- Option Gadget can have `PIXMAPS` or `STRINGS`
- Options Can have Open Callbacks e.g. Text Auto Completion Functionality
- Name of Text is optional

### List Gadget

```
setup form !!ListGadget resize
    !this.formTitle = |List Gadget Form| 
    list .l1 || |Single Array List   | call |!this.QueryValue( '1' )| SINGLE ZEROSEL width 15 height 5
    path down
    list .l2 |Multi Select List   | call |!this.QueryValue( '2' )| MULTI width 15 height 5
    list .l3 |List Appending      | call |!this.QueryValue( '3' )| width 15 height 5
    list .l4 |Multi column List   | call |!this.QueryValue( '4' )| width 15 height 5
exit

define method .ListGadget() 
    !this.SetL1Member()
    !this.SetL2Member()
    !this.SetL3Member()
    !this.SetL4Member()
endmethod

define method .SetL1Member()
    !dtext[1] = |d1|
    !rtext[1] = |r1|
    !dtext[2] = |d2|
    !rtext[2] = |r2|
    !this.l1.dtext = !dtext
    !this.l1.rtext = !rtext
    !heading = |Heading|
    !this.l1.setHeadings(!Heading.split())
endmethod

define method .SetL2Member()
    !dtext[1] = |d1|
    !dtext[2] = |d2|
    !this.l2.dtext = !dtext
endmethod

define method .SetL3Member()
    !dtext[1] = |Appendable List|
    !this.l3.dtext = !dtext
    !this.l3.add(|New Item 1 Added|)
endmethod

define method .SetL4Member()
    !heading = |Heading_1 Heading_2|
    !this.l4.setHeadings(!heading.split())
    !row[1] = |Data 1 1|
    !row[2] = |Data 1 1|
    !rowData[1] = !row
    !row[1] = |Data 2 1|
    !row[2] = |Data 2 1|
    !rowData[2] = !row
    !this.l4.setRows(!rowData)
endmethod

define method .QueryValue( !listNumber is string ) 
    !dtext = !this.l$!<listNumber>.selection('Dtext') 
    !rtext = !this.l$!<listNumber>.selection('Rtext') 
    $p Selected Dtext = $!<dtext> Rtext = $!<rtext>
endmethod
```

Key Points to Remember,
- List can be Single Select Multiple Select
- List can have Multiple Columns
- Rtext and Dtext Will react based on the type of the list defination

### Frame Gadget

```
setup form !!FrameGadget resize
    !this.formTitle = |Frame Gadget Form| 
    frame .f1 TABSET anchor ALL wid 15 hei 5 
        frame .fToolBar |Normal Tab| dock fill
            para .p1 text |Put any required Gadgets|
        exit
        frame .fPanel |Panel| dock fill
            button .b1 |Show Hide Panel| at 0 0 call |!this.foldUnfold()| 
            frame .fPanel1 panel |Panel Frame| at x0 ymax.b1 dock fill
                frame .fPanelFoldup foldup |Foldup 1| at x0 ymin.fPanel1 + 1 width 10 height 5
                   
                exit
            exit
        exit
        frame .fDock |Dock| dock fill
            frame .fDockAll |Dock All| dock fill  
                frame .fDockRight |Dock Right| dock RIGHT width.fPanelFoldup + 10 
                    frame .fDockLeft |Dock Bottom| dock b hei 4 
                    exit
                exit 
            exit
        exit
    exit
exit

define method .FrameGadget() 

endmethod

define method .foldUnfold() 

    if (!this.fPanelFoldup.expanded) then
        !this.fPanelFoldup.expanded = false
    else
        !this.fPanelFoldup.expanded = true
    endif

endmethod
```

Key Points to Remember,
- Frame can be any one of the type `TABSET`, `FOLDUP`, `PANEL`, `TOOLBAR`(when defined for the main window)
- Frame must be ending with `exit`
- If any error occured within frame, type `exit` untill error is available (In other words, Exit the frame & form). 

### Radio Gadget


### [Toggle Gadget](#toggle-gadget)
### [Slider Gadget](#slider-gadget)
### [Line Gadget](#line-gadget)
### [Alpha View Gadget](#alpha-view-gadget)
### [Area View Gadget](#area-view-gadget)
### [Plot View Gadget](#plot-view-gadget)
### [3D Graphics/ Canvas/ Volume View](#3d-graphics/-canvas/-volume-view)
### [Alert Gadget](#alert-gadget)
### [Progress Bar Gadget](#progress-bar-gadget)
## [Tooltip & pixmap](##tooltip-&-pixmap)
## [Menu Gadget](##menu-gadget)
### [bar menu](#bar-menu)
### [popup menu](#popup-menu)
### [Adding menu](#adding-menu)
## [FileBrowser](##file-browser)
## [TreeView](##tree-view)