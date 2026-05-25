# man chown

```text
CHOWN(8)                    System Manager's Manual                   CHOWN(8)

NNAAMMEE
     cchhoowwnn – change file owner and group

SSYYNNOOPPSSIISS
     cchhoowwnn [--ffhhnnvvxx] [--RR [--HH | --LL | --PP]] _o_w_n_e_r[:_g_r_o_u_p] _f_i_l_e _._._.
     cchhoowwnn [--ffhhnnvvxx] [--RR [--HH | --LL | --PP]] :_g_r_o_u_p _f_i_l_e _._._.

DDEESSCCRRIIPPTTIIOONN
     The cchhoowwnn utility changes the user ID and/or the group ID of the
     specified files.  Symbolic links named by arguments are silently left
     unchanged unless --hh is used.

     The options are as follows:

     --HH      If the --RR option is specified, symbolic links on the command line
             are followed and hence unaffected by the command.  (Symbolic
             links encountered during traversal are not followed.)

     --LL      If the --RR option is specified, all symbolic links are followed.

     --PP      If the --RR option is specified, no symbolic links are followed.
             Instead, the user and/or group ID of the link itself are
             modified.  This is the default.  For matching behavior when using
             cchhoowwnn without the --RR option, the --hh option should be used
             instead.

     --RR      Change the user ID and/or the group ID of the file hierarchies
             rooted in the files, instead of just the files themselves.
             Beware of unintentionally matching the “_._.” hard link to the
             parent directory when using wildcards like “.*”.

     --ff      Do not report any failure to change file owner or group, nor
             modify the exit status to reflect such failures.

     --hh      If the file is a symbolic link, change the user ID and/or the
             group ID of the link itself.

     --nn      Interpret user ID and group ID as numeric, avoiding name lookups.

     --vv      Cause cchhoowwnn to be verbose, showing files as the owner is
             modified.  If the --vv flag is specified more than once, cchhoowwnn will
             print the filename, followed by the old and new numeric
             user/group ID.

     --xx      File system mount points are not traversed.

     The --HH, --LL and --PP options are ignored unless the --RR option is specified.
     In addition, these options override each other and the command's actions
     are determined by the last one specified.

     The _o_w_n_e_r and _g_r_o_u_p operands are both optional, however, one must be
     specified.  If the _g_r_o_u_p operand is specified, it must be preceded by a
     colon (``:'') character.

     The _o_w_n_e_r may be either a numeric user ID or a user name.  If a user name
     is also a numeric user ID, the operand is used as a user name.  The _g_r_o_u_p
     may be either a numeric group ID or a group name.  If a group name is
     also a numeric group ID, the operand is used as a group name.

     The ownership of a file may only be altered by a super-user for obvious
     security reasons.  Similarly, only a member of a group can change a
     file's group ID to that group.

     If cchhoowwnn receives a SIGINFO signal (see the ssttaattuuss argument for stty(1)),
     then the current filename as well as the old and new file owner and group
     are displayed.

EEXXIITT SSTTAATTUUSS
     The cchhoowwnn utility exits 0 on success, and >0 if an error occurs.

CCOOMMPPAATTIIBBIILLIITTYY
     Previous versions of the cchhoowwnn utility used the dot (``.'') character to
     distinguish the group name.  This has been changed to be a colon (``:'')
     character so that user and group names may contain the dot character.

     On previous versions of this system, symbolic links did not have owners.

     The --vv and --xx options are non-standard and their use in scripts is not
     recommended.

LLEEGGAACCYY DDEESSCCRRIIPPTTIIOONN
     In legacy mode, the --RR and --RRPP options do not change the user ID or the
     group ID of symbolic links.

SSEEEE AALLSSOO
     chgrp(1), chmod(1), find(1), chown(2), fts(3), compat(5), symlink(7)

SSTTAANNDDAARRDDSS
     The cchhoowwnn utility is expected to be IEEE Std 1003.2 (“POSIX.2”)
     compliant.

HHIISSTTOORRYY
     A cchhoowwnn utility appeared in Version 1 AT&T UNIX.

macOS 26.3                      August 24, 2022                     macOS 26.3

```
