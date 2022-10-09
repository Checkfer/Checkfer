#include <GDIPlus.au3>
#include <GUIConstantsEx.au3>

Example()

Func Example()
        Local $hGUI, $hGraphic, $hBrush, $hFormat, $hFamily, $hFont, $tLayout, $aInfo
        Local $sString = "Hello"

        ; Create GUI
        $hGUI = GUICreate("GDI+", 400, 300)
		GUISetBkColor(0x123456, $hGUI)
    $ExStyle = GUIGetStyle($hGUI)[1]
    GUISetStyle(-1, BitAND($ExStyle, 0x80000) = 0x80000 ? $ExStyle : $ExStyle + 0x80000, $hGUI)
    DllCall("user32.dll", "bool", "SetLayeredWindowAttributes", "hwnd", $hGUI, "INT", 0x563412, "byte", 255, "dword", 0x03)
GUISetState(@SW_SHOW)
        GUISetState(@SW_SHOW)

        ; Draw a string
        _GDIPlus_Startup()
        $hGraphic = _GDIPlus_GraphicsCreateFromHWND($hGUI)
        $hBrush = _GDIPlus_BrushCreateSolid(0xFFFF0000)
        $hFormat = _GDIPlus_StringFormatCreate()
        $hFamily = _GDIPlus_FontFamilyCreate("Arial")
        $hFont = _GDIPlus_FontCreate($hFamily, 50, 2)
        $tLayout = _GDIPlus_RectFCreate(140, 110, 0, 0)
        $aInfo = _GDIPlus_GraphicsMeasureString($hGraphic, $sString, $hFont, $tLayout, $hFormat)
        _GDIPlus_GraphicsDrawStringEx($hGraphic, $sString, $hFont, $aInfo[0], $hFormat, $hBrush)

        ; Loop until the user exits.
        Do
        Until GUIGetMsg() = $GUI_EVENT_CLOSE

        ; Clean up resources
        _GDIPlus_FontDispose($hFont)
        _GDIPlus_FontFamilyDispose($hFamily)
        _GDIPlus_StringFormatDispose($hFormat)
        _GDIPlus_BrushDispose($hBrush)
        _GDIPlus_GraphicsDispose($hGraphic)
        _GDIPlus_Shutdown()
EndFunc   ;==>Example
