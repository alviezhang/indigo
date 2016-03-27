---
layout: post
title: Poker II交换Alt与Win
tags: "OS X"
blog: true
---

[之前](/2015/09/osx-swap-fn-and-control/)有设置交换MacBook内建键盘的Fn与Crtl键，但是如果同时使用外接键盘，外接键盘的Ctrl键就会不能使用。Poker II上的Alt与Meta键是反的，我也只希望交换这款键盘的键位。还好Karabiner足够强大，网上搜了下就搞定了。

获取Poker II与MacBook内建键盘`VendorID`与`ProductID`的命令如下：

    ioreg -n IOHIDKeyboard -r | grep -e 'class IOHIDKeyboard' -e VendorID\" -e Product

完成的`private.xml`：

~~~ xml
<?xml version="1.0"?>
<root>
    <item>
        <name>For POKER II</name>
        <devicevendordef>
            <vendorname>POKER_CORP</vendorname>
            <vendorid>0x0f39</vendorid>
        </devicevendordef>
        <deviceproductdef>
            <productname>POKER_II</productname>
            <productid>0x0611</productid>
        </deviceproductdef>
        <item>
            <name>swapLeftCommandAndleftAlt</name>
            <identifier>private.pkSwapLeftCommandAndleftAlt</identifier>
            <device_only>DeviceVendor::POKER_CORP, DeviceProduct::POKER_II</device_only>
            <autogen>__KeyToKey__ KeyCode::COMMAND_L, KeyCode::OPTION_L</autogen>
            <autogen>__KeyToKey__ KeyCode::OPTION_L, KeyCode::COMMAND_L</autogen>
        </item>
        <item>
            <name>rightAltToRightCommand</name>
            <identifier>private.pkRightAltToLeftCommand</identifier>
            <device_only>DeviceVendor::POKER_CORP, DeviceProduct::POKER_II</device_only>
            <autogen>__KeyToKey__ KeyCode::OPTION_R, KeyCode::COMMAND_R</autogen>
        </item>
        <item>
            <name>rightCtrlToRightArrow</name>
            <identifier>private.pkRightCtrlToRightArrow</identifier>
            <device_only>DeviceVendor::POKER_CORP, DeviceProduct::POKER_II</device_only>
            <autogen>__KeyToKey__ KeyCode::CONTROL_R, KeyCode::CURSOR_RIGHT</autogen>
        </item>
        <item>
            <name>changeEscToTilde</name>
            <identifier>private.pkChangeEscToTilde</identifier>
            <device_only>DeviceVendor::POKER_CORP, DeviceProduct::POKER_II</device_only>
            <autogen>__KeyToKey__ KeyCode::ESCAPE, KeyCode::BACKQUOTE</autogen>
        </item>
    </item>
    <item>
        <name>For Macbook Pro Early 2015</name>
        <devicevendordef>
            <vendorname>APPLE_INC</vendorname>
            <vendorid>0x5ac</vendorid>
        </devicevendordef>
        <deviceproductdef>
            <productname>APPLE_INTERNAL_KEYBOARD</productname>
            <productid>0x273</productid>
        </deviceproductdef>
        <item>
            <name>leftControlToFn</name>
            <identifier>private.appleInternalLeftControlToFn</identifier>
            <device_only>DeviceVendor::APPLE_INC, DeviceProduct::APPLE_INTERNAL_KEYBOARD</device_only>
            <!--Swap Fn and Left Control-->
            <autogen>__KeyToKey__ KeyCode::FN, KeyCode::CONTROL_L</autogen>
            <autogen>__KeyToKey__ KeyCode::CONTROL_L, KeyCode::FN</autogen>
            <!--Fn+Functional Keys to F1..F12-->
            <autogen>__KeyToKey__ ConsumerKeyCode::BRIGHTNESS_DOWN, ModifierFlag::FN, KeyCode::F1</autogen>
            <autogen>__KeyToKey__ KeyCode::BRIGHTNESS_DOWN,         ModifierFlag::FN, KeyCode::F1</autogen>
            <autogen>__KeyToKey__ ConsumerKeyCode::BRIGHTNESS_UP,   ModifierFlag::FN, KeyCode::F2</autogen>
            <autogen>__KeyToKey__ KeyCode::BRIGHTNESS_UP,           ModifierFlag::FN, KeyCode::F2</autogen>
            <autogen>__KeyToKey__ KeyCode::EXPOSE_ALL, ModifierFlag::FN, KeyCode::F3</autogen>
            <autogen>__KeyToKey__ KeyCode::DASHBOARD,  ModifierFlag::FN, KeyCode::F4</autogen>
            <autogen>__KeyToKey__ KeyCode::LAUNCHPAD,  ModifierFlag::FN, KeyCode::F4</autogen>
            <autogen>__KeyToKey__ ConsumerKeyCode::KEYBOARDLIGHT_LOW,  ModifierFlag::FN, KeyCode::F5</autogen>
            <autogen>__KeyToKey__ ConsumerKeyCode::KEYBOARDLIGHT_HIGH, ModifierFlag::FN, KeyCode::F6</autogen>
            <autogen>__KeyToKey__ ConsumerKeyCode::MUSIC_PREV, ModifierFlag::FN, KeyCode::F7</autogen>
            <autogen>__KeyToKey__ ConsumerKeyCode::MUSIC_PLAY, ModifierFlag::FN, KeyCode::F8</autogen>
            <autogen>__KeyToKey__ ConsumerKeyCode::MUSIC_NEXT, ModifierFlag::FN, KeyCode::F9</autogen>
            <autogen>__KeyToKey__ ConsumerKeyCode::VOLUME_MUTE, ModifierFlag::FN, KeyCode::F10</autogen>
            <autogen>__KeyToKey__ ConsumerKeyCode::VOLUME_DOWN, ModifierFlag::FN, KeyCode::F11</autogen>
            <autogen>__KeyToKey__ ConsumerKeyCode::VOLUME_UP,   ModifierFlag::FN, KeyCode::F12</autogen>
        </item>
    </item>
</root>
~~~



参考链接：

<http://apple.stackexchange.com/a/88096>

<http://qiita.com/MagicKyle/items/097f9fc10eb520f07f42>

<https://raw.githubusercontent.com/599316527/my-karabiner-configuration/master/private.xml>

