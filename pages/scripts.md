# [↩](https://aledua.github.io/)

## <center>Scripts</center>
<center>This script was created as an automation tool for transcription tasks on a simple transcription platform. Its functions include creating keyboard shortcuts, inserting tags for categorizing various sound elements (conversation participants, background sounds, specific menu items from the store), adjusting the page to speed up the time between tasks, automating audio playback, and inserting timestamps, all while utilizing the available buttons on the screen and mouse movements.
Additionally, it generates a minimalist overlay window on the page with a timer that automatically starts after each task, accompanied by a sound alert when the time limit is reached, as well as adding to a counter the total number of completed tasks.
</center>

&nbsp;

![tool](./tool.png)

<div style="max-height: 200px; overflow-y: auto; padding: 10px; border: 1px solid #ccc; border-radius: 5px; white-space: pre-wrap; word-wrap: break-word;">
`
#NoEnv    
#SingleInstance, Force
SetBatchLines, -1  
#MaxThreadsBuffer Off
#MaxThreadsPerHotkey 1
; ---------------------- PROJECT CODE BELOW ----------------------
Menu, Tray, Icon, Shell32.dll, 3 ; Custom Icon pulled from Shell32
Menu, tray, tip, %A_ScriptName% ; Custom traytip
Count := 0
~PgDn::
send, {PgDn}
number_loops := 6
loop, %number_loops%
{
Send, {WheelDown}
sleep, 200
}
; Trigger hotkey
    timerCount := 60 ; Change me
    Count := Count + 1
    Gosub, Sub_ShowOverlay
return
; Creates and shows the GUI
Sub_ShowOverlay:
    Gui, GUI_Overlay:New, +ToolWindow  +LastFound +AlwaysOnTop -Caption +hwndGUI_Overlay_hwnd
    Gui, Margin, 10, 10
    Gui, Font, s30 q4, Segoe UI Bold
    Gui, Add, Text, w400 Center vTEXT_Timer cWhite, %timerCount% seconds (%Count%)
    
    Gui, Color, 000000
    WinSet, Transparent, 200
    Gui, Show, Hide, Overlay
    WinMove, 2670, 157 ; Change these values to move the window original 750
    Gui, GUI_Overlay:Show
    SetTimer, Timer_Countdown, 1000
return
; Does the countdown and updating of the timer
Timer_Countdown:
    if (timerCount == 1) {
        SetTimer, Timer_Countdown, Off
        SoundPlay, fail.wav
        Gui, GUI_Overlay:Destroy
    }
    timerCount--
    GuiControl, GUI_Overlay:, TEXT_Timer, %timerCount% seconds (%Count%)
    
    
return
#MaxThreadsBuffer Off
#MaxThreadsPerHotkey 1
#SingleInstance force
;SetMouseDelay,-1 ;remove delays from mouse actions
Process, Priority,, High

!LButton::
KeyWait, LAlt
send, ^b
MouseGetPos, StartX, StartY
;sleep, 50
MouseMove, 0, -125, 0, R
;sleep, 50
MouseGetPos, FirstX, FirstY
MouseMove, 410, FirstY, 0
send, {Click}
sleep, 100
send, {LControl down}
sleep, 100
send, !r
send, {LControl up}
MouseMove, StartX, StartY, 0
return
*LShift::
send, {LControl down}
send, !i
send, {LControl up}
return
*1::
MouseMove, 0, 80, 0, R
send, ^b
MouseMove, 0, -80, 0, R
;sleep, 50
KeyWait, LButton, D
KeyWait, LButton
sleep, 50
send, {Tab}
sleep, 50
send, {LControl down}
sleep, 100
send, !p
send, {LControl up}
return
*2::
MouseMove, 0, 80, 0, R
send, ^b
MouseMove, 0, -80, 0, R
;sleep, 50
KeyWait, LButton, D
KeyWait, LButton
sleep, 50
send, {Tab}
sleep, 50
send, {LControl down}
sleep, 100
send, !n
send, {LControl up}
return
*3::
MouseMove, 0, 80, 0, R
send, ^b
MouseMove, 0, -80, 0, R
;sleep, 50
KeyWait, LButton, D
KeyWait, LButton
sleep, 50
send, {Tab}
sleep, 50
send, {LControl down}
sleep, 100
send, !u
send, {LControl up}
return
*4::
MouseMove, 0, 80, 0, R
send, ^b
MouseMove, 0, -80, 0, R
;sleep, 50
KeyWait, LButton, D
KeyWait, LButton
sleep, 50
send, {Tab}
sleep, 50
send, {LControl down}
sleep, 100
send, !t
send, {LControl up}
return
*5::
MouseMove, 0, 80, 0, R
send, ^b
MouseMove, 0, -80, 0, R
;sleep, 50
KeyWait, LButton, D
KeyWait, LButton
send, {Tab}
sleep, 50
send, {LControl down}
sleep, 100
send, !r
send, {LControl up}
return
*!1::
send, {backspace 3}
send, {LControl down}
sleep, 100
send, !p
send, {LControl up}
return
*!2::
send, {backspace 3}
send, {LControl down}
sleep, 100
send, !n
send, {LControl up}
return
*!3::
send, {backspace 3}
send, {LControl down}
sleep, 100
send, !u
send, {LControl up}
return
*!4::
send, {backspace 3}
send, {LControl down}
sleep, 100
send, !t
send, {LControl up}
return
*!5::
send, {backspace 3}
send, {LControl down}
sleep, 100
send, !r
send, {LControl up}
return
*6::
send, {LControl down}
sleep, 100
send, !h
send, {LControl up}
return
*7::
Send, {space 2}
Send, {Rshift down}
Send, {left 2}
Send, {Rshift up}
Send, {LControl down}
send, !c
send, {LControl up}
Send, {left 3}
Send, {Rshift down}
Send, {left 1}
Send, {Rshift up}
Send, {space}
return
*8::
send, {LControl down}
sleep, 100
send, !k
send, {LControl up}
return
*9::
send, {LControl down}
sleep, 100
send, !l
send, {LControl up}
return
*!n::
send, ñ
return
*!m::
send, ma'am
send, {space}
return
*!,::
send, -edited-
send, {space}
return
*!.::
send, welcome to -edited- will you be using your mobile app today?
send, {space}
return
*!/::
send, if your order is correct on your screen please move forward thank you.
send, {space}
return

:*?:'a::{Asc 0225}
return
:*?:'e::{Asc 0233}
return
:*?:'i::{Asc 0237}
return
:*?:'o::{Asc 0243}
return
:*?:'u::{Asc 0250}
return
`
</div>
