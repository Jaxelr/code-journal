# Disable capslock

Taken from this [answer](https://answers.microsoft.com/en-us/windows/forum/all/disable-caps-lock-key/8083d4ee-721d-463f-aeda-630cd7f047c3)


1. Open an editor
1. Paste to the editor this:

```
        Windows Registry Editor Version 5.00

        [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout]
        "Scancode Map"=hex:00,00,00,00,00,00,00,00,02,00,00,00,00,00,3a,00,00,00,00,00
```

1. File > Save As...
    Select for Save as type: All Files
    Enter in the File name field: disable_caps_lock.reg
    Click Save 
1. Right click on the created file > Merge
1. Restart your system 


In the case that you want to enable CAPS LOCK again, you need to delete that registry entry, so you need follow these steps:

1. Press WinKey+R > type regedit and press Enter
1. Navigate to HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout
1. Right click on the Scancode Map > Delete
1. Restart your system 
