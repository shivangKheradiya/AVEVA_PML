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
    - [View Gadget](#view-gadget)
    - [Tooltip](##tooltip)
- [Alert Object](#alert-gadget)
- [Progress Bar Object](#progress-bar-gadget)
- [Menu Gadget](#menu-gadget)
    - [Bar Menu](#bar-menu)
    - [Popup Menu](#popup-menu)
- [File Browser Object](#file-browser-object)
- [Event Driven Graphics(EDG)](#event-driven-graphics-(edg))
- [Tree View](#tree-view)

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
 
 - `PATH` : Right / Left / Up / Down
 - `HDIST` or VDIST : number
 - `HALIGN` : Left / Right / Centre or VALIGN : Top/ Bottom / Centre.

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
- Pixmap Button

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
    button .b6 pixmap
    member .but5Active is boolean 
exit

define method .ButtonGadget() 
    !this.but5Active = true
    !this.b6.addPixmap(!!pml.getPathName('discard.png'))
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

```
setup form !!RadioGadget resize
    !this.formTitle = |Radio Gadget Form|
    rgroup .rgp |RGroup| FRAME horizontal callback |!this.rGroupCb(!this.rgp)|
        add tag |TagA| select |A|
        add tag |TagB| select |B|
        add tag |TagC| select |C|
    exit
    path down
    frame .rToggleFrame |RToggle| 
      rToggle .tagA |TagA| states || |A| 
      rToggle .tagB |TagB| call |!this.getOnValue(!this.tagB)| states |SBOFF| |B| 
      rToggle .tagC |TagC| states || |C|
      button .bu1 |B1|
    exit 
exit

define method .RadioGadget() 
    !this.rToggleFrame.callback = |!this.rtgFrame(!this.rToggleFrame)|
endmethod

define method .rGroupCb(!gad is GADGET) 
    q var !gad.selection()
endmethod

define method .rtgFrame(!gad is GADGET)
    -- Ony For Rtoggle, From the Frame, it's possible to get the Rtoggle child number
    !rtog = !gad.rtoggle(!gad.val) 
    $p OnValue
    q var !rtog.onvalue
    $p OffValue
    q var !rtog.offvalue 
endmethod

define method .getOnValue(!gad is GADGET)
    $p OnValue
    q var !gad.onvalue
    $p OffValue
    q var !gad.offvalue 
endmethod
```

Key Points to Remember,
- Radio Buttons are can be implimented in 2 ways `rgroup` and `rtoggle`.
- `rgroup` will may depricate in future. and It can be arranged horizontally or vertically
- `rtoggle` is used within frame only. and it can be placed within frame anywhere.
- Ony For `Rtoggle`, From the `frame`, it's possible to get the Rtoggle child based on number

### Toggle Gadget

```
setup form !!TogglesGadget resize
    !this.formTitle = |Toggles Gadget Form| 
    path right 
    toggle .toggleA tagwid 15 |Normal Toggle| call |!this.stateChange(!this.toggleA)| 
    toggle .toggleB tagwid 15 |Change States| call |!this.stateChange(!this.toggleB)| states |N| |Y| 
    numeric .numToggle |Numeric Toggle| callback |!this.NumToggleChange(| at xmin.toggleA ymax.toggleB range 0 10 step 1 NDP 0 wid 3 
exit

define method .TogglesGadget()

endmethod

define method .stateChange(!gad is GADGET) 
    if ( !gad.val ) then 
        q var !gad.onvalue 
    else 
        q var !gad.offvalue 
    endif 
endmethod

define method .NumToggleChange(!gad is GADGET, !event is STRING)
    q var !gad.val
    q var !event
endmethod
```

Key Points to Remember,
- Toggle can be any one of 
    - `toggle` (Checkbox with/ without state)
    - `NumericInput`

### Line Gadget

Lines are used to generate partition within the form.

```
setup form !!LineGadget resize
    !this.formTitle = |Line Gadget Form| 
    line .lineA horizontal wid 15 hei 1
    path right
    line .lineB vertical wid 1 hei 5
    line .lineC horizontal wid 15 hei 1
exit

define method .LineGadget()

endmethod
```

### Slider Gadget

```
setup form !!SliderGadget 
    !this.formTitle = |Slider Gadget Form| 
    slider .slider anchor L+R horizontal range 0 100 step 5 val 50 width 30 
    member .sliderValue is REAL 
exit

define method .SliderGadget()
    !this.slider.callback = |!this.sliderMove(|
endmethod

define method .SliderMove(!gad is GADGET, !event is STRING)
    q var !gad.val
    q var !event
endmethod
```

Obsurve the command window to see the outcome of the slider movement. 

### View Gadget

View Gadget has following types of implimentations,
- Alpha View Gadget - 1D
- Area View Gadget - 2D Draw
- Plot View Gadget - 2D Plot File
- Volume View Gadget - 3D

```
setup form !!AlphaViewGadget
    !this.formTitle = |Alpha View Gadget Form|
    view .input AT X 0 Y 0 ALPHA
        height 15 width 60
        channel REQUESTS
        channel COMMANDS
    exit
exit
```

```
setup form !!PlotViewGadget resize
    !this.formTitle = |Plot View Gadget Form| 
    view .plot plot anchor all width 41 hei 15 
        -- CURS NOCURSOR 
    exit
exit 
 
define method .PlotViewGadget() 
    !this.plot.borders = true 
    !this.plot.add(|/%PMLUI%\plots\equip\base-for-pumpset-drg.plt|) 
endmethod
```

Select any graphical element e.g. PIPE, EQUI and open below form,

```
setup form !!VolumeViewGadget resize
    !this.formTitle = |Volume View Gadget Form|
    !this.initcall = |!this.init()|
    !this.firstShownCall = |!this.firstShownCall()|
    !this.quitcall = |!this.quit()|
    view .VolumeView Volume width 41 hei 15
        width 46 height 15 
        limits auto 
        isometric 3
    exit
    path down
    button .buAdd |Add CE| call |!this.setDrawlist(1, false)| width 15
    button .buRemove |Rem CE| call |!this.setDrawlist(2, false)| width 15
    button .buClear |Clear| call |!this.setDrawlist(0, true)| width 15
    member .drawlist is REAL
exit 
 
define method .VolumeViewGadget()
    !this.VolumeView.borders = true
    !this.drawlist = !!gphDrawlists.createDrawList()
endmethod

define method .setDrawlist(!flag is REAL, !reset is BOOLEAN)
    !drawlist = !!gphDrawlists.drawlist(!this.drawlist)

    -- Clear the drawlist is a reset is requested 
    if !reset then 
        !drawlist.removeall() 
    endif

    -- Add/Remove CE 
    if !flag.eq(1) then 
        !drawlist.add(!!CE) 
    elseif !flag.eq(2) then 
        !drawlist.remove(!!CE) 
    endif

    !this.walkDrawlist() 
endmethod

define method .walkDrawlist() 
    !drawlist = !!gphDrawlists.drawlist(!this.drawlist) 
    -- derive a volume object from the members of the drawlist 
    !volume = object volume(!drawlist.members()) 
    !limits[1]    = !volume.from.east 
    !limits[2]    = !volume.to.east 
    !limits[3]    = !volume.from.north 
    !limits[4]    = !volume.to.north 
    !limits[5]    = !volume.from.up 
    !limits[6]    = !volume.to.up 
    !this.volumeView.limits = !limits 
endmethod 

define method .init()
    !this.setDrawlist(1, TRUE)
endmethod

define method .firstShownCall()
    !!gphViews.add(!this.volumeView)
    !!gphDrawlists.attachView(!this.drawlist, !this.volumeView) 
endmethod

define method .close() 
    !!gphDrawlists.detachView(!this.volumeView) 
    !!gphDrawlists.deleteDrawlist(!this.drawlist) 
endmethod
```

### Tooltip

When The mouse curser is hover on the Gadget, it will give some extra information about the functionality called as tooltip.

```
setup form !!TooltipGadget resize
    !this.formTitle = |Tooltip Object Form|
    button .buToolTip |Has Tool Tip| width 15 tooltip |This button represents the Tooltip functionality.|
exit

define method .TooltipGadget()

endmethod
```

## Alert Object

Types of Alert Object,
- Alert with No Return Value
    - Error
    - Message
    - Warning
- Alert with Return Value
    - Confirm
    - Question
    - Input

```
setup form !!AlertGadget resize
    !this.formTitle = |Alert Object Form|
    button .buError |Error| call |!this.ShowAlert('Error')| width 15
    path down
    button .buMessage |Message| call |!this.ShowAlert('Message')| width 15
    button .buWarning |Warning| call |!this.ShowAlert('Warning')| width 15
    button .buConfirm |Confirm| call |!this.ShowAlert('Confirm')| width 15
    button .buQuestion |Question| call |!this.ShowAlert('Question')| width 15
    button .buInput |Input| call |!this.ShowAlert('Input')| width 15
exit 
 
define method .AlertGadget()

endmethod

define method .ShowAlert( !type is string)

    !isReturnType = !type inset ( |Confirm|, |Question|, |Input|)

    if(!isReturnType) then
        if (!type.eq(|Input|)) then
            !answer = !!alert.$!<type>( |Type of the Alert is | + !type + | !!! |, |100|)
            q var !answer
        else
            !answer = !!alert.$!<type>( |Type of the Alert is | + !type + | !!! |)
            q var !answer
        endif
    else
        !!alert.$!<type>( |Type of the Alert is | + !type + | !!! |)
    endif

endmethod
```

## Progress Bar Object

Progress bar is part of the `!!fmsys` object.

```
setup form !!ProgressBarGadget resize
    !this.formTitle = |Progress Bar Gadget Form|
    button .buStart |Start| call |!this.Start()| width 15
    path down
    button .buStop |Stop| call |!this.Stop()| width 15
    button .buReset |Reset| call |!this.Reset()| width 15
    member .progress is real
exit
 
define method .ProgressBarGadget()
    !!fmsys.setInterrupt(!!ProgressBarGadget.buStop)
endmethod

define method .Start()
    do !n from 1 to 10000 
        !percent = !n / 100 
        -- Check if the method has been interrupted.  Break
        if (!!FMSYS.interrupt()) then 
          !!alert.message(!n & | loops were completed - | & !percent.string(|D1|) & |%|) 
          break
        endif 
        !!FMSYS.setProgress(!percent) 
    enddo
endmethod

define method .Stop()
    $p Progress bar is stoped
endmethod

define method .Reset()
    !!fmsys.setProgress(0)
endmethod
```

Key Point's to remember,
- Progress for the bar is set using `!!fmsys.setProgress( <real> )` method.
- `!!fmsys` can be inturupt using `!!fmsys.interrupt()` method. 
- To use `!!fmsys.interrupt()` method, `!!fmsys.setInturrupt(<Gadget>)` method must be implimented.

## Menu Gadget

Menu provide options to users and possible to use in a form.

Menu Object will have 3 arguments,
1. Action to perform: `Callback` , `FORM`, `SEPERATOR`, `MENU`
2. Display Text
3. PML Syntax to Perform Action

### Bar Menu

Menu bar will be in the top of the form,

```
setup form !!BarMenuGadget resize
    !this.formTitle = |Bar Menu Gadget Form|

    bar
    !this.bar.add(|File|,|FileMenu|)
    !this.bar.add(|Sub Menu|,|ViewMenu|)
    !this.bar.add(|Help|,|HelpMenu|)

    !FileMenuObj = !this.newmenu(|FileMenu|)
    !FileMenuObj.add(|SEPARATOR|)
    !FileMenuObj.add(|FORM|,|Radio Gadget Form|, |RadioGadget|)
    !FileMenuObj.add(|CALLBACK|,|Q ATT|,|q att|)

    !ViewMenuObj = !this.newmenu(|ViewMenu|)
    !ViewMenuObj.add(|SEPARATOR|)
    !ViewMenuObj.add(|MENU|,|Sub Menu|,|SubMenu|)
    !ViewMenuObj.add(|SEPARATOR|)
    
    !SubMenuObj = !this.newmenu(|SubMenu|)
    !SubMenuObj.add(|SEPARATOR|)
    !SubMenuObj.add(|CALLBACK|,|Q CE|,|Q CE|)

    !HelpMenuObj = !this.newmenu(|HelpMenu|)
    !HelpMenuObj.add(|SEPARATOR|)
    !HelpMenuObj.add(|CALLBACK|,|About|,|!this.OpenAbout()|)
exit
 
define method .BarMenuGadget()

endmethod

define method .OpenAbout()
    $p About is opened
endmethod
```

Key Point's to remember,
- Bar menu is applicable only for non dockable forms

### Popup Menu

Popup Menu can be added in the list view.

```
setup form !!PopupMenuGadget resize
    !this.formTitle = |Popup Menu Gadget Form|
    !this.initCall = |!this.init()|
    list .lst |All Zones| callback |!this.SetupMenu()| width 100

    !MenuObj = !this.newmenu(|ZoneMenu|)
    !MenuObj.add(|SEPARATOR|)
    !MenuObj.add(|CALLBACK|,|Q ATT|,|!this.ShowData('attributes()')|)
    !MenuObj.add(|CALLBACK|,|Q Mem|,|!this.ShowData('mem')|)
exit
 
define method .BarMenuGadget()

endmethod

define method .init()
    var !allZones collect all zone for ce
    var !zoneNames eval FLNN for all from !allZones 
    !this.lst.dtext = !zoneNames 
    !this.lst.rtext = !allZones
endmethod

define method .SetupMenu()
    !this.lst.setPopup(!this.ZoneMenu)
endmethod

define method .ShowData( !event is string)
    !selectedElement = !this.lst.selection(|RTEXT|)
    !dbref = object dbref(!selectedElement)
    q var !dbref.$!event
endmethod
```

Key Point's to remember,
- `<ListGadget>.setPopup(!this.<MenuName>)` Method is used to setup popup menu.

## File Browser Object

```
setup form !!FileBrowserForm resize
    !this.formTitle = |File Browser Form|
    button .open |Open| linklabel callback |!this.OpenFileChangeText()| width 10
    path right
    hdist 1
    text .txtp || width 50 is string 
exit
 
define method .FileBrowserForm()

endmethod

define method .OpenFileChangeText()
    !!fileBrowser('c:\','*','Open File', true ,'!!FileBrowserForm.ChangeText()')
endmethod

define method .ChangeText()
    q var !!fileBrowser.file
    !this.txtp.val = !!fileBrowser.file.string()
endmethod
```

Syntax for File Browser,
```
!!fileBrowser(!directory is STRING, !seedFile is STRING, !title is STRING, !existFlag is BOOLEAN, !callback is STRING)
```
Where,
- `!directory` : Origin directory
- `!seedFile` : Seed Filename
- `!title` : Form title string
- `!existFlag` : True if file must exist
- `!callback` : Callback assigned to OK button

Detailed implimentation for the file browser is done using `.Net`/ `PMLNet` callable library. To know the syntax for the same get the function file path using `!!pml.getpathname('filebrowser.pmlfnc')`.

## Event Driven Graphics (EDG)

EDG is used to interact with 3D view/ Volume view. The functionality allows user to select elements form the 3D Canvas/ View.

```
setup form !!EDGForm resize
    !this.formTitle = |EDG Form|
    !this.initCall = |!this.init()|
    button .BuAdd |Add Equipment| linklabel callback |!this.GetEdgData()| width 10
    path down
    list .lst |All Equipments| callback |!this.SetupMenu()| width 50
    member .selection is array
exit
 
define method .EDGForm()
    
endmethod

define method .init()
    !emptyData = object array()
    !this.lst.val = !emptyData
endmethod

define method .SetData()
    !existingData = !!EDGForm.lst.rtext
    do !val values !!EDGForm.selection
        q var !val
        !name = name of equi of $!val
        q var !name
        !existingData.append( !name )
    enddo
    !!EDGForm.lst.dtext = !existingData
    !!EDGForm.lst.rtext = !existingData
endmethod

define method .GetEdgData()
  !packet = object EDGPACKET()
  !packet.elementPick(|Pick Equipments <esc> to add to list|)
  !packet.description = |Select Equipment|
  !packet.action = |!!EDGForm.StoreSelection(!this.return[1].item)|
  !packet.close = |!!EDGForm.SetData()|
  !!EDGCntrl.add(!packet)
endmethod

define method .StoreSelection( !pickedElement is dbref)
    $p Piecked Element
    q var !pickedElement
    !!EDGForm.selection.clear()
    !index = !pickedElement.ahlist.findfirst(|EQUI|)
    if (not unset(!index)) then
        !!EDGForm.selection.append(!pickedElement)
    endif
    !!EDGForm.lst.refresh()
endmethod
```

## Tree View

