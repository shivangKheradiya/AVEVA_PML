# 10. Forms

- [Basic Understanding And Syntax](#basic-understanding-and-syntax)
- [Syntax of Form & Callbacks](#syntax-of-form-&-callbacks)
- [Gedget Positioning Using Paths](#gedget-positioning-using-paths)
- [Docking and Anchoring](#docking-and-anchoring)
- [Gadgets Implimentation](#gadgets-implimentation)
    - [TEXTPANE Gadget](#textpane-implimentation)
    - [Text Entry Gadget](#text-entry-gadget)
    - [Paragraph Gadget](#paragraph-gadget)
    - [Button Gadget](#button-gadget)
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

## Gedget Positioning Using Paths
