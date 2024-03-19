# Enigma
This repository offers a suite of tools related to the Enigma cipher machine used by the German military in World War II.  It includes a historically accurate emulator and (eventually) a tool oriented toward cracking the Enigma encryption.

Python file "enigma" is the emulator.  It's built with the Python package argparse and supports integrated help (./enigma -h).  All of the configuration settings can be supplied from the command line, but the program also supports an auto (-a, --auto) option which will cause it to take settings from a "code sheet" file, selecting the configuration that matches the current day of the month.

The fully manual mode looks like this:

./enigma -p 'plug config' -r 'rotor config' -u 'ukw/reflector config' -s 'start position' 'text'

Automated mode uses a variant of the actual German "per message start position" procedure.  To send a message using auto mode, type

./enigma -a -s 'start' 'text'

The program will use the start position specified in the code sheet file for the current day to encrypt your 'start' parameter.  The result will form the first characters of the encrypted output.  Then it sets the rotor positions to match your 'start' parameter and encrypts 'text' from there, appending it to the encrypted output.

To decrypt such a result, type

./enigma -a 'text'

where 'text' is the result of the auto encryption process just described.  The program will use the code sheet start position for the day to decrypt the first characters of the message (this might be either three or four characters, depending on your machine configuration).  It then uses that result to set the rotor position and decrypts the remainder of 'text' from there.  The results of this second decryption are printed - you will not actually see the decrypted message start position.

The program offers a debug mode which will cause a quite verbose description of the detailed internal operation of the machine, character by character.  This is triggered  with -d or --debug.  The debug info is written to stderr, which you can re-direct to a file:

./enigma -d -a -s 'start' 'text' 2>debug.txt

A series of historical Enigma sample messages are available online here:

http://wiki.franklinheath.co.uk/index.php/Enigma/Sample_Messages

and the decryptions of these are found here:

http://wiki.franklinheath.co.uk/index.php/Enigma/Sample_Decrypts

I'm not sure how to handle the "Turing Treatise" item, and the "Enigma Tirpitz, 1944" item seems to involve some strange special case manual manipulation of the leftmost ring - the program doesn't know how to handle that.  On all of the other items, though, it produces correct results.
