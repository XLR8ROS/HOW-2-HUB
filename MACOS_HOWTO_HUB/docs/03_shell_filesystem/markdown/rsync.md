# man rsync

```text
OPENRSYNC(1)                General Commands Manual               OPENRSYNC(1)

NNAAMMEE
     ooppeennrrssyynncc – synchronise local and remote files

SSYYNNOOPPSSIISS
     ooppeennrrssyynncc [--00446688BBCCDDEEFFHHIILLOOPPRRSSTTWWVVaabbccddeeffgghhiikkllmmnnooppqqrrttuuvvxxyyzz] [--ee _p_r_o_g_r_a_m]
               [--ff _f_i_l_t_e_r] [----aaddddrreessss=_s_o_u_r_c_e_a_d_d_r] [----aappppeenndd]
               [----bbaacckkuupp--ddiirr=directory] [----bbwwlliimmiitt=limit]
               [----ccaacchhee | ----nnoo--ccaacchhee] [----cchheecckkssuumm--sseeeedd=NUM] [----cchhmmoodd=MODE]
               [----ccoommppaarree--ddeesstt=_d_i_r_e_c_t_o_r_y] [----ccoommpprreessss--lleevveell=NUM]
               [----ccoonnttiimmeeoouutt=_s_e_c_o_n_d_s] [----ccooppyy--ddeesstt=_d_i_r_e_c_t_o_r_y]
               [----ccooppyy--uunnssaaffee--lliinnkkss] [----ddeell] [----ddeellaayy--uuppddaatteess]
               [----ddeelleettee--bbeeffoorree] [----ddeelleettee--dduurriinngg] [----ddeelleettee--ddeellaayy]
               [----ddeelleettee--aafftteerr] [----ddeelleettee--eexxcclluuddeedd] [----eexxcclluuddee _p_a_t_t_e_r_n]
               [----eexxcclluuddee--ffrroomm=_f_i_l_e] [----eexxtteennddeedd--aattttrriibbuutteess]
               [----ffiilleess--ffrroomm=_f_i_l_e_s_p_e_c] [----ffoorrccee] [----iiggnnoorree--eerrrroorrss]
               [----iiggnnoorree--eexxiissttiinngg] [----iiggnnoorree--nnoonn--eexxiissttiinngg] [----iinncclluuddee _p_a_t_t_e_r_n]
               [----iinncclluuddee--ffrroomm=_f_i_l_e] [----iinnppllaaccee] [----kkeeeepp--ddiirrlliinnkkss]
               [----lliinnkk--ddeesstt=_d_i_r_e_c_t_o_r_y] [----lliisstt--oonnllyy] [----lloogg--ffiillee=_f_i_l_e]
               [----lloogg--ffiillee--ffoorrmmaatt=_f_o_r_m_a_t] [----mmaaxx--ddeelleettee=MAX] [----mmaaxx--ssiizzee=size]
               [----mmiinn--ssiizzee=size] [----mmooddiiffyy--wwiinnddooww=sec] [----nnoo--iimmpplliieedd--ddiirrss]
               [----nnoo--mmoottdd] [----nnuummeerriicc--iiddss] [----ppaarrttiiaall] [----ppaarrttiiaall--ddiirr=DIR]
               [----ppaasssswwoorrdd--ffiillee=_p_w_f_i_l_e] [----ppoorrtt=_s_e_r_v_i_c_e] [----pprrooggrreessss=_V_E_R]
               [----pprroottooccooll] [----rreeaadd--bbaattcchh=_f_i_l_e] [----rreemmoovvee--ssoouurrccee--ffiilleess]
               [----rrssyynncc--ppaatthh=_p_r_o_g_r_a_m] [----ssaaffee--lliinnkkss] [----ssiizzee--oonnllyy]
               [----ssoocckkooppttss=_s_o_c_k_o_p_t_s] [----ssppeecciiaallss] [----ssttaattss] [----ssuuffffiixx=_s_u_f_f_i_x]
               [----ssuuppeerr] [----ttiimmeeoouutt=_s_e_c_o_n_d_s]
               [----oonnllyy--wwrriittee--bbaattcchh=_f_i_l_e | ----wwrriittee--bbaattcchh=_f_i_l_e] _s_o_u_r_c_e _._._.
               _d_i_r_e_c_t_o_r_y

     ooppeennrrssyynncc ----ddaaeemmoonn [--4466hhvv] [----aaddddrreessss=_b_i_n_d_a_d_d_r] [----bbwwlliimmiitt=_b_w_l_i_m_i_t]
               [----ccoonnffiigg=_c_o_n_f_i_g_f_i_l_e] [----nnoo--ddeettaacchh] [----lloogg--ffiillee=_l_o_g_f_i_l_e]
               [----ppoorrtt=_s_e_r_v_i_c_e] [----ssoocckkooppttss=_s_o_c_k_o_p_t_s]

DDEESSCCRRIIPPTTIIOONN
     The ooppeennrrssyynncc utility synchronises files in the destination _d_i_r_e_c_t_o_r_y
     with one or more _s_o_u_r_c_e files.  Either the _s_o_u_r_c_e or the destination
     _d_i_r_e_c_t_o_r_y may be remote, but not both.  The arguments are as follows:

     --44, ----iippvv44
             Use IPv4 when connecting to a remote host, or binding to a local
             address.  If ooppeennrrssyynncc is configured to use an ----rrsshh program
             named “ssh”, then it will pass --44 to it.

     --66, ----iippvv66
             Use IPv6 when connecting to a remote host, or binding to a local
             address.  As with the --44 option, ooppeennrrssyynncc will pass --66 to the
             ----rrsshh program if it is named “ssh”.

     --88, ----88--bbiitt--oouuttppuutt
             Do not escape high-bit characters in the output (which is
             otherwise the default).

     --aa, ----aarrcchhiivvee
             Shorthand for --DDgglloopprrtt.

     ----aaddddrreessss=_s_o_u_r_c_e_a_d_d_r
             When connecting to an rsync daemon, use _s_o_u_r_c_e_a_d_d_r as the source
             address for connections, which is useful on machines with
             multiple interfaces.

     ----aappppeenndd
             If the destination file exists and is shorter than the source
             file then rsync will append the difference to the destination
             file.  If after the transfer the whole-file checksums do not
             match then the destination file will be updated via the usual
             block-based delta-merge protocol.  This option implies ----iinnppllaaccee.

     --bb, ----bbaacckkuupp
             Make a backup of changed files with ~ suffix.

     ----bbaacckkuupp--ddiirr _d_i_r_e_c_t_o_r_y
             When combined with the ----bbaacckkuupp flag, ooppeennrrssyynncc will store
             backups of files being replaced in the designated backup
             directory on the receiving side.  Can be combined with the
             ----ssuuffffiixx flag to name the backup files with a suffix.  The
             default is to not append a suffix.

             If specified as a relative path, the backup directory will be
             contained within the copied tree, and may cause conflicts or be
             subject to ----ddeelleettee rules.  It is advised to use an absolute path
             outside of the copied tree, or a relative path such as "../".

     --BB, ----bblloocckk--ssiizzee=_B_L_O_C_K_S_I_Z_E
             Specify the block size to be used for file transfers.  The upper
             bound is 512M, but it is enforced only if a differential transfer
             is required.

     ----bblloocckkiinngg--iioo
             This flag is ignored by openrsync, but is accepted for
             compatibility.

     ----bbwwlliimmiitt _l_i_m_i_t
             Limit transfer speed to _l_i_m_i_t kilobytes/sec.  The _l_i_m_i_t may also
             contain any of the suffixes described in the ----mmaaxx--ssiizzee
             definition of size.

     ----ccaacchhee
             Use the operating system buffer cache when reading and writing
             files.  This is the default on all operating systems except
             macOS, where ooppeennrrssyynncc sets F_NOCACHE by default to limit memory
             growth.  Setting this option will enabling caching by not setting
             any flags.

     ----nnoo--ccaacchhee
             Sets O_DIRECT when reading and writing files to avoid using the
             buffer cache.  Setting this option can avoid filling the cache
             with files that will not be read again, such as during a backup.
             This is the default on macOS, where F_NOCACHE is used instead of
             O_DIRECT.

     --cc, ----cchheecckkssuumm
             Use full-file checksums to determine which files have changed and
             should be transferred, rather than the usual file size and
             modification time "quick check".

     ----cchheecckkssuumm--sseeeedd=_N_U_M
             Use _N_U_M as the seed for both the 4-byte block and MD4 file
             checksums.  By default, _N_U_M is randomly generated, but if set to
             zero directs ooppeennrrssyynncc to use _t_i_m_e_(_3_) as the checksum seed.

     ----cchhmmoodd=_M_O_D_E
             Modify the permissions on files that are transferred, overriding
             the original source permissions.  Only has an effect if ----ppeerrmmss
             is specified as well.  The _M_O_D_E string can be a comma separated
             list of literal (755) or relative (g+w) permissions.

             ooppeennrrssyynncc also supports two additional extensions to relative
             permissions, adding a ‘D’ or ‘F’ infront of the relative
             permissions will apply the changes to only directories or files
             respectively.  For example: -chmod=Dg+w,Fo-w

     ----ccoommppaarree--ddeesstt=_d_i_r_e_c_t_o_r_y
             Use directory as an alternate base directory to compare files
             against on the destination machine.  If file in _d_i_r_e_c_t_o_r_y is
             found and identical to the sender's file, the file will not be
             transferred.  Multiple ----ccoommppaarree--ddeesstt directories may be
             provided.  If _d_i_r_e_c_t_o_r_y is a relative path, it is relative to the
             destination directory.

     --zz, ----ccoommpprreessss
             Compress file data during transfer to reduce the amount of data
             transferred.

     ----ccoommpprreessss--lleevveell=NUM
             Set the compression level used by ----ccoommpprreessss.

     ----ccoonnttiimmeeoouutt=_s_e_c_o_n_d_s
             Set the connection timeout in seconds.  Exit if no connection
             established within the specified time.  The default is 0, which
             means no timeout.

     ----ccooppyy--ddeesstt=_d_i_r_e_c_t_o_r_y
             Use directory as an alternate base directory to compare files
             against on the destination machine.  If file in _d_i_r_e_c_t_o_r_y is
             found and identical to the sender's file, the file will be
             locally copied.  Multiple ----ccooppyy--ddeesstt directories may be
             provided.  If _d_i_r_e_c_t_o_r_y is a relative path, it is relative to the
             destination directory.

     --LL, ----ccooppyy--lliinnkkss
             Copy targets of symbolic links, rather than the link itself.

     ----ccooppyy--uunnssaaffee--lliinnkkss
             Copy targets of symbolic links that are unsafe (absolute symlinks
             or where the target reaches outside the copied tree).

     --kk, ----ccooppyy--ddiirrlliinnkkss
             Copy targets of symbolic links that point to directories only.

     --CC, ----ccvvss--eexxcclluuddee
             Exclude a common list of files as CVS would.  The patterns
             deployed are specifically:

                   RCS            SCCS            CVS      CVS.adm
                   RCSLOG         cvslog.*        tags     TAGS
                   .make.state    .nse_depinfo    *~       #*
                   .#*            ,*              _$*      *$
                   *.old          *.bak           *.BAK    *.orig
                   *.rej          .del-*          *.a      *.olb
                   *.o            *.obj           *.so     *.exe
                   *.Z            *.elc           *.ln     core
                   .svn/
             Followed by any patterns included in _$_H_O_M_E_/_._c_v_s_i_g_n_o_r_e and the
             CVSIGNORE environment variable.

             The --CC flag also adds a “dir-merge” CVS rule to include per-dir
             _._c_v_s_i_g_n_o_r_e files.  All of these rules are appended to the end of
             the filter list with the equivalent of specifying --ff “_-_C” --ff
             “_:_C”.

     --DD      Also transfer device and special files.  Shorthand for ----ddeevviicceess
             ----ssppeecciiaallss.

     ----ddeell, ----ddeelleettee
             Delete files in _d_i_r_e_c_t_o_r_y not found in _s_o_u_r_c_e directories.  Only
             applicable with --rr.

     ----ddeellaayy--uuppddaatteess
             Delay updates of (only) plain files until all other operations
             are complete.  This is done to be more atomic.  Requires extra
             space in the destination directory up to the amount of the whole
             tree.

     ----ddeelleettee--bbeeffoorree
             Execute the above described ----ddeelleettee behavior before the transfer
             begins.  This is the default timing when

     ----ddeelleettee
             is used.  This option is mutually exclusive with ----ddeelleettee--dduurriinngg,
             ----ddeelleettee--ddeellaayy, and ----ddeelleettee--aafftteerr.

     ----ddeelleettee--dduurriinngg
             Execute the above described ----ddeelleettee behavior as the transfer
             happens, right before each directory to be transferred is checked
             for updates.  This option is mutually exclusive with
             ----ddeelleettee--bbeeffoorree, ----ddeelleettee--ddeellaayy, and ----ddeelleettee--aafftteerr.

     ----ddeelleettee--ddeellaayy
             Execute the above described ----ddeelleettee behavior after the transfer
             happens, but collect the list to be deleted right before each
             directory to be transferred is checked for updates.  This option
             is mutually exclusive with ----ddeelleettee--bbeeffoorree, ----ddeelleettee--dduurriinngg, and
             ----ddeelleettee--aafftteerr.

     ----ddeelleettee--aafftteerr
             Execute the above described ----ddeelleettee behavior after the transfer
             has completed.  This option is mutually exclusive with
             ----ddeelleettee--bbeeffoorree, ----ddeelleettee--dduurriinngg, and ----ddeelleettee--ddeellaayy.

     ----ddeelleettee--eexxcclluuddeedd
             When used in combination with any one of the above ----ddeelleettee
             options, supplied ----eexxcclluuddee patterns will not prevent a file from
             being deleted.

     --dd,, ----ddiirrss
             Copies directories, which are normally skipped unless ----rreeccuurrssiivvee
             is specified.  Directory contents are not copied, unless the path
             specified includes a trailing slash (“dir/”), or is the literal
             “.”.

     ----eexxcclluuddee _p_a_t_t_e_r_n
             Exclude files matching _p_a_t_t_e_r_n.

     ----eexxcclluuddee--ffrroomm=_f_i_l_e
             Load _p_a_t_t_e_r_n_s and _r_u_l_e_s from _f_i_l_e.

     --EE, ----eexxtteennddeedd--aattttrriibbuutteess
             Apple specific option to copy extended attributes, resource
             forks, and ACLs.  Requires at least Mac OS X 10.4 or suitably
             patched rsync.

     ----eexxeeccuuttaabbiilliittyy
             Preserve the executability of regular files (i.e., a file is
             "executable" if at least one 'x' mode bit is enabled in its
             permissions).  If the source file is executable, then for each
             'r' mode bit enabled in the destination file's permissions, the
             corresponding 'x' mode bit will be enabled.  If the source file
             is not executable then all ugo 'x' mode bits of the destination
             file will be disabled.  This option has no effect if ----ppeerrmmss is
             also specified.

     --00, ----ffrroomm00
             Use a null ('\0') character, rather than a newline to separate
             filenames read from: ----eexxcclluuddee--ffrroomm, ----iinncclluuddee--ffrroomm,
             ----ffiilleess--ffrroomm, and any merged files specified in ----ffiilltteerr rules.
             Does not affect ----ccvvss--eexxcclluuddee.

     ----ffiilleess--ffrroomm=_f_i_l_e_s_p_e_c
             Load list of files to transfer (as opposed to the command line)
             from _f_i_l_e_s_p_e_c.  _F_i_l_e_s_p_e_c can be of the form hostname:port:path.

     ----ffoorrccee
             Force deletion of non-empty directories about to be replaced by a
             non-directory.  This option has no effect if any of the ----ddeelleettee
             options are present.

     ----iiggnnoorree--eerrrroorrss
             Works in conjunction with ----ddeelleettee to delete files despite I/O
             errors.

     --yy, ----ffuuzzzzyy
             Look for files in the destination directory that might be the
             same to use as a basis to avoid copying the entire file.  The
             first file with an identical size and modification time is used
             to try to reduce the total amount of data that has to be
             transferred.

             Note that the use of the ----ddeelleettee option might get rid of any
             potential fuzzy-matches, so either use ----ddeelleettee--aafftteerr or specify
             some exclusions to prevent this.

     ----iiggnnoorree--eexxiissttiinngg
             Ignore files that already exist.

     ----iiggnnoorree--nnoonn--eexxiissttiinngg, ----eexxiissttiinngg
             Ignore files that do not already exist (do not create them).

     --II, ----iiggnnoorree--ttiimmeess
             Do not skip based on file size and modification time.

     ----iinncclluuddee _p_a_t_t_e_r_n
             Include files matching _p_a_t_t_e_r_n.

     ----iinncclluuddee--ffrroomm=_f_i_l_e
             Load _p_a_t_t_e_r_n_s and _r_u_l_e_s from _f_i_l_e.

     ----ddeevviicceess
             Also transfer device files.

     --ee _p_r_o_g_r_a_m, ----rrsshh=_p_r_o_g_r_a_m
             Specify alternative communication program, defaults to ssh(1).
             The RSYNC_RSH environment variable will be used if an --ee option
             is not present.  Note that ooppeennrrssyynncc will generally handle
             quotes, but it makes no attempt to deal with escape sequences.
             In particular, escaped quotation marks will not be escaped.

     --FF      Adds a standard _._r_s_y_n_c_-_f_i_l_t_e_r dir-merge filter rule.
             Specifically, --FF will add “: /.rsync-filter” the first time it is
             seen, and “- .rsync-filter” the second time it is seen.
             Subsequent uses have no effect.

     --ff _f_i_l_t_e_r, ----ffiilltteerr=_f_i_l_t_e_r
             Process _f_i_l_t_e_r against the global filter chain.  The specified
             _f_i_l_t_e_r may be a rule to include a filter file, or to include a
             per-directory filter file.  Regular filter files are processed
             immediately, while per-directory filter files are processed as
             directories are encountered.  See _P_A_T_T_E_R_N_S _A_N_D _R_U_L_E_S for more
             details about the syntax and capabilities of ooppeennrrssyynncc filters.

     --gg, ----ggrroouupp
             Set the group name to match the source.  For example, group
             "kristaps" with ID 1000 on a remote server is matched to group
             "kristaps" on the local machine with ID 2000.  If ----nnuummeerriicc--iiddss
             is also given or if the remote group name is unknown on the local
             machine, set the numeric group ID to match the source instead.

     --HH, ----hhaarrdd--lliinnkkss
             Attempt to preserve hard links within the list of files
             transferred.

     --hh,, ----hhuummaann--rreeaaddaabbllee
             Display numbers of bytes in human readable units.  If specified
             once, uses units of 1000, if specified twice uses units of 1024.

     ----hheellpp  Print a brief description of all options.

     --ll, ----lliinnkkss
             Also transfer symbolic links.  The link is transferred as a
             standalone file: if the destination does not exist, it will be
             broken.

     ----iinnppllaaccee
             Avoid creating temporary files, instead operating on files
             directly in place in the destination.  This option has some
             notable trade-offs that must be considered prior to using it.
             For example, hardlinks will not be broken even if a file is no
             longer hardlinked in the source directory.

     ----kkeeeepp--ddiirrlliinnkkss
             When a directory is sent, and the receiving side has a symlink to
             a directory in that place, follow that symlink and place the
             directory's contents in that symlinked dir.

     ----lliinnkk--ddeesstt=_d_i_r_e_c_t_o_r_y
             Use directory as an alternate base directory to compare files
             against on the destination machine.  If file in _d_i_r_e_c_t_o_r_y is
             found and identical to the sender's file, the file will be
             hardlinked.  Multiple ----lliinnkk--ddeesstt directories may be provided.
             If _d_i_r_e_c_t_o_r_y is a relative path, it is relative to the
             destination directory.

     ----lliisstt--oonnllyy
             Instead of transferring files, only list them.  This option is
             implied if there is only a single source argument and no
             destination argument.

     ----lloogg--ffiillee=_f_i_l_e
             Specify a _f_i_l_e to log to instead of _s_t_d_o_u_t.  This implies a
             ----lloogg--ffiillee--ffoorrmmaatt of “%i %n%L” if none was previously specified.

     ----lloogg--ffiillee--ffoorrmmaatt=_f_o_r_m_a_t
             Specify a log format for each file involved in the transfer.  The
             _f_o_r_m_a_t argument may contain any number of tokens, like “%i”, with
             special meaning.  The following tokens are defined for daemon
             mode, but are also accepted for normal ooppeennrrssyynncc usage:

             %a  The client's remote IP address.

             %h  The client's hostname.

             %m  The module requested by the client.

             %P  The path to the module requested by the client.

             %u  The username that the client has authenticated as.

             These tokens are globally defined:

             %b  The number of bytes transferred.

             %B  The file mode, in a human-readable format.

             %c  The size of block checksums received for the source file.
                 This is not currently implemented by this implementation, but
                 will be accepted.

             %f  The long-form filename without a trailing “/” indicator.

             %G  The group of the file in decimal format, or “DEFAULT” when
                 the group is 0.

             %I  The itemized list of updates including unchanged files, as if
                 ----iitteemmiizzee--cchhaannggeess was specified twice.

             %i  The itemized list of updates, as if ----iitteemmiizzee--cchhaannggeess was
                 specified.

             %l  The length of the file.

             %L  An indicator of the file being a symlink or a hardlink.  For
                 hardlinks, this token is replaced with “=> FILENAME”.  For
                 symlinks, this token is replaced with “=> FILENAME”.  For
                 non-links, this token is replaced with the empty string.

             %M  The mtime of the file, in full date-time format.

             %n  The short-form filename with a trailing “/” indicator.

             %o  The operation conducted on the file.  This can be one of
                 “send”, “recv”, or “del.”.

             %p  The PID of the rsync client.

             %t  The current time, in date-time format.

             %U  The user of the file in decimal format, or “DEFAULT” when the
                 user is 0.

     ----mmaaxx--ddeelleettee _M_A_X
             Once MAX files have been deleted, do not delete any more files.

     ----mmaaxx--ssiizzee _s_i_z_e
             Don't transfer any file that is larger than _s_i_z_e bytes.
             Alternatively _s_i_z_e may instead use a multiplier (such as 0B,
             100B, 1023B, 1K, 1.5K, 5.5M; or any sequence with a case-
             insensitive terminal scale multiplier of B, K, M, G, T, P, or E;
             corresponding to bytes, kilobytes, and so on) to specify the
             size.

     ----mmiinn--ssiizzee _s_i_z_e
             Don't transfer any file that is smaller than _s_i_z_e bytes.  See
             ----mmaaxx--ssiizzee on the definition of size.

     ----mmooddiiffyy--wwiinnddooww _s_e_c
             When comparing file modification times for the purpose of
             speeding up transfers consider offsets of up to _s_e_c seconds the
             same.

     --nn, ----ddrryy--rruunn
             Do not actually modify the destination.  Mainly useful in
             combination with --vv.

     ----nnoo--mmoottdd
             Do not display the Message of the Day.

     ----nnuummeerriicc--iiddss
             Ignore user and group names, use numeric user and group IDs only.
             Has no effect unless --gg or --oo is also given.

     --OO, ----oommiitt--ddiirr--ttiimmeess
             Do not perserve the modification times of directories.  This can
             be expensive when the directories reside on NFS.  This option is
             inferred if you use ----bbaacckkuupp without ----bbaacckkuupp--ddiirr.

     --oo, ----oowwnneerr
             Set the user name to match the source, with similar matching
             logic as for --gg.  If ----nnuummeerriicc--iiddss is also given or if the remote
             user name is unknown on the local machine, set the numeric user
             ID to match the source instead.  Only works if run as root.

     --PP      Shorthand for ----ppaarrttiiaall ----pprrooggrreessss.

     --pp, ----ppeerrmmss
             Set destination file or directory permissions to match the source
             when it is updated.

     ----ppaarrttiiaall
             Do not remove partially transferred files if ooppeennrrssyynncc is
             interrupted, which opens up the possibility for them to be easily
             resumed later.

     ----ppaarrttiiaall--ddiirr=_D_I_R
             Store all partially transferred files in _D_I_R to allow an
             interrupted transfer to resume without re-transferring files.
             Implies --ppaarrttiiaall.

     ----ppaasssswwoorrdd--ffiillee=_p_w_f_i_l_e
             Define a file to read the password from when connecting to an
             rsync daemon.  The password should be written on the first line
             of the file, and may have a terminating newline.  The _p_w_f_i_l_e is
             expected to not be readable by 'other', and to be owned by root
             if ooppeennrrssyynncc is running as root.

     ----ppoorrtt=_s_e_r_v_i_c_e
             Specify an alternative TCP port number.  The _s_e_r_v_i_c_e can be given
             as a decimal integer or as a name to be looked up in the
             services(5) database.  The default is “rsync”.

     --mm, ----pprruunnee--eemmppttyy--ddiirrss
             Prune empty directories from the file list on the receiver side.
             Empty directories may be excluded from pruning with an exclude or
             protect filter rule.  A directory wich only contains other empty,
             non-excluded directories, is also considered empty.

     --qq, ----qquuiieett
             Suppress all non-error related informational messages.

     ----pprrooggrreessss
             Periodically report file transfer progress.

     ----pprroottooccooll=VER
             Force ooppeennrrssyynncc to operate using the specified protocol version.
             Normally the protocol version is negotiated automatically, but an
             older protocol version can be forced with this flag.

     --rr, ----rreeccuurrssiivvee
             If _s_o_u_r_c_e designates a directory, synchronise the directory and
             the entire subtree connected at that point.  If _s_o_u_r_c_e ends with
             a slash, only the subtree is synchronised, not the _s_o_u_r_c_e
             directory itself.  If _s_o_u_r_c_e is a file, this has no effect.

     ----rreeaadd--bbaattcchh=_f_i_l_e
             Read a batch file previously prepared by ooppeennrrssyynncc from _f_i_l_e.
             See the ----wwrriittee--bbaattcchh option for a description of a batch file.
             When reading a batch file, the _s_o_u_r_c_e arguments are optional and
             ignored if specified.

     ----rreemmoovvee--ssoouurrccee--ffiilleess
             Remove _s_o_u_r_c_e files as they are transferred into _d_i_r_e_c_t_o_r_y.
             Files are only removed once they are confirmed to be fully in
             place.  By default ooppeennrrssyynncc will delete files as the transfer
             progresses, but given its asynchronous nature there may be a
             noticeable delay between a given file finishing its transfer and
             its subsequent removal.

             When combined with ----ddeellaayy--uuppddaatteess, files will be removed in a
             larger batch toward the end of the transfer.

     --RR, ----rreellaattiivvee
             Normally, pathnames on the commandline omit the directory
             components.  This option will include the dir components.

     ----nnoo--iimmpplliieedd--ddiirrss
             Changes the default behavior of ----rreellaattiivvee such that implied
             directories do not have their attributes modified, or are created
             with default attributes, rather than the source attributes, if
             they do not exist.  This allows the implied directories to
             differ, including being a symlink on one side and a real
             directory on the other.

     ----rrssyynncc--ppaatthh=_p_r_o_g_r_a_m
             Run _p_r_o_g_r_a_m on the remote host instead of the default _r_s_y_n_c.

     ----ssiizzee--oonnllyy
             Skip files whose sizes match (regardless of timestamp).

     ----ssaaffee--lliinnkkss
             Skip any symlinks that are unsafe (absolute symlinks or where the
             target is outside the copied tree).

     ----ssoocckkooppttss=_s_o_c_k_o_p_t_s
             Set custom _s_o_c_k_o_p_t_s on the socket created to communicate with an
             rsync daemon.  _s_o_c_k_o_p_t_s should be of the form
             “name[=value][,...]”, where _n_a_m_e matches an SO_* option described
             in setsockopt(2).  Note that only the following options are
             currently supported:

                   SO_KEEPALIVE
                   SO_REUSEADDR
                   SO_SNDBUF
                   SO_RCVBUF
                   SO_SNDLOWAT
                   SO_RCVLOWAT
                   SO_SNDTIMEO
                   SO_RCVTIMEO
                   SO_REUSEPORT May not be available on all systems.

     --SS, ----ssppaarrssee
             Attempt to efficiently handle sparse files.  Note that attempting
             to combine --SS and ----iinnppllaaccee will result in an error.

     ----ssppeecciiaallss
             Also transfer fifo and unix domain socket files.

     ----ssttaattss
             Print verbose statistics about the transfer at the end of the
             run.  Provides details about how much data transfer was saved by
             ooppeennrrssyynncc.

     ----ssuuffffiixx _s_u_f_f_i_x
             Sets the suffix to be appended to filenames when creating backups
             on the receiver before replacing files.  Defaults to ~ except
             when combined with ----bbaacckkuupp--ddiirr where the default is an empty
             string.

     ----ssuuppeerr
             Always attempt traditionally super-user activities.  This flag
             mostly interacts with the ----oowwnneerr, ----ggrroouupp, and ----ddeevviicceess
             options, which may be permitted to unprivileged users on the
             receiving end in some configurations.  ----nnoo--ssuuppeerr is also
             supported to avoid them entirely.

     --TT, ----tteemmpp--ddiirr=_d_i_r_e_c_t_o_r_y
             Instead of creating temporarily files in the destination
             directory, create them in the specified temporary directory.  If
             this directory is on a different filesystem, that will require
             moving the file rather than renaming it into place, and is
             therefore not atomic.

     ----ttiimmeeoouutt=_s_e_c_o_n_d_s
             Set the I/O timeout in seconds.  Exit if no data was transferred
             for the specified time.  The default is 0, which means no
             timeout.

     --tt, ----ttiimmeess
             Set destination file and directory modification time to match the
             source when it is updated or created.

     --uu, ----uuppddaattee
             Skip existing files on the destination that have a modification
             time newer than the source file.

     --vv, ----vveerrbboossee
             Increase verbosity.  Specify once for files being transferred,
             twice for specific status, thrice for per-file transfer
             information, and four times for per-file breakdowns.

     --xx, ----oonnee--ffiillee--ssyysstteemm
             Do not cross filesystem boundaries.  If this option is repeated,
             all mount point directories from the copy are omitted.
             Otherwise, it includes an empty directory at each mount point it
             encounters.

     --VV, ----vveerrssiioonn
             Print version and exit.

     --WW, ----wwhhoollee--ffiillee
             Copy the entire file rather than using the rsync incremental
             algorithm.  This option may be faster, especially if the network
             link is faster than the disk.

     ----oonnllyy--wwrriittee--bbaattcchh=_f_i_l_e
             Prepare a batch file and write it to _f_i_l_e.  With this option, the
             batch file is written without updating the destination.  See the
             below ----wwrriittee--bbaattcchh option for a description of a batch file.

     ----wwrriittee--bbaattcchh=_f_i_l_e
             Prepare a batch file and write it to _f_i_l_e.  A batch file is
             composed of a small heading describing the transfer parameters
             negotiated, followed by a raw dump of the data transmitted by the
             sender.  When used with ----rreeaadd--bbaattcchh on the other side, the
             transfer is simply replayed from the batch file against the
             application's reeceiver, and the destination tree is updated
             accordingly.

             Batch files are intended to reproduce an update to a destination
             tree to many other identical trees without needing to establish a
             direct connection between them.  This mechanism also avoids
             having to perform many of the intermediate steps required for a
             transfer, such as receiver-side checksums and blocking.

     A remote _s_o_u_r_c_e or _d_i_r_e_c_t_o_r_y has the syntax _h_o_s_t:_p_a_t_h for connecting via
     ssh(1), or rrssyynncc://_h_o_s_t/_p_a_t_h or _h_o_s_t::_p_a_t_h for connecting to a remote
     daemon.  Subsequent to the first remote _s_o_u_r_c_e, the host may be dropped
     to become just :_p_a_t_h or ::_p_a_t_h.

     For connecting to a remote daemon with rrssyynncc://_h_o_s_t or _h_o_s_t::_p_a_t_h, the
     first path component is interpreted as a "module": _h_o_s_t::_m_o_d_u_l_e/_p_a_t_h.
     This only applies to the first _s_o_u_r_c_e invocation; subsequent to that, the
     module should not be specified.

     By default, new destination files and directories are given the current
     time and the source file permissions.  Updated files retain their
     existing permissions.  It is an error if updated files have their file
     types change (e.g., updating a directory with a file).

     At this time, _s_o_u_r_c_e may only consist of regular files, directories (only
     with --rr), or symbolic links (only with --ll).  The destination _d_i_r_e_c_t_o_r_y
     must be a directory and is created if not found.

     ooppeennrrssyynncc also supports a ----ddaaeemmoonn mode, which may be run either
     standalone or may be invoked by, e.g., inetd(8) or similar services that
     hand a socket off to an external program for handling.

     Daemon options that are shared with the non-daemon mode of ooppeennrrssyynncc
     behave as described above.  Options specific to daemon mode are as
     follows:

     ----ccoonnffiigg=_c_o_n_f_i_g_f_i_l_e
             Load daemon configuration from the named _c_o_n_f_i_g_f_i_l_e instead of
             the default location.  By default, ooppeennrrssyynncc will look for its
             configuration at _/_e_t_c_/_r_s_y_n_c_d_._c_o_n_f.  See rsyncd.conf(5) for
             details of the format of this file.

     ----nnoo--ddeettaacchh
             Run the ooppeennrrssyynncc daemon in the foreground, instead of the
             background.

     Note that the ooppeennrrssyynncc daemon mode will log to syslog(3) by default
     unless ----lloogg--ffiillee is specified, regardless of whether ----nnoo--ddeettaacchh has
     been specified to run in the foreground or not.

PPAATTTTEERRNNSS AANNDD RRUULLEESS
     The --ff, ----iinncclluuddee, ----iinncclluuddee--ffrroomm, ----eexxcclluuddee, and ----eexxcclluuddee--ffrroomm options
     may be used to load a filter rule or a set of filter rules.  A single
     filter rule consists of a _t_y_p_e, an optional set of _m_o_d_i_f_i_e_r_s, and a
     _p_a_t_t_e_r_n.  Each _t_y_p_e has a short name and a long name.  These will be
     described in more depth shortly.

     A filter file is a set of rules, one per line.  Comments are accepted,
     starting with a ‘#’.  Empty lines are ignored.

     Each rule is of the following form:

     <TYPE>[,<MODIFIERS>] <PATTERN>

     If the short name is used, then the comma separating the modifiers from
     the rule type is optional.  The delimiter between the type/modifiers and
     the pattern may also be an underbar instead of a space.

     The following rule types are supported:

           LONG NAME    SHORT NAME    DESCRIPTION
           exclude      -             Exclude a file from the transfer
           include      +             Include a file from the transfer
           merge        .             Merge rules in from a file
           dir-merge    :             Merge rules in from a per-directory file
           hide         H             Hide a file from the transfer
           show         S             “not hide a file from the transfer”
           protect      P             Protect a file from deletion
           risk         R             “not protect a file from deletion”
           clear        !             Clear the current filter list

     The following rule modifiers are supported for the “exclude” and
     “include” rule types:

           MODIFIER    DESCRIPTION
           /           Match against the absolute pathname of the entry
           !           Take effect if the pattern does not match the entry
           C           Insert the global CVS exclusions
           s           Marks a rule as sender-side only
           r           Marks a rule as receiver-side only
           p           Marks a rule as perishable (do not prevent removal of a
                       directory)

     The above modifiers will be ignored if applied to other rule types, with
     the exception of “merge” and “dir-merge” rules.  See the _M_e_r_g_e _R_u_l_e_s
     section for more details of the semantics.

   IInncclluuddee aanndd EExxcclluuddee RRuulleess
     The six basic types of include and exclude rules briefly described above
     are “exclude”, “include”, “hide”, “show”, “protect”, “risk”.

     The “hide” and “show” types are sender-side versions of the “exclude” and
     “include” rules, while the “protect” and “risk” types are their receiver-
     side equivalents.

     Each of these rules take a pattern that is typically matched against the
     basename of a transfer candidate's name.  A trailing ‘/’ in the pattern
     indicates that the entry should only match a directory name, while a
     leading ‘/’ indicates that the pattern is anchored to the beginning of
     the transfer path.  The beginning of the transfer path is either the root
     of the transfer, or the directory containing a dir-merge file if the rule
     in question comes from a dir-merge file.  A ‘/’ at any other position, or
     a “**” in the pattern, will match against the full path to the transfer
     entry beginning at the root of the transfer.

     Patterns may contain any of the following wildcards.

           WILDCARD    DESCRIPTION
           ?           Matches any character, except ‘/’
           *           Matches zero or more characters, except ‘/’
           **          Matches zero or more characters
           [           Character class, as in POSIX regular expressions
           /***        Matches a directory and all of its contents

     Backslashes may be used to escape one of the above wildcard characters,
     but is ordinary when appearing before any other character.

     Note that exclude rules with the “C” modifier applied do not take a
     pattern.

   MMeerrggee RRuulleess
     The merge rules, “merge” and “dir-merge”, are another way to insert a
     filter rule file.  “merge” rules are evaluated once as soon as they are
     processed, and the rules read in are inserted at the same position as the
     merge file.  “dir-merge” rules are evaluated as ooppeennrrssyynncc progresses
     through the file list, searching each directory encountered for the file
     named in the rule's pattern.

     If a “dir-merge” rule appears before a “clear” rule, it will not be
     processed at all.

     “dir-merge” rules are inserted into their own chain of rules, rather than
     directly into the global ruleset.  “clear” rules appearing in a dir-
     merged file do not affect the global ruleset.  As we find dir-merged
     files in the transfer, their rules are prepended to their dir-merge chain
     so that a deeper directory's rules take precedence over its parent's
     rules.

     When one of the above exclude/include modifiers are applied to “merge” or
     “dir-merge” rule, those modifiers are applied to the exclude/include
     rules within the file.  The following modifiers may additionally be
     specified for merge rules:

           MODIFIER    DESCRIPTION
           -           All rules within are exclude rules
           +           All rules within are include rules
           C           File processing should assume CVS-compatible parsing
           e           Exclude the file's name from the transfer
           n           Rules are not inherited by subdirectories
           w           Rules are word-split instead of line-split

     The CVS-compatible modifier implies the ‘-’, ‘n’ and ‘w’ modifiers.  If a
     filename is not supplied with it, then “.cvsignore” is used.

EENNVVIIRROONNMMEENNTT
     The following environment variables affect execution of ooppeennrrssyynncc:

     LOGNAME         This variable may also hold the username to use when
                     connecting to an rsync daemon.  If LOGNAME is not set,
                     then “nobody” will be used.

     USER            This variable holds the username to use when connecting
                     to an rsync daemon.  If USER is not set, then LOGNAME
                     will be used.

     RSYNC_RSH       This variable specifies the remote shell to use for
                     remote connections.  The default remote shell is ssh(1)
                     if neither RSYNC_RSH nor ----rrsshh are specified.

     RSYNC_PASSWORD  This variable specifies the password to use when
                     connecting to an rsync daemon.  It will be ignored if the
                     ----ppaasssswwoorrdd--ffiillee option is specified and passes the mode
                     and owner check described above in the option's
                     description.  On many systems, environment variables are
                     readable by other processes and should be considered
                     insecure.  Please prefer a password file instead.

EEXXIITT SSTTAATTUUSS
     The ooppeennrrssyynncc utility exits 0 on success, 1 if an error occurs, or 2 if
     the remote protocol version is older than the local protocol version.

EEXXAAMMPPLLEESS
     A common invocation of ooppeennrrssyynncc is for archiving from a remote host to
     the local computer:

           % openrsync -av --delete remote:rpath /local/path

     This will update the contents of _/_l_o_c_a_l_/_p_a_t_h_/_r_p_a_t_h with those on the
     remote server.  Switching remote and local wil update the remote contents
     instead:

           % openrsync -av --delete /local/path remote:rpath

     All examples use --tt so that destination files inherit the source time.
     If not changed, subsequent invocations of ooppeennrrssyynncc will then consider
     the file up to date and not transfer block hashes.

     To update the out-of-date remote files _h_o_s_t_:_d_e_s_t_/_b_a_r and _h_o_s_t_:_d_e_s_t_/_b_a_z
     with the local _._._/_s_r_c_/_b_a_r and _._._/_s_r_c_/_b_a_z:

           % openrsync -t ../src/bar ../src/baz host:dest

     To update the out-of-date local files _b_a_r and _b_a_z with the remote files
     _h_o_s_t_:_s_r_c_/_b_a_r and _h_o_s_t_:_s_r_c_/_b_a_z:

           % openrsync -t host:src/bar :src/baz .

     To update the out-of-date local files _._._/_d_e_s_t_/_b_a_r and _._._/_d_e_s_t_/_b_a_z with
     _b_a_r and _b_a_z:

           % openrsync -t bar baz ../dest

     To update the out-of-date remote files in _h_o_s_t_:_d_e_s_t on a remote host
     running ooppeennrrssyynncc with the local host running rsync(1):

           % rsync --rsync-path openrsync -t ../dest/* host:dest

SSEEEE AALLSSOO
     ssh(1), rsync(5), rsyncd(5)

SSTTAANNDDAARRDDSS
     ooppeennrrssyynncc is compatible with rsync protocol versions 27 - 29 as supported
     by the samba.org implementation of rsync.

HHIISSTTOORRYY
     The ooppeennrrssyynncc utility has been available since OpenBSD 6.5.

AAUUTTHHOORRSS
     The ooppeennrrssyynncc utility was written by Kristaps Dzonsons <_k_r_i_s_t_a_p_s_@_b_s_d_._l_v>.

macOS 26.3                       May 25, 2026                       macOS 26.3

```
