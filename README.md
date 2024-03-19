# Enigma
This repository offers a suite of tools related to the Enigma cipher machine used by the German military in World War II.  It includes a historically accurate emulator and (eventually) a tool oriented toward cracking the Enigma encryption.

Python file "enigma" is the emulator.  It's built with the Python package argparse and supports integrated help (./enigma -h).  All of the configuration settings can be supplied from the command line, but the program also supports an auto (-a, --auto) option which will cause it to take settings from a "code sheet" file, selecting the configuration that matches the current day of the month.

The fully manual mode looks like this:

./enigma -p 'plug config' -r 'rotor config' -u 'ukw/reflector config' -s 'start position' 'text'

