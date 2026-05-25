# man security

```text
security(1)                 General Commands Manual                security(1)

NNAAMMEE
     sseeccuurriittyy – Command line interface to keychains and Security framework

SSYYNNOOPPSSIISS
     sseeccuurriittyy [--hhiillqqvv] [--pp _p_r_o_m_p_t] [_c_o_m_m_a_n_d] [_c_o_m_m_a_n_d___o_p_t_i_o_n_s] [_c_o_m_m_a_n_d___a_r_g_s]

DDEESSCCRRIIPPTTIIOONN
     A simple command line interface which lets you administer keychains,
     manipulate keys and certificates, and do just about anything the Security
     framework is capable of from the command line.

     By default sseeccuurriittyy will execute the _c_o_m_m_a_n_d supplied and report if
     anything went wrong.

     If the --ii or --pp options are provided, sseeccuurriittyy will enter interactive
     mode and allow the user to enter multiple commands on stdin.  When EOF is
     read from stdin sseeccuurriittyy will exit.

     Here is a complete list of the options available:

     --hh       If no arguments are specified, show a list of all commands.  If
              arguments are provided, show usage for each the specified
              commands.  This option is essentially the same as the hheellpp
              command.

     --ii       Run sseeccuurriittyy in interactive mode.  A prompt (security> by
              default) will be displayed and the user will be able to type
              commands on stdin until an EOF is encountered.

     --ll       Before sseeccuurriittyy exits, run
                    /usr/bin/leaks -nocontext
              on itself to see if the command(s) you executed had any leaks.

     --pp _p_r_o_m_p_t
              This option implies the --ii option but changes the default prompt
              to the argument specified instead.

     --qq       Will make sseeccuurriittyy less verbose.

     --vv       Will make sseeccuurriittyy more verbose.

SSEECCUURRIITTYY CCOOMMMMAANNDD SSUUMMMMAARRYY
     sseeccuurriittyy provides a rich variety of commands (_c_o_m_m_a_n_d in the _S_Y_N_O_P_S_I_S),
     each of which often has a wealth of options, to allow access to the broad
     functionality provided by the Security framework.  However, you don't
     have to master every detail for sseeccuurriittyy to be useful to you.

     Here are brief descriptions of all the sseeccuurriittyy commands:

     hheellpp                        Show all commands, or show usage for a
                                 command.
     lliisstt--kkeeyycchhaaiinnss              Display or manipulate the keychain search
                                 list.
     ddeeffaauulltt--kkeeyycchhaaiinn            Display or set the default keychain.
     llooggiinn--kkeeyycchhaaiinn              Display or set the login keychain.
     ccrreeaattee--kkeeyycchhaaiinn             Create keychains.
     ddeelleettee--kkeeyycchhaaiinn             Delete keychains and remove them from the
                                 search list.
     lloocckk--kkeeyycchhaaiinn               Lock the specified keychain.
     uunnlloocckk--kkeeyycchhaaiinn             Unlock the specified keychain.
     sseett--kkeeyycchhaaiinn--sseettttiinnggss       Set settings for a keychain.
     sseett--kkeeyycchhaaiinn--ppaasssswwoorrdd       Set password for a keychain.
     sshhooww--kkeeyycchhaaiinn--iinnffoo          Show the settings for keychain.
     dduummpp--kkeeyycchhaaiinn               Dump the contents of one or more keychains.
     ccrreeaattee--kkeeyyppaaiirr              Create an asymmetric key pair.
     aadddd--ggeenneerriicc--ppaasssswwoorrdd        Add a generic password item.
     aadddd--iinntteerrnneett--ppaasssswwoorrdd       Add an internet password item.
     aadddd--cceerrttiiffiiccaatteess            Add certificates to a keychain.
     ffiinndd--ggeenneerriicc--ppaasssswwoorrdd       Find a generic password item.
     ddeelleettee--ggeenneerriicc--ppaasssswwoorrdd     Delete a generic password item.
     sseett--ggeenneerriicc--ppaasssswwoorrdd--ppaarrttiittiioonn--lliisstt
                                 Set the partition list of a generic password
                                 item.
     ffiinndd--iinntteerrnneett--ppaasssswwoorrdd      Find an internet password item.
     ddeelleettee--iinntteerrnneett--ppaasssswwoorrdd    Delete an internet password item.
     sseett--iinntteerrnneett--ppaasssswwoorrdd--ppaarrttiittiioonn--lliisstt
                                 Set the partition list of a internet password
                                 item.
     ffiinndd--kkeeyy                    Find keys in the keychain
     sseett--kkeeyy--ppaarrttiittiioonn--lliisstt      Set the partition list of a key.
     ffiinndd--cceerrttiiffiiccaattee            Find a certificate item.
     ffiinndd--iiddeennttiittyy               Find an identity (certificate + private key).
     ddeelleettee--cceerrttiiffiiccaattee          Delete a certificate from a keychain.
     ddeelleettee--iiddeennttiittyy             Delete a certificate and its private key from
                                 a keychain.
     sseett--iiddeennttiittyy--pprreeffeerreennccee     Set the preferred identity to use for a
                                 service.
     ggeett--iiddeennttiittyy--pprreeffeerreennccee     Get the preferred identity to use for a
                                 service.
     ccrreeaattee--ddbb                   Create a db using the DL.
     eexxppoorrtt                      Export items from a keychain.
     iimmppoorrtt                      Import items into a keychain.
     ccmmss                         Encode or decode CMS messages.
     iinnssttaallll--mmddss                 Install (or re-install) the MDS database.
     aadddd--ttrruusstteedd--cceerrtt            Add trusted certificate(s).
     rreemmoovvee--ttrruusstteedd--cceerrtt         Remove trusted certificate(s).
     dduummpp--ttrruusstt--sseettttiinnggss         Display contents of trust settings.
     uusseerr--ttrruusstt--sseettttiinnggss--eennaabbllee  Display or manipulate user-level trust
                                 settings.
     ttrruusstt--sseettttiinnggss--eexxppoorrtt       Export trust settings.
     ttrruusstt--sseettttiinnggss--iimmppoorrtt       Import trust settings.
     vveerriiffyy--cceerrtt                 Verify certificate(s).
     aauutthhoorriizzee                   Perform authorization operations.
     aauutthhoorriizzaattiioonnddbb             Make changes to the authorization policy
                                 database.
     eexxeeccuuttee--wwiitthh--pprriivviilleeggeess     Execute tool with privileges.
     lleeaakkss                       Run _/_u_s_r_/_b_i_n_/_l_e_a_k_s on this process.
     ssmmaarrttccaarrddss                  Enable, disable or list disabled smartcard
                                 tokens.
     lliisstt--ssmmaarrttccaarrddss             Display available smartcards.
     eexxppoorrtt--ssmmaarrttccaarrdd            Export/display items from a smartcard.
     eerrrroorr                       Display a descriptive message for the given
                                 error code(s).

CCOOMMMMOONN CCOOMMMMAANNDD OOPPTTIIOONNSS
     This section describes the _c_o_m_m_a_n_d___o_p_t_i_o_n_s that are available across most
     sseeccuurriittyy commands.

     --hh       Show a usage message for the specified command.  This option is
              essentially the same as the _h_e_l_p command.

SSEECCUURRIITTYY CCOOMMMMAANNDDSS
     Here (finally) are details on all the sseeccuurriittyy commands and the options
     each accepts.

     hheellpp Show all commands, or show usage for a command.

     lliisstt--kkeeyycchhaaiinnss [--hh] [--dd _u_s_e_r|_s_y_s_t_e_m|_c_o_m_m_o_n|_d_y_n_a_m_i_c] [--ss [_k_e_y_c_h_a_i_n_._._.]]
     Display or manipulate the keychain search list.

            --dd _u_s_e_r|_s_y_s_t_e_m|_c_o_m_m_o_n|_d_y_n_a_m_i_c
                     Use the specified preference domain.
            --ss       Set the search list to the specified keychains.

     ddeeffaauulltt--kkeeyycchhaaiinn [--hh] [--dd _u_s_e_r|_s_y_s_t_e_m|_c_o_m_m_o_n|_d_y_n_a_m_i_c] [--ss [_k_e_y_c_h_a_i_n]]
     Display or set the default keychain.

            --dd _u_s_e_r|_s_y_s_t_e_m|_c_o_m_m_o_n|_d_y_n_a_m_i_c
                     Use the specified preference domain.
            --ss       Set the default keychain to the specified _k_e_y_c_h_a_i_n.
                     Unset it if no keychain is specified.

     llooggiinn--kkeeyycchhaaiinn [--hh] [--dd _u_s_e_r|_s_y_s_t_e_m|_c_o_m_m_o_n|_d_y_n_a_m_i_c] [--ss [_k_e_y_c_h_a_i_n]]
     Display or set the login keychain.

            --dd _u_s_e_r|_s_y_s_t_e_m|_c_o_m_m_o_n|_d_y_n_a_m_i_c
                     Use the specified preference domain.
            --ss       Set the login keychain to the specified _k_e_y_c_h_a_i_n.  Unset
                     it if no keychain is specified.

     ccrreeaattee--kkeeyycchhaaiinn [--hhPP] [--pp _p_a_s_s_w_o_r_d] [_k_e_y_c_h_a_i_n_._._.] Create keychains.

            --PP              Prompt the user for a password using the
                            SecurityAgent.
            --pp _p_a_s_s_w_o_r_d     Use _p_a_s_s_w_o_r_d as the password for the keychains
                            being created.

            If neither --PP or --pp _p_a_s_s_w_o_r_d are specified, the user is prompted
            for a password on the command line. Use of the -p option is
            insecure.

     ddeelleettee--kkeeyycchhaaiinn [--hh] [_k_e_y_c_h_a_i_n_._._.] Delete keychains and remove them from
     the search list.

     lloocckk--kkeeyycchhaaiinn [--hh] [--aa|_k_e_y_c_h_a_i_n] Lock _k_e_y_c_h_a_i_n, or the default keychain
     if none is specified.  If the --aa option is specified, all keychains are
     locked.

     uunnlloocckk--kkeeyycchhaaiinn [--hhuu] [--pp _p_a_s_s_w_o_r_d] [_k_e_y_c_h_a_i_n] Unlock _k_e_y_c_h_a_i_n, or the
     default keychain if none is specified.

     sseett--kkeeyycchhaaiinn--sseettttiinnggss [--hhlluu] [--tt _t_i_m_e_o_u_t] [_k_e_y_c_h_a_i_n] Set settings for
     _k_e_y_c_h_a_i_n, or the default keychain if none is specified.

            --ll              Lock keychain when the system sleeps.
            --uu              Lock keychain after timeout interval.
            --tt _t_i_m_e_o_u_t      Specify _t_i_m_e_o_u_t interval in seconds (omitting this
                            option specifies "no timeout").

     sseett--kkeeyycchhaaiinn--ppaasssswwoorrdd [--hh] [--oo _o_l_d_P_a_s_s_w_o_r_d] [--pp _n_e_w_P_a_s_s_w_o_r_d] [_k_e_y_c_h_a_i_n]
     Set password for _k_e_y_c_h_a_i_n, or the default keychain if none is specified.

            --oo _o_l_d_P_a_s_s_w_o_r_d  Old keychain password (if not provided, will
                            prompt)
            --pp _n_e_w_P_a_s_s_w_o_r_d  New keychain password (if not provided, will
                            prompt)

     sshhooww--kkeeyycchhaaiinn--iinnffoo [_k_e_y_c_h_a_i_n] Show the settings for _k_e_y_c_h_a_i_n.

     dduummpp--kkeeyycchhaaiinn [--aaddhhiirr] [_k_e_y_c_h_a_i_n_._._.] Dump the contents of one or more
     keychains.

            --aa              Dump access control list of items
            --dd              Dump (decrypted) data of items
            --ii              Interactive access control list editing mode
            --rr              Dump raw (encrypted) data of items

     ccrreeaattee--kkeeyyppaaiirr [--hh] [--aa _a_l_g] [--ss _s_i_z_e] [--ff _d_a_t_e] [--tt _d_a_t_e] [--dd _d_a_y_s] [--kk
     _k_e_y_c_h_a_i_n] [--AA|--TT _a_p_p_P_a_t_h] [_d_e_s_c_r_i_p_t_i_o_n] Create an asymmetric key pair.

            --aa _a_l_g          Use _a_l_g as the algorithm, can be rsa, dh, dsa or
                            fee (default rsa)
            --ss _s_i_z_e         Specify the keysize in bits (default 512)
            --ff _d_a_t_e         Make a key valid from the specified date (ex:
                            "13/11/10 3:30pm")
            --tt _d_a_t_e         Make a key valid to the specified date
            --dd _d_a_y_s         Make a key valid for the number of days specified
                            from today
            --kk _k_e_y_c_h_a_i_n     Use the specified keychain rather than the default
            --AA              Allow any application to access this key without
                            warning (insecure, not recommended!)
            --TT _a_p_p_P_a_t_h      Specify an application which may access this key
                            (multiple --TT options are allowed)

     aadddd--ggeenneerriicc--ppaasssswwoorrdd [--hh] [--aa _a_c_c_o_u_n_t] [--ss _s_e_r_v_i_c_e] [--ww _p_a_s_s_w_o_r_d]
     [_o_p_t_i_o_n_s_._._.] [--AA|--TT _a_p_p_P_a_t_h] [_k_e_y_c_h_a_i_n] Add a generic password item.

            --aa _a_c_c_o_u_n_t      Specify account name (required)
            --cc _c_r_e_a_t_o_r      Specify item creator (optional four-character
                            code)
            --CC _t_y_p_e         Specify item type (optional four-character code)
            --DD _k_i_n_d         Specify kind (default is "application password")
            --GG _v_a_l_u_e        Specify generic attribute value (optional)
            --jj _c_o_m_m_e_n_t      Specify comment string (optional)
            --ll _l_a_b_e_l        Specify label (if omitted, service name is used as
                            default label)
            --ss _s_e_r_v_i_c_e      Specify service name (required)
            --pp _p_a_s_s_w_o_r_d     Specify password to be added (legacy option,
                            equivalent to --ww)
            --ww _p_a_s_s_w_o_r_d     Specify password to be added. Put at end of
                            command to be prompted (recommended)
            --AA              Allow any application to access this item without
                            warning (insecure, not recommended!)
            --TT _a_p_p_P_a_t_h      Specify an application which may access this item
                            (multiple --TT options are allowed)
            --UU              Update item if it already exists (if omitted, the
                            item cannot already exist)
            --XX _p_a_s_s_w_o_r_d     Specify password data to be added as a hexadecimal
                            string

            By default, the application which creates an item is trusted to
            access its data without warning.  You can remove this default
            access by explicitly specifying an empty app pathname: --TT "". If
            no keychain is specified, the password is added to the default
            keychain.

     aadddd--iinntteerrnneett--ppaasssswwoorrdd [--hh] [--aa _a_c_c_o_u_n_t] [--ss _s_e_r_v_e_r] [--ww _p_a_s_s_w_o_r_d]
     [_o_p_t_i_o_n_s_._._.] [--AA|--TT _a_p_p_P_a_t_h] [_k_e_y_c_h_a_i_n] Add an internet password item.

            --aa _a_c_c_o_u_n_t      Specify account name (required)
            --cc _c_r_e_a_t_o_r      Specify item creator (optional four-character
                            code)
            --CC _t_y_p_e         Specify item type (optional four-character code)
            --dd _d_o_m_a_i_n       Specify security domain string (optional)
            --DD _k_i_n_d         Specify kind (default is "application password")
            --jj _c_o_m_m_e_n_t      Specify comment string (optional)
            --ll _l_a_b_e_l        Specify label (if omitted, service name is used as
                            default label)
            --pp _p_a_t_h         Specify path string (optional)
            --PP _p_o_r_t         Specify port number (optional)
            --rr _p_r_o_t_o_c_o_l     Specify protocol (optional four-character
                            SecProtocolType, e.g. "http", "ftp ")
            --ss _s_e_r_v_e_r       Specify server name (required)
            --tt _a_u_t_h_e_n_t_i_c_a_t_i_o_n_T_y_p_e
                            Specify authentication type (as a four-character
                            SecAuthenticationType, default is "dflt")
            --ww _p_a_s_s_w_o_r_d     Specify password to be added. Put at end of
                            command to be prompted (recommended)
            --AA              Allow any application to access this item without
                            warning (insecure, not recommended!)
            --TT _a_p_p_P_a_t_h      Specify an application which may access this item
                            (multiple --TT options are allowed)
            --UU              Update item if it already exists (if omitted, the
                            item cannot already exist)
            --XX _p_a_s_s_w_o_r_d     Specify password data to be added as a hexadecimal
                            string

            By default, the application which creates an item is trusted to
            access its data without warning.  You can remove this default
            access by explicitly specifying an empty app pathname: --TT "". If
            no keychain is specified, the password is added to the default
            keychain.

     aadddd--cceerrttiiffiiccaatteess [--hh] [--kk _k_e_y_c_h_a_i_n] _f_i_l_e_._._. Add certficates contained in
     the specified _f_i_l_e_s to the default keychain.  The files must contain one
     DER encoded X509 certificate each.
     --kk _k_e_y_c_h_a_i_n     Use _k_e_y_c_h_a_i_n rather than the default keychain.

     ffiinndd--ggeenneerriicc--ppaasssswwoorrdd [--hh] [--aa _a_c_c_o_u_n_t] [--ss _s_e_r_v_i_c_e] [_o_p_t_i_o_n_s_._._.] [--gg]
     [_k_e_y_c_h_a_i_n_._._.] Find a generic password item.

            --aa _a_c_c_o_u_n_t      Match account string
            --cc _c_r_e_a_t_o_r      Match creator (four-character code)
            --CC _t_y_p_e         Match type (four-character code)
            --DD _k_i_n_d         Match kind string
            --GG _v_a_l_u_e        Match value string (generic attribute)
            --jj _c_o_m_m_e_n_t      Match comment string
            --ll _l_a_b_e_l        Match label string
            --ss _s_e_r_v_i_c_e      Match service string
            --gg              Display the password for the item found
            --ww              Display the password(only) for the item found

     ddeelleettee--ggeenneerriicc--ppaasssswwoorrdd [--hh] [--aa _a_c_c_o_u_n_t] [--ss _s_e_r_v_i_c_e] [_o_p_t_i_o_n_s_._._.]
     [_k_e_y_c_h_a_i_n_._._.] Delete a generic password item.

            --aa _a_c_c_o_u_n_t      Match account string
            --cc _c_r_e_a_t_o_r      Match creator (four-character code)
            --CC _t_y_p_e         Match type (four-character code)
            --DD _k_i_n_d         Match kind string
            --GG _v_a_l_u_e        Match value string (generic attribute)
            --jj _c_o_m_m_e_n_t      Match comment string
            --ll _l_a_b_e_l        Match label string
            --ss _s_e_r_v_i_c_e      Match service string

     ddeelleettee--iinntteerrnneett--ppaasssswwoorrdd [--hh] [--aa _a_c_c_o_u_n_t] [--ss _s_e_r_v_e_r] [_o_p_t_i_o_n_s_._._.]
     [_k_e_y_c_h_a_i_n_._._.] Delete an internet password item.

            --aa _a_c_c_o_u_n_t      Match account string
            --cc _c_r_e_a_t_o_r      Match creator (four-character code)
            --CC _t_y_p_e         Match type (four-character code)
            --dd _s_e_c_u_r_i_t_y_D_o_m_a_i_n
                            Match securityDomain string
            --DD _k_i_n_d         Match kind string
            --jj _c_o_m_m_e_n_t      Match comment string
            --ll _l_a_b_e_l        Match label string
            --pp _p_a_t_h         Match path string
            --PP _p_o_r_t         Match port number
            --rr _p_r_o_t_o_c_o_l     Match protocol (four-character code)
            --ss _s_e_r_v_e_r       Match server string
            --tt _a_u_t_h_e_n_t_i_c_a_t_i_o_n_T_y_p_e
                            Match authenticationType (four-character code)

     ffiinndd--iinntteerrnneett--ppaasssswwoorrdd [--hh] [--aa _a_c_c_o_u_n_t] [--ss _s_e_r_v_e_r] [_o_p_t_i_o_n_s_._._.] [--gg]
     [_k_e_y_c_h_a_i_n_._._.] Find an internet password item.

            --aa _a_c_c_o_u_n_t      Match account string
            --cc _c_r_e_a_t_o_r      Match creator (four-character code)
            --CC _t_y_p_e         Match type (four-character code)
            --dd _s_e_c_u_r_i_t_y_D_o_m_a_i_n
                            Match securityDomain string
            --DD _k_i_n_d         Match kind string
            --jj _c_o_m_m_e_n_t      Match comment string
            --ll _l_a_b_e_l        Match label string
            --pp _p_a_t_h         Match path string
            --PP _p_o_r_t         Match port number
            --rr _p_r_o_t_o_c_o_l     Match protocol (four-character code)
            --ss _s_e_r_v_e_r       Match server string
            --tt _a_u_t_h_e_n_t_i_c_a_t_i_o_n_T_y_p_e
                            Match authenticationType (four-character code)
            --gg              Display the password for the item found
            --ww              Display the password(only) for the item found

     ffiinndd--kkeeyy [_o_p_t_i_o_n_s_._._.] [_k_e_y_c_h_a_i_n_._._.] Search the keychain for keys.

            --aa _a_p_p_l_i_c_a_t_i_o_n_-_l_a_b_e_l
                            Match "application label" string
            --cc _c_r_e_a_t_o_r      Match creator (four-character code)
            --dd              Match keys that can decrypt
            --DD _d_e_s_c_r_i_p_t_i_o_n  Match "description" string
            --ee              Match keys that can encrypt
            --jj _c_o_m_m_e_n_t      Match comment string
            --ll _l_a_b_e_l        Match label string
            --rr              Match keys that can derive
            --ss              Match keys that can sign
            --tt _t_y_p_e         Type of key to find: one of "symmetric", "public",
                            or "private"
            --uu              Match keys that can unwrap
            --vv              Match keys that can verify
            --ww              Match keys that can wrap

     sseett--ggeenneerriicc--ppaasssswwoorrdd--ppaarrttiittiioonn--lliisstt [--aa _a_c_c_o_u_n_t] [--ss _s_e_r_v_i_c_e] [--SS
     _p_a_r_t_i_t_i_o_n_-_l_i_s_t] [--kk _p_a_s_s_w_o_r_d] [_o_p_t_i_o_n_s_._._.] [_k_e_y_c_h_a_i_n] Sets the "partition
     list" for a generic password. The "partition list" is an extra parameter
     in the ACL which limits access to the item based on an application's code
     signature. You must present the keychain's password to change a partition
     list.

            --SS _p_a_r_t_i_t_i_o_n_-_l_i_s_t
                            Comma-separated partition list. See output of
                            "security dump-keychain" for examples.
            --kk _p_a_s_s_w_o_r_d     Password for keychain (deprecated)
            --aa _a_c_c_o_u_n_t      Match account string
            --cc _c_r_e_a_t_o_r      Match creator (four-character code)
            --CC _t_y_p_e         Match type (four-character code)
            --DD _k_i_n_d         Match kind string
            --GG _v_a_l_u_e        Match value string (generic attribute)
            --jj _c_o_m_m_e_n_t      Match comment string
            --ll _l_a_b_e_l        Match label string
            --ss _s_e_r_v_i_c_e      Match service string

     sseett--iinntteerrnneett--ppaasssswwoorrdd--ppaarrttiittiioonn--lliisstt [--aa _a_c_c_o_u_n_t] [--ss _s_e_r_v_e_r] [--SS
     _p_a_r_t_i_t_i_o_n_-_l_i_s_t] [--kk _p_a_s_s_w_o_r_d] [_o_p_t_i_o_n_s_._._.] [_k_e_y_c_h_a_i_n] Sets the "partition
     list" for an internet password. The "partition list" is an extra
     parameter in the ACL which limits access to the item based on an
     application's code signature. You must present the keychain's password to
     change a partition list.

            --SS _p_a_r_t_i_t_i_o_n_-_l_i_s_t
                            Comma-separated partition list. See output of
                            "security dump-keychain" for examples.
            --kk _p_a_s_s_w_o_r_d     Password for keychain (deprecated)
            --aa _a_c_c_o_u_n_t      Match account string
            --cc _c_r_e_a_t_o_r      Match creator (four-character code)
            --CC _t_y_p_e         Match type (four-character code)
            --dd _s_e_c_u_r_i_t_y_D_o_m_a_i_n
                            Match securityDomain string
            --DD _k_i_n_d         Match kind string
            --jj _c_o_m_m_e_n_t      Match comment string
            --ll _l_a_b_e_l        Match label string
            --pp _p_a_t_h         Match path string
            --PP _p_o_r_t         Match port number
            --rr _p_r_o_t_o_c_o_l     Match protocol (four-character code)
            --ss _s_e_r_v_e_r       Match server string
            --tt _a_u_t_h_e_n_t_i_c_a_t_i_o_n_T_y_p_e
                            Match authenticationType (four-character code)

     sseett--kkeeyy--ppaarrttiittiioonn--lliisstt [--SS _p_a_r_t_i_t_i_o_n_-_l_i_s_t] [--kk _p_a_s_s_w_o_r_d] [_o_p_t_i_o_n_s_._._.]
     [_k_e_y_c_h_a_i_n] Sets the "partition list" for a key. The "partition list" is
     an extra parameter in the ACL which limits access to the key based on an
     application's code signature. You must present the keychain's password to
     change a partition list. If you'd like to run /usr/bin/codesign with the
     key, "apple:" must be an element of the partition list.

            --SS _p_a_r_t_i_t_i_o_n_-_l_i_s_t
                            Comma-separated partition list. See output of
                            "security dump-keychain" for examples.
            --kk _p_a_s_s_w_o_r_d     Password for keychain (deprecated)
            --aa _a_p_p_l_i_c_a_t_i_o_n_-_l_a_b_e_l
                            Match "application label" string
            --cc _c_r_e_a_t_o_r      Match creator (four-character code)
            --dd              Match keys that can decrypt
            --DD _d_e_s_c_r_i_p_t_i_o_n  Match "description" string
            --ee              Match keys that can encrypt
            --jj _c_o_m_m_e_n_t      Match comment string
            --ll _l_a_b_e_l        Match label string
            --rr              Match keys that can derive
            --ss              Match keys that can sign
            --tt _t_y_p_e         Type of key to find: one of "symmetric", "public",
                            or "private"
            --uu              Match keys that can unwrap
            --vv              Match keys that can verify
            --ww              Match keys that can wrap

     ffiinndd--cceerrttiiffiiccaattee [--hh] [--aa] [--cc _n_a_m_e] [--ee _e_m_a_i_l_A_d_d_r_e_s_s] [--mm] [--pp] [--ZZ]
     [_k_e_y_c_h_a_i_n_._._.] Find a certificate item.  If no _k_e_y_c_h_a_i_n arguments are
     provided, the default search list is used.

            Options:
            --aa              Find all matching certificates, not just the first
                            one
            --cc _n_a_m_e         Match on _n_a_m_e when searching (optional)
            --ee _e_m_a_i_l_A_d_d_r_e_s_s
                            Match on _e_m_a_i_l_A_d_d_r_e_s_s when searching (optional)
            --mm              Show the email addresses in the certificate
            --pp              Output certificate in pem format.  Default is to
                            dump the attributes and keychain the cert is in.
            --ZZ              Print SHA-256 (and SHA-1) hash of the certificate

            EExxaammpplleess

            security> find-certificate -a -p > allcerts.pem
                     Exports all certificates from all keychains into a pem
                     file called allcerts.pem.

            security> find-certificate -a -e me@foo.com -p > certs.pem
                     Exports all certificates from all keychains with the
                     email address me@foo.com into a pem file called
                     certs.pem.

            security> find-certificate -a -c MyName -Z login.keychain | grep
                     ^SHA-256
                     Print the SHA-256 hash of every certificate in
                     'login.keychain' whose common name includes 'MyName'

     ffiinndd--iiddeennttiittyy [--hh] [--pp _p_o_l_i_c_y] [--ss _s_t_r_i_n_g] [--vv] [_k_e_y_c_h_a_i_n_._._.] Find an
     identity (certificate + private key) satisfying a given policy. If no
     _p_o_l_i_c_y arguments are provided, the X.509 basic policy is assumed. If no
     _k_e_y_c_h_a_i_n arguments are provided, the default search list is used.

            Options:
            --pp _p_o_l_i_c_y       Specify _p_o_l_i_c_y to evaluate (multiple -p options
                            are allowed). Supported policies: basic, ssl-
                            client, ssl-server, smime, eap, ipsec, ichat,
                            codesigning, sys-default, sys-kerberos-kdc
            --ss _s_t_r_i_n_g       Specify optional policy-specific _s_t_r_i_n_g (e.g. a
                            DNS hostname for SSL, or RFC822 email address for
                            S/MIME)
            --vv              Show valid identities only (default is to show all
                            identities)

            EExxaammpplleess

            security> find-identity -v -p ssl-client
                     Display valid identities that can be used for SSL client
                     authentication

            security> find-identity -p ssl-server -s www.domain.com
                     Display identities for a SSL server running on the host
                     'www.domain.com'

            security> find-identity -p smime -s user@domain.com
                     Display identities that can be used to sign a message
                     from 'user@domain.com'

     ddeelleettee--cceerrttiiffiiccaattee [--hh] [--cc _n_a_m_e] [--ZZ _h_a_s_h] [--tt] [_k_e_y_c_h_a_i_n_._._.] Delete a
     certificate from a keychain.  If no _k_e_y_c_h_a_i_n arguments are provided, the
     default search list is used.

            --cc _n_a_m_e         Specify certificate to delete by its common name
            --ZZ _h_a_s_h         Specify certificate to delete by its SHA-256 (or
                            SHA-1) hash
            --tt              Also delete user trust settings for this
                            certificate

            The certificate to be deleted must be uniquely specified either by
            a string found in its common name, or by its SHA-256 (or SHA-1)
            hash.

     ddeelleettee--iiddeennttiittyy [--hh] [--cc _n_a_m_e] [--ZZ _h_a_s_h] [--tt] [_k_e_y_c_h_a_i_n_._._.] Delete a
     certificate and its private key from a keychain.  If no _k_e_y_c_h_a_i_n
     arguments are provided, the default search list is used.

            --cc _n_a_m_e         Specify certificate to delete by its common name
            --ZZ _h_a_s_h         Specify certificate to delete by its SHA-256 (or
                            SHA-1) hash
            --tt              Also delete user trust settings for this identity
                            certificate

            The identity to be deleted must be uniquely specified either by a
            string found in its common name, or by its SHA-256 (or SHA-1)
            hash.

     sseett--iiddeennttiittyy--pprreeffeerreennccee [--hh] [--nn] [--cc _i_d_e_n_t_i_t_y] [--ss _s_e_r_v_i_c_e] [--uu
     _k_e_y_U_s_a_g_e] [--ZZ _h_a_s_h] [_k_e_y_c_h_a_i_n_._._.] Set the preferred identity to use for a
     service.

            --nn              Specify no identity (clears existing preference
                            for the given service)
            --cc _i_d_e_n_t_i_t_y     Specify identity by common name of the certificate
            --ss _s_e_r_v_i_c_e      Specify service (may be a URL, RFC822 email
                            address, DNS host, or other name) for which this
                            identity is to be preferred
            --uu _k_e_y_U_s_a_g_e     Specify key usage (optional)
            --ZZ _h_a_s_h         Specify identity by SHA-256 (or SHA-1) hash of
                            certificate (optional)

            The identity is located by searching the specified keychain(s) for
            a certificate whose common name contains the given identity
            string. If no keychains are specified to search, the default
            search list is used. Different identity preferences can be set for
            individual key usages. You can differentiate between two
            identities which contain the same string by providing a SHA-256
            (or SHA-1) hash of the certificate in addition to, or instead of,
            the name.

            PPAARRTTIIAALL PPAATTHHSS AANNDD WWIILLDDCCAARRDDSS

            Prior to 10.5.4, identity preferences for SSL/TLS client
            authentication could only be set on a per-URL basis. The URL being
            visited had to match the service name exactly for the preference
            to be in effect.

            In 10.5.4, it became possible to specify identity preferences on a
            per-server basis, by using a service name with a partial path URL
            to match more specific paths on the same server. For example, if
            an identity preference for "https://www.apache-ssl.org/" exists,
            it will be in effect for "https://www.apache-ssl.org/cgi/cert-
            export", and so on. Note that partial path URLs must end with a
            trailing slash character.

            Starting with 10.6, it is possible to specify identity preferences
            on a per-domain basis, by using the wildcard character '*' as the
            leftmost component of the service name. Unlike SSL wildcards, an
            identity preference wildcard can match more than one subdomain.
            For example, an identity preference for the name "*.army.mil" will
            match "server1.subdomain1.army.mil" or
            "server2.subdomain2.army.mil". Likewise, a preference for "*.mil"
            will match both "server.army.mil" and "server.navy.mil".

            KKEEYY UUSSAAGGEE CCOODDEESS

                 0 - preference is in effect for all possible key usages
            (default)
                 1 - encryption only
                 2 - decryption only
                 4 - signing only
                 8 - signature verification only
                16 - signing with message recovery only
                32 - signature verification with message recovery only
                64 - key wrapping only
               128 - key unwrapping only
               256 - key derivation only

            To specify more than one usage, add values together.

     ggeett--iiddeennttiittyy--pprreeffeerreennccee [--hh] [--ss _s_e_r_v_i_c_e] [--uu _k_e_y_U_s_a_g_e] [--pp] [--cc] [--ZZ]
     Get the preferred identity to use for a service.

            --ss _s_e_r_v_i_c_e      Specify service (may be a URL, RFC822 email
                            address, DNS host, or other name)
            --uu _k_e_y_U_s_a_g_e     Specify key usage (optional)
            --pp              Output identity certificate in pem format
            --cc              Print common name of the preferred identity
                            certificate
            --ZZ              Print SHA-256 (and SHA-1) hash of the preferred
                            identity certificate

     ccrreeaattee--ddbb [--aahhoo00] [--gg _d_l|_c_s_p_d_l] [--mm _m_o_d_e] [_n_a_m_e] Create a db using the
     DL.  If _n_a_m_e isn't provided sseeccuurriittyy will prompt the user to type a name.

            Options:
            --aa              Turn off autocommit
            --gg _d_l|_c_s_p_d_l     Use the AppleDL (default) or AppleCspDL
            --mm _m_o_d_e         Set the file permissions to _m_o_d_e.
            --oo              Force using openparams argument
            --00              Force using version 0 openparams

            EExxaammpplleess

            security> create-db -m 0644 test.db

            security> create-db -g cspdl -a test2.db

     eexxppoorrtt [--kk _k_e_y_c_h_a_i_n] [--tt _t_y_p_e] [--ff _f_o_r_m_a_t] [--ww] [--pp] [--PP _p_a_s_s_p_h_r_a_s_e] [--oo
     _o_u_t_f_i_l_e] Export one or more items from a keychain to one of a number of
     external representations.  If _k_e_y_c_h_a_i_n isn't provided, items will be
     exported from the user's default keychain.

            Options:
            --kk _k_e_y_c_h_a_i_n     Specify keychain from which item(s) will be
                            exported.
            --tt _t_y_p_e         Specify the type of items to export. Possible
                            types are certs, allKeys, pubKeys, privKeys,
                            identities, and all. The default is all. An
                            identity consists of both a certificate and the
                            corresponding private key.
            --ff _f_o_r_m_a_t       Specify the format of the exported data. Possible
                            formats are openssl, bsafe, pkcs7, pkcs8, pkcs12,
                            x509, openssh1, openssh2, and pemseq. The default
                            is pemseq if more than one item is being exported.
                            The default is openssl if one key is being
                            exported. The default is x509 if one certificate
                            is being exported.
            --ww              Specifies that private keys are to be wrapped on
                            export.
            --pp              Specifies that PEM armour is to be applied to the
                            output data.
            --PP _p_a_s_s_p_h_r_a_s_e   Specify the wrapping passphrase immediately. The
                            default is to obtain a secure passphrase via GUI.
            --oo _o_u_t_f_i_l_e      Write the output data to _o_u_t_f_i_l_e. Default is to
                            write data to stdout.

            EExxaammpplleess

            security> export -k login.keychain -t certs -o /tmp/certs.pem

            security> export -k newcert.keychain -t identities -f pkcs12 -o
                     /tmp/mycerts.p12

     iimmppoorrtt inputfile [--kk _k_e_y_c_h_a_i_n] [--tt _t_y_p_e] [--ff _f_o_r_m_a_t] [--ww] [--PP _p_a_s_s_p_h_r_a_s_e]
     [_o_p_t_i_o_n_s_._._.] Import one or more items from _i_n_p_u_t_f_i_l_e into a keychain. If
     _k_e_y_c_h_a_i_n isn't provided, items will be imported into the user's default
     keychain.

            Options:
            --kk _k_e_y_c_h_a_i_n     Specify keychain into which item(s) will be
                            imported.
            --tt _t_y_p_e         Specify the type of items to import. Possible
                            types are cert, pub, priv, session, cert, and agg.
                            Pub, priv, and session refer to keys; agg is one
                            of the aggregate types (pkcs12 and PEM sequence).
                            The command can often figure out what item_type an
                            item contains based in the filename and/or
                            item_format.
            --ff _f_o_r_m_a_t       Specify the format of the exported data. Possible
                            formats are openssl, bsafe, raw, pkcs7, pkcs8,
                            pkcs12, x509, openssh1, openssh2, and pemseq. The
                            command can often figure out what format an item
                            is in based in the filename and/or item_type.
            --ww              Specify that private keys are wrapped and must be
                            unwrapped on import.
            --xx              Specify that private keys are non-extractable
                            after being imported.
            --PP _p_a_s_s_p_h_r_a_s_e   Specify the unwrapping passphrase immediately. The
                            default is to obtain a secure passphrase via GUI.
            --aa _a_t_t_r_N_a_m_e _a_t_t_r_V_a_l_u_e
                            Specify optional extended attribute name and
                            value. Can be used multiple times. This is only
                            valid when importing keys.
            --AA              Allow any application to access the imported key
                            without warning (insecure, not recommended!)
            --TT _a_p_p_P_a_t_h      Specify an application which may access the
                            imported key (multiple --TT options are allowed)

            EExxaammpplleess

            security> import /tmp/certs.pem -k

            security> import /tmp/mycerts.p12 -t agg -k newcert.keychain

            security> import /tmp/mycerts.p12 -f pkcs12 -k newcert.keychain

     ccmmss [--CC|--DD|--EE|--SS] [_o_p_t_i_o_n_s_._._.] Encode or decode CMS messages.
     --CC              create a CMS encrypted message
     --DD              decode a CMS message
     --EE              create a CMS enveloped message
     --SS              create a CMS signed message

            Decoding options:
            --cc _c_o_n_t_e_n_t      use this detached content file
            --hh _l_e_v_e_l        generate email headers with info about CMS message
                            (output _l_e_v_e_l >= 0)
            --nn              suppress output of content

            Encoding options:
            --rr _i_d_,_._._.       create envelope for comma-delimited list of
                            recipients, where id can be a certificate nickname
                            or email address
            --GG              include a signing time attribute
            --HH _h_a_s_h         hash = MD2|MD4|MD5|SHA1|SHA256|SHA384|SHA512
                            (default: SHA1)
            --NN _n_i_c_k         use certificate named "nick" for signing
            --PP              include a SMIMECapabilities attribute
            --TT              do not include content in CMS message
            --YY _n_i_c_k         include an EncryptionKeyPreference attribute with
                            certificate (use "NONE" to omit)
            --ZZ _h_a_s_h         find a certificate by subject key ID

            Common options:
            --ee _e_n_v_e_l_o_p_e     specify envelope file (valid with --DD or --EE)
            --kk _k_e_y_c_h_a_i_n     specify keychain to use
            --ii _i_n_f_i_l_e       use infile as source of data (default: stdin)
            --oo _o_u_t_f_i_l_e      use outfile as destination of data (default:
                            stdout)
            --pp _p_a_s_s_w_o_r_d     use password as key db password (default: prompt)
            --ss              pass data a single byte at a time to CMS
            --uu _c_e_r_t_u_s_a_g_e    set type of certificate usage (default:
                            certUsageEmailSigner)
            --vv              print debugging information

            Cert usage codes:
                              0 - certUsageSSLClient
                              1 - certUsageSSLServer
                              2 - certUsageSSLServerWithStepUp
                              3 - certUsageSSLCA
                              4 - certUsageEmailSigner
                              5 - certUsageEmailRecipient
                              6 - certUsageObjectSigner
                              7 - certUsageUserCertImport
                              8 - certUsageVerifyCA
                              9 - certUsageProtectedObjectSigner
                             10 - certUsageStatusResponder
                             11 - certUsageAnyCA


     iinnssttaallll--mmddss Install (or re-install) the Module Directory Services (MDS)
     database. This is a system tool which is not normally used by users.
     There are no options.

     aadddd--ttrruusstteedd--cceerrtt [--dd] [--rr _r_e_s_u_l_t_T_y_p_e] [--pp _p_o_l_i_c_y] [--aa _a_p_p_P_a_t_h] [--ss
     _p_o_l_i_c_y_S_t_r_i_n_g] [--ee _a_l_l_o_w_e_d_E_r_r_o_r] [--uu _k_e_y_U_s_a_g_e] [--kk _k_e_y_c_h_a_i_n] [--ii
     _s_e_t_t_i_n_g_s_F_i_l_e_I_n] [--oo _s_e_t_t_i_n_g_s_F_i_l_e_O_u_t] [_c_e_r_t_F_i_l_e] Add certificate (in DER
     or PEM format) from _c_e_r_t_F_i_l_e to per-user or local Admin Trust Settings.
     When modifying per-user Trust Settings, user authentication is required
     via an authentication dialog. When modifying admin Trust Settings, the
     process must be running as root, or admin authentication is required.

            Options:
            --dd              Add to admin cert store; default is user.
            --rr _r_e_s_u_l_t_T_y_p_e   resultType =
                            trustRoot|trustAsRoot|deny|unspecified; default is
                            trustRoot.
            --pp _p_o_l_i_c_y       Specify policy constraint (ssl, smime, codeSign,
                            IPSec, basic, swUpdate, pkgSign, eap, macappstore,
                            appleID, timestamping).
            --aa _a_p_p_P_a_t_h      Specify application constraint.
            --ss _p_o_l_i_c_y_S_t_r_i_n_g
                            Specify policy-specific string.
            --ee _a_l_l_o_w_e_d_E_r_r_o_r
                            Specify allowed error (an integer value, or one
                            of: certExpired, hostnameMismatch)
            --uu _k_e_y_U_s_a_g_e     Specify key usage, an integer.
            --kk _k_e_y_c_h_a_i_n     Specify keychain to which cert is added.
            --ii _s_e_t_t_i_n_g_s_F_i_l_e_I_n
                            Input trust settings file; default is user domain.
            --oo _s_e_t_t_i_n_g_s_F_i_l_e_O_u_t
                            Output trust settings file; default is user
                            domain.

            KKeeyy uussaaggee ccooddeess::
                -1 - Any
                 1 - Sign
                 2 - Encrypt/Decrypt Data
                 4 - Encrypt/Decrypt Key
                 8 - Sign certificate
                16 - Sign revocation
                32 - Key exchange
                To specify more than one usage, add values together (except -1
            - Any).

            EExxaammpplleess
                  security> add-trusted-cert /tmp/cert.der
                  security> add-trusted-cert -d .tmp/cert.der

     rreemmoovvee--ttrruusstteedd--cceerrtt [--dd] certFile Remove certificate (in DER or PEM
     format) in _c_e_r_t_F_i_l_e from per-user or local Admin Trust Settings. When
     modifying per-user Trust Settings, user authentication is required via an
     authentication dialog. When modifying admin Trust Settings, the process
     must be running as root, or admin authentication is required.

            Options:
            --dd              Remove from admin cert store; default is user.

     dduummpp--ttrruusstt--sseettttiinnggss [--ss] [--dd] Display Trust Settings.

            Options:
            --ss              Display trusted system certs; default is user.
            --dd              Display trusted admin certs; default is user.

     uusseerr--ttrruusstt--sseettttiinnggss--eennaabbllee [--dd] [--ee] Display or manipulate user-level
     Trust Settings. With no arguments, shows the current state of the user-
     level Trust Settings enable. Otherwise enables or disables user-level
     Trust Settings.

            Options:
            --dd              Disable user-level Trust Settings.
            --ee              Enable user-level Trust Settings.

     ttrruusstt--sseettttiinnggss--eexxppoorrtt [--ss] [--dd] settings_file Export Trust Settings to
     the specified file.

            Options:
            --ss              Export system Trust Settings; default is user.
            --dd              Export admin Trust Settings; default is user.

     ttrruusstt--sseettttiinnggss--iimmppoorrtt [--dd] settings_file Import Trust Settings from the
     specified file. When modifying per-user Trust Settings, user
     authentication is required via an authentication dialog. When modifying
     admin Trust Settings, the process must be running as root, or admin
     authentication is required.

            Options:
            --dd              Import admin Trust Settings; default is user.

     vveerriiffyy--cceerrtt [_o_p_t_i_o_n_s_._._.] [_u_r_l] Verify one or more certificates. If a
     direct URL argument is provided, a TLS connection is attempted and the
     certificate presented by that server is evaluated according to standard
     SSL server policy; other certificates or policy options will be ignored
     in this case.

            Options:
            --cc _c_e_r_t_F_i_l_e     Certificate to verify, in DER or PEM format. Can
                            be specified more than once; leaf certificate has
                            to be specified first.
            --rr _r_o_o_t_C_e_r_t_F_i_l_e
                            Root certificate, in DER or PEM format. Can be
                            specified more than once. If not specified, the
                            system anchor certificates are used. If one root
                            certificate is specified, and zero (non-root)
                            certificates are specified, the root certificate
                            is verified against itself.
            --pp _p_o_l_i_c_y       Specify verification policy (ssl, smime, codeSign,
                            IPSec, basic, swUpdate, pkgSign, eap, appleID,
                            macappstore, timestamping). Default is basic.
            --CC              Specify this evaluation is for client usage, if
                            the verification policy (e.g. ssl) distinguishes
                            between client and server usage. Default is server
                            usage.
            --dd _d_a_t_e         Date to set for verification. Specified in the
                            format of YYYY-MM-DD-hh:mm:ss (time optional).
                            e.g: 2016-04-25-15:59:59 for April 25, 2016 at
                            3:59:59 pm in GMT
            --kk _k_e_y_c_h_a_i_n     Keychain to search for intermediate CA
                            certificates. Can be specified multiple times.
                            Default is the current user's keychain search
                            list.
            --nn _n_a_m_e         Specify a name to be verified, e.g. the SSL host
                            name for the ssl policy, or RFC822 email address
                            for the smime policy. For backward compatibility,
                            if the -n option is provided without an argument,
                            it will be interpreted as equivalent to -N.
            --NN              Avoid searching any keychains.
            --LL              Use local certificates only. If an issuing CA
                            certificate is missing, this option will avoid
                            accessing the network to fetch it.
            --ll              Specifies that the leaf certificate is a CA cert.
                            By default, a leaf certificate with a Basic
                            Constraints extension with the CA bit set fails
                            verification.
            --ee _e_m_a_i_l_A_d_d_r_e_s_s
                            Specify email address for the smime policy. (This
                            option is deprecated; use -n instead.)
            --ss _s_s_l_H_o_s_t      Specify SSL host name for the ssl policy. (This
                            option is deprecated; use -n instead.)
            --qq              Quiet, no stdout or stderr.
            --RR _r_e_v_C_h_e_c_k_O_p_t_i_o_n
                            Specify a revocation checking option for this
                            evaluation (ocsp, require, offline). Can be
                            specified multiple times; e.g. to enable
                            revocation checking via the OCSP method and
                            require a positive response, use "-R ocsp -R
                            require". The offline option will consult
                            previously cached responses, but will not make a
                            request to a revocation server.
            --PP              Output the constructed certificate chain in PEM
                            format.
            --tt              Output certificate contents as text.
            --vv              Specify verbose output, including per-certificate
                            trust results.

            EExxaammpplleess

            security> verify-cert -c applestore0.cer -c applestore1.cer -p ssl
                     -n store.apple.com

            security> verify-cert -r serverbasic.crt

            security> verify-cert -v https://www.apple.com

     aauutthhoorriizzee [_o_p_t_i_o_n_s_._._.] _r_i_g_h_t_._._. Authorize requested right(s).  The
     extend-rights flag will be passed by default.

            Options:
            --uu              Allow user interaction.
            --pp              Allow returning partial rights.
            --dd              Destroy acquired rights.
            --PP              Pre-authorize rights only.
            --ll              Operate authorization in least privileged mode.
            --ii              Internalize authref passed on stdin.
            --ee              Externalize authref to stdout
            --ww              Wait while holding AuthorizationRef until stdout
                            is closed. This will allow client to read
                            externalized AuthorizationRef from pipe.

            EExxaammpplleess

            security> security authorize -ud my-right
                     Basic authorization of my-right.

            security> security -q authorize -uew my-right | security -q
                     authorize -i my-right
                     Authorizing a right and passing it to another command as
                     a way to add authorization to shell scripts.

     aauutthhoorriizzaattiioonnddbb _r_e_a_d _<_r_i_g_h_t_-_n_a_m_e_>

     aauutthhoorriizzaattiioonnddbb _w_r_i_t_e _<_r_i_g_h_t_-_n_a_m_e_> _[_a_l_l_o_w_|_d_e_n_y_|_<_r_u_l_e_n_a_m_e_>_]

     aauutthhoorriizzaattiioonnddbb _r_e_m_o_v_e _<_r_i_g_h_t_-_n_a_m_e_> Read/Modify authorization policy
     database. Without a rulename write will read a dictionary as a plist from
     stdin.

            EExxaammpplleess

            security> security authorizationdb read system.privilege.admin >
                     /tmp/aewp-def
                     Read definition of system.privilege.admin right.

            security> security authorizationdb write system.preferences <
                     /tmp/aewp-def
                     Set system.preferences to definition of
                     system.privilege.admin right.

            security> security authorizationdb write system.preferences
                     authenticate-admin
                     Every change to preferences requires an Admin user to
                     authenticate.

     eexxeeccuuttee--wwiitthh--pprriivviilleeggeess _<_p_r_o_g_r_a_m_> [_a_r_g_s_._._.] Execute tool with privileges.
     On success stdin will be read and forwarded to the tool.

     lleeaakkss [--ccyycclleess] [--nnooccoonntteexxtt] [--nnoossttaacckkss] [--eexxcclluuddee _s_y_m_b_o_l] Run
     /usr/bin/leaks on this process.  This can help find memory leaks after
     running certain commands.

            Options:
            --ccyycclleess         Use a stricter algorithm (See leaks(1) for
                            details).
            --nnooccoonntteexxtt      Withhold the hex dumps of the leaked memory.
            --nnoossttaacckkss       Don't show stack traces of leaked memory.
            --eexxcclluuddee _s_y_m_b_o_l
                            Ignore leaks called from _s_y_m_b_o_l.

     ssmmaarrttccaarrddss _t_o_k_e_n [--ll] [--ee _t_o_k_e_n] [--dd _t_o_k_e_n] Enable, disable or list
     disabled smartcard tokens.

            Options:
            --ll              List disabled smartcard tokens.
            --ee _t_o_k_e_n        Enable smartcard token.
            --dd _t_o_k_e_n        Disable smartcard token.

            TToo lliisstt ttookkeennss aavvaaiillaabbllee iinn tthhee ssyysstteemm

            pluginkit -m -p com.apple.ctk-tokens

            EExxaammpplleess

            security smartcards token -l
            security smartcards token -d com.apple.CryptoTokenKit.pivtoken
            security smartcards token -e com.apple.CryptoTokenKit.pivtoken

     lliisstt--ssmmaarrttccaarrddss Display _i_ds of available smartcards.

     eexxppoorrtt--ssmmaarrttccaarrdd _t_o_k_e_n [--ii _i_d] [--tt _t_y_p_e] [--ee _e_x_p_o_r_t_P_a_t_h] Export/display
     items from a smartcard. If _i_d isn't provided, items from all smartcards
     will be displayed.

            Options:
            --ii _i_d           Export/display items from token specified by token
                            _i_d, available _i_ds can be listed by list-smartcards
                            command.
            --tt _c_e_r_t_s|_p_r_i_v_K_e_y_s|_i_d_e_n_t_i_t_i_e_s|_a_l_l
                            Display items of the specified type (Default: _a_l_l)
            --ee _e_x_p_o_r_t_P_a_t_h   Specify path to export certificates and public
                            keys. If _e_x_p_o_r_t_P_a_t_h
                             is specified screen output is suppressed. This
                            option cannot be combined with -t option.

     eerrrroorr [_e_r_r_o_r_-_c_o_d_e_._._.] Display an error string for the given security-
     related error code.  The error can be in decimal or hex, e.g. 1234 or
     0x1234. Multiple errors can be separated by spaces.

EENNVVIIRROONNMMEENNTT
     MallocStackLogging
              When using the lleeaakkss command or the --ll option it's probably a
              good idea to set this environment variable before sseeccuurriittyy is
              started.  Doing so will allow leaks to display symbolic
              backtraces.

FFIILLEESS
     _~_/_L_i_b_r_a_r_y_/_P_r_e_f_e_r_e_n_c_e_s_/_c_o_m_._a_p_p_l_e_._s_e_c_u_r_i_t_y_._p_l_i_s_t

              Property list file containing the current user's default
              keychain and keychain search list.

     _/_L_i_b_r_a_r_y_/_P_r_e_f_e_r_e_n_c_e_s_/_c_o_m_._a_p_p_l_e_._s_e_c_u_r_i_t_y_._p_l_i_s_t

              Property list file containing the system default keychain and
              keychain search list.  This is used by processes started at boot
              time, or those requesting to use the system search domain, such
              as system daemons.

     _/_L_i_b_r_a_r_y_/_P_r_e_f_e_r_e_n_c_e_s_/_c_o_m_._a_p_p_l_e_._s_e_c_u_r_i_t_y_-_c_o_m_m_o_n_._p_l_i_s_t

              Property list file containing the common keychain search list,
              which is appended to every user's search list and to the system
              search list.

SSEEEE AALLSSOO
     certtool(1), leaks(1), pluginkit(8)

HHIISSTTOORRYY
     sseeccuurriittyy was first introduced in Mac OS X version 10.3.

BBUUGGSS
     sseeccuurriittyy still needs more commands before it can be considered complete.
     In particular, it should someday supersede both the certtool and
     systemkeychain commands.

Darwin                         January 17, 2024                         Darwin

```
