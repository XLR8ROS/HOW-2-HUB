# man plutil

```text
PLUTIL(1)                   General Commands Manual                  PLUTIL(1)

NNAAMMEE
     pplluuttiill – property list utility

SSYYNNOOPPSSIISS
     pplluuttiill [command_option] [other_options] _f_i_l_e
             ...

DDEESSCCRRIIPPTTIIOONN
     pplluuttiill can be used to check the syntax of property list files, or convert
     a plist file from one format to another.  Specifying - as an input file
     reads from stdin.

     The first argument indicates the operation to perform, one of:

     --hheellpp         Show the usage information for the command and exit.

     --pp            Print the property list in a human-readable fashion. The
                   output format is not stable and not designed for machine
                   parsing. The purpose of this command is to be able to
                   easily read the contents of a plist file, no matter what
                   format it is in.

     --lliinntt         Check the named property list files for syntax errors.
                   This is the default command option if none is specified.

     --ccoonnvveerrtt _f_m_t  Convert the named _f_i_l_e to the indicated format and write
                   back to the file system.  If the file can't be loaded due
                   to invalid syntax, the operation fails. This is the only
                   option to support oobbjjcc sswwiifftt formats.

     --ccoonnvveerrtt _o_b_j_c --hheeaaddeerr
                   Converts the named file to Obj-C literal syntax and creates
                   a _._h file. Useful for first time conversions to literal
                   syntax and only supported with the oobbjjcc format.

     --iinnsseerrtt _k_e_y_p_a_t_h --_t_y_p_e [_v_a_l_u_e] [--aappppeenndd]
                   Insert a value into the property list before writing it
                   out.  _v_a_l_u_e is required unless _t_y_p_e is ddiiccttiioonnaarryy or aarrrraayy.
                   If --aappppeenndd is specified, _k_e_y_p_a_t_h is expected to reference
                   an array and the value will be appended to the end of the
                   array.

     --rreeppllaaccee _k_e_y_p_a_t_h --_t_y_p_e _v_a_l_u_e
                   Overwrite an existing value in the property list before
                   writing it out.

     --rreemmoovvee _k_e_y_p_a_t_h
                   Removes the value at _k_e_y_p_a_t_h from the property list before
                   writing it out.

     --eexxttrraacctt _k_e_y_p_a_t_h _f_m_t [--eexxppeecctt _e_x_p_e_c_t___t_y_p_e]
                   Outputs the value at _k_e_y_p_a_t_h in the property list as a new
                   plist of type _f_m_t.  Optionally fails if --eexxppeecctt _e_x_p_e_c_t___t_y_p_e
                   is used and the value at _k_e_y_p_a_t_h does not match that type.

     --ttyyppee _k_e_y_p_a_t_h [--eexxppeecctt _e_x_p_e_c_t___t_y_p_e]
                   Outputs the type of the value at _k_e_y_p_a_t_h in the property
                   list. Optionally fails if --eexxppeecctt _e_x_p_e_c_t___t_y_p_e is used and
                   the value at _k_e_y_p_a_t_h does not match that type.

     --ccrreeaattee _f_m_t   Creates an empty plist of the specified _f_m_t.

     There are a few additional options:

     ----            Specifies that all further arguments are file names

     --nn            When used with --eexxttrraacctt using the rraaww format, will not
                   print a terminating newline character. This aids use in
                   shell interpolation.

     --ss            Don't print anything on success.

     --rr            For JSON, add whitespace and indentation to make the output
                   more human-readable and sort the keys like --pp, does.

     --oo _p_a_t_h       Specify an alternate path name for the result of the
                   _-_c_o_n_v_e_r_t operation; this option is only useful with a
                   single file to be converted.  Specifying - as the path
                   outputs to stdout.

     --ee _e_x_t_e_n_s_i_o_n  Specify an alternate extension for converted files, and the
                   output file names are otherwise the same.

AARRGGUUMMEENNTTSS
     _f_m_t is one of:
           xxmmll11     for version 1 of the XML plist format
           bbiinnaarryy11  for version 1 of the binary plist format
           jjssoonn     for the JSON format
           sswwiifftt    to convert from plist to swift literal syntax
           oobbjjcc     to convert from plist to Obj-C literal syntax
           rraaww      when used with --eexxttrraacctt, will print the unencapsulated
                    value at the keypath. See RRAAWW VVAALLUUEESS AANNDD EEXXPPEECCTTEEDD TTYYPPEESS
                    below. The result will be output to stdout unless --oo is
                    specified.

     _k_e_y_p_a_t_h is a key-value coding key path, with one extension: a numerical
     path component applied to an array will act on the object at that index
     in the array or insert it into the array if the numerical path component
     is the last one in the key path.

     _t_y_p_e is one of:
            --bbooooll        YES if passed "YES" or "true", otherwise NO
            --iinntteeggeerr     any valid 64 bit integer
            --ffllooaatt       any valid 64 bit float
            --ssttrriinngg      UTF8 encoded string
            --ddaattee        date in XML property list format, not supported if
                         outputting JSON
            --ddaattaa        a base-64 encoded string
            --xxmmll         an XML property list, useful for inserting compound
                         values
            --jjssoonn        JSON fragment, useful for inserting compound values
            --aarrrraayy       An empty array, when used with --iinnsseerrtt.  Does not
                         accept a _v_a_l_u_e.
            --ddiiccttiioonnaarryy  An empty dictionary, when used with --iinnsseerrtt Does not
                         accept a _v_a_l_u_e.

     _v_a_l_u_e will be assigned to the _k_e_y_p_a_t_h specified with the --iinnsseerrtt or
     --rreeppllaaccee flags.

RRAAWW VVAALLUUEESS AANNDD EEXXPPEECCTTEEDD TTYYPPEESS
     With --eexxttrraacctt _k_e_y_p_a_t_h rraaww the value printed depends on its type.

     Following are the possible _e_x_p_e_c_t___t_y_p_e values and how they will be
     printed when encountered with --eexxttrraacctt _k_e_y_p_a_t_h rraaww
            bbooooll         the string "true" or "false"
            iinntteeggeerr      the numeric value
            ffllooaatt        the floating point value with no specific precision
            ssttrriinngg       the raw unescaped string, UTF8-encoded
            ddaattee         the RFC3339-encoded string representation in UTC time
                         zone
            ddaattaa         a base64-encoded string representation of the data
            aarrrraayy        a number indicating the count of elements in the
                         array
            ddiiccttiioonnaarryy   each key in the dictionary will be printed on a new
                         line in alpha-sorted order
     The above _e_x_p_e_c_t___t_y_p_e string is itself printed when --ttyyppee _k_e_y_p_a_t_h is
     used.

DDIIAAGGNNOOSSTTIICCSS
     The pplluuttiill command exits 0 on success, and 1 on failure.

SSEEEE AALLSSOO
     plist(5)

SSTTAANNDDAARRDDSS
     The pplluuttiill command obeys no one's rules but its own.

HHIISSTTOORRYY
     The pplluuttiill command first appeared in macOS 10.2.

     The rraaww format type, --ttyyppee command, --eexxppeecctt option, and --aappppeenndd option
     first appeared in macOS 12.

macOS                           March 29, 2021                           macOS

```
