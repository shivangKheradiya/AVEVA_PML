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
- 
```
setup form !!TextEntryGadget
    !this.formTitle = |Text Entry Gadget Form|
    text .t1 |Text String| width 50 is string
    Halign Left
    path down
    text .t2 |String| width 50 is string
    text .t3 |Numbers| width 50 is real format !!realfmt
    text .t4 |Round Numbers| width 50 is real format !!integerfmt
    text .t5 |Passwords| width 50 NOE is string
    text .t6 |Non Editable| width 50 is string
exit

define method .TextEntryGadget()
    !this.t6.val = |Fixed Text|
    !this.t6.setEditable(False)
endmethod
```

### Textpane Gadget
```

setup form !!TextpaneGadget
    
exit

define method .DockAnchor() 
    
endmethod
```
