# 1. Introduction
Programmable Macro Language(PML) is basically used with all AVEVA Products where AVEVA has provided the commandline interface. Following is the poduct list where PML implimentation can be obsurved extensively,
    
    -- AVEVA Administration
        -- Lexicon
        -- Administrator
        -- Monitor
    -- AVEVA Everything 3D (new version of AVEVA Plant Design Management System)
        -- Model (new version of Design)
        -- IsoDraft
        -- Draw (new version of Draft)
        -- Specon
        -- Propcon
        -- Catalogue (new version of Paragon)
        -- Spooler
    -- AVEVA Engineering 
        -- Tags
        -- Configuration
    -- AVEVA Diagrams

Because of the following advantages of PML, It is so popular and strong in the plant design,
1. PML is case insensitive language.
2. PML has capability to direcly interact with the AVEVA database in the form of commands.
3. Forms(UI) can be designed with same PML language and it can direcly interacts with the user controlers.
4. PML can be extend with PML.net support.
5. PML is supporting OOP and It's interpreted language similar to Python, js.
6. Core PML Language structure is upgraded in such a way that it supports backward & forward compatibiliy of the code. In other words, you can use the same code written for the newer version in older version and vice a versa.
7. Code having same logical evaluation can be used across all the AVEVA Modules. E.g. A object written for the Design can be used in catalogue as well.

There are some disadvantages as follows,
1. Threading or parallel Processing/computation is not possible.
2. As PML Runs always in one thread, It's very slow. PML is slow in comparion with other languages.
3. PML can't combined with all other languages easily (Except C#.net).
4. It's limited to AVEVA Only. and Very less documentation is available which can describe the exect behavior of PML.

Even after having these pro/cons, use case of the PML is charm and user friendly. So, Let's go to the next chapter.