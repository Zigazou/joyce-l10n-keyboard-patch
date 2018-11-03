joyce-l10n-keyboard-patch
=========================

The `joyce-l10n-keyboard.patch` is a patch to apply to the Amstrad PCW emulator
from John Elliott, Joyce.

How to apply the patch
----------------------

This patch has been tested against Joyce v2.2.12. You need Joyce sources.

    # Download Joyce Unix sources
    wget http://www.seasip.info/Unix/Joyce/joyce-2.2.12.tar.gz

    # Extract the Joyce archive
    tar xzvf joyce-2.2.12.tar.gz

    # Enter the directory
    cd joyce-2.2.12

Copy `joyce-l10n-keyboard.patch` in the `joyce-2.2.12` directory.

You then need to use the Linux `patch` command.

    # Patch JoycePcwKeyboard.cxx
    patch bin/JoycePcwKeyboard.cxx joyce-l10n-keyboard.patch

You can now proceed with the standard way of compiling under Linux.

    sh configure.sh
    make
    sudo make install

Why this patch?
---------------

Joyce considers the keyboard to be the default PC keyboard which causes problem
with localized keyboards, such as french keyboard, when you use the localized
version of PCW CP/M Plus or LocoScript in the emulator.

Joyce is not affected by the Gnome keyboard mapping. This means you usually
would have to use `setxkbmap` to have a correct keyboard mapping:

    # Use the default PC keyboard layout
    setxkbmap us

    # Use the localized french keyboard layout
    setxkbmap fr -variant oss

But `setxkbmap` works globally. You have to switch back and forth between the
layouts using command line.

The patch forces Joyce to use keyboard scancodes instead of SDL key symbols by
providing a key map from scancodes to SDL key symbols.

