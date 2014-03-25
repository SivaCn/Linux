FIX KEYBOARD MAPPING:
---------------------

Change keyboard mapping to US

  $ setxkbmap us



FIX VLC SIZZLING NOISE:
-----------------------

    It's not just a problem with Skype, I believe it's a problem with, you've guessed it, PulseAudio.

    Workaround? Indeed there is.

    Disabling PulseAudio's Glitch Free Audio seems to have solved the crackling
    for me (which became unbearable on Ubuntu 12.10 Beta 2)

    To do this, edit the /etc/pulse/default.pa file in your favourite text editor.

    Search for the following line:

    load-module module-hal-detect

    and append "tsched=0" to the end:

    load-module module-hal-detect tsched=0

    restart pulse (or just reboot your system), and the crackling should be gone.

    Not sure what the side effects are by disabling Glitch Free Audio, but I can't seem to find any yet.

    UPDATE: If you don't have a line with load-module module-hal-detect, then search for following line:

    load-module module-udev-detect

    and append "tsched=0" to the end:

    load-module module-udev-detect tsched=0

    restart pulse (or just reboot your system), and the crackling should be gone.


        Thanks a lot, it helped at least 5 people, unfortunately not me :-(. There is
        no load-module module-hal-detect in the file /etc/pulse/default.p on my system.
        The closest are the lines ### Use the static hardware detection module (for
        systems that lack udev/hal support) load-module module-detect, so I added
        tsched=0 to the last line. But no change. I added another line with load-module
        module-hal-detect tsched=0 and then with the same line, but deleted load-module
        module-detect, too. Unfortunately all this did not let disappear any sizzling
        after restart. Any tip left? –  Filbuntu Oct 19 '12 at 7:32

        try replacing that whole section with the following: ### Automatically load
        driver modules depending on the hardware available .ifexists
        module-udev-detect.so load-module module-udev-detect tsched=0 .else ### Use the
        static hardware detection module (for systems that lack udev/hal support)
        load-module module-detect .endif –  Robert Ian Hawdon Oct 19 '12 at 22:51

        I tried again, just added tsched=0 to the line with module-udev-detect and it
        works (hopefully for ever :-). Before I copied & pasted what you wrote, but
        probably some spaces at the end of the lines or something else I missed caused
        me to have no sound ("dummy output" & no input). –  Filbuntu Oct 20 '12 at 2:37


  For the whole post Please Check:

    http://askubuntu.com/questions/157891/skype-and-vlc-sounds-sizzle-distorted-bad
