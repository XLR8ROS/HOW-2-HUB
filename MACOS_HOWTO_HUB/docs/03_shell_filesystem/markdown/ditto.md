# man ditto

```text
DITTO(1)                    General Commands Manual                   DITTO(1)




NNAAMMEE
     ddiittttoo – copy directory hierarchies, create and extract archives

SSYYNNOOPPSSIISS
     ddiittttoo [--vv] [--VV] [--XX] [<options>] _s_r_c _._._. _d_s_t___d_i_r_e_c_t_o_r_y
     ddiittttoo [--vv] [--VV] [<options>] _s_r_c___f_i_l_e _d_s_t___f_i_l_e
     ddiittttoo --cc [--zz | --jj | --kk] [--vv] [--VV] [--XX] [<options>] _s_r_c _d_s_t___a_r_c_h_i_v_e
     ddiittttoo --xx [--zz | --jj | --kk] [--vv] [--VV] [<options>]
           _s_r_c___a_r_c_h_i_v_e _._._. _d_s_t___d_i_r_e_c_t_o_r_y
     ddiittttoo --hh | ----hheellpp

DDEESSCCRRIIPPTTIIOONN
     In its first form, ddiittttoo copies one or more source files or directories
     to a destination directory.  If the destination directory does not exist
     it will be created before the first source is copied.  If the destination
     directory already exists then the source directories are merged with the
     previous contents of the destination.

     In its second form, ddiittttoo copies a file to the supplied _d_s_t___f_i_l_e
     pathname.

     The next two forms reflect ddiittttoo's ability to create and extract
     archives.  These archives can be either CPIO format (preferred for unix
     content) or PKZip (for Windows compatibility).  _s_r_c___a_r_c_h_i_v_e (and
     _d_s_t___a_r_c_h_i_v_e) can be the single character '-', causing ditto to read
     (write) archive data from stdin (or to stdout, respectively).

     ddiittttoo follows symbolic links provided as arguments but does not follow
     any links as it traverses the source or destination hierarchies.  ddiittttoo
     overwrites existing files, symbolic links, and devices in the destination
     when these are copied from a source.  The resulting files, links, and
     devices will have the same mode, access time, modification time, owner,
     and group as the source items from which they are copied.  Pipes,
     sockets, and files with names beginning with .nfs or .afpDeleted will be
     ignored.  ddiittttoo does not modify the mode, owner, group, extended
     attributes, or ACLs of existing directories in the destination.  Files
     and symbolic links cannot overwrite directories or vice-versa.

     ddiittttoo can be used to "thin" Universal Mach-O binaries during a copy.
     ddiittttoo can also copy files selectively based on the contents of a BOM
     ("Bill of Materials") file.  ddiittttoo preserves file hard links (but not
     directory hard links) present in the source directories and preserves
     setuid and setgid modes when run as the superuser.

     ddiittttoo will preserve resource forks and HFS meta-data information when
     copying unless instructed otherwise using ----nnoorrssrrcc .  ----nnoorrssrrcc will
     disable copy of resource forks, extended attributes, Access Control Lists
     (ACLs), as well as quarantine bits.  DITTONORSRC can be set in the
     environment as an alias to ----nnoorrssrrcc ----nnooeexxttaattttrr ----nnooaaccll ----nnooqqttnn on the
     command line. However, each option can be individually turned on or off,
     see the OPTIONS section for more details.

OOPPTTIIOONNSS
     --hh, ----hheellpp    Print full usage.

     --vv            Print a line of output to stderr for each source directory
                   copied.

     --VV            Print a line of output to stderr for every file, symbolic
                   link, and device copied.

     --XX            When copying one or more source directories, do not descend
                   into directories that have a different device ID.

     --cc            Create an archive at the destination path.  The default
                   format is CPIO, unless --kk is given.  CPIO archives should
                   be stored in files with names ending in .cpio.  Compressed
                   CPIO archives should be stored in files with names ending
                   in .cpgz.

     --zz            Create compressed CPIO archives, using gzip(1) compression.

     --jj            Create compressed CPIO archives, using bzip2(1)
                   compression.

     --xx            Extract the archives given as source arguments. The format
                   is assumed to be CPIO, unless --kk is given.  Compressed CPIO
                   is automatically handled.

     --kk            Create or extract from a PKZip archive instead of the
                   default CPIO.  PKZip archives should be stored in filenames
                   ending in .zip.

     ----kkeeeeppPPaarreenntt  When creating an archive, embed the parent directory name
                   _s_r_c in _d_s_t___a_r_c_h_i_v_e.

     ----aarrcchh _a_r_c_h   Thin Universal binaries to the specified architecture.  If
                   multiple ----aarrcchh options are specified then the resulting
                   destination file will contain each of the specified
                   architectures (if they are present in the source file).
                   _a_r_c_h should be specified as "arm64", "x86_64", etc.

     ----bboomm _b_o_m     Copy only files, links, devices, and directories that are
                   present in the specified BOM.

     ----rrssrrcc        Preserve resource forks and HFS meta-data.  ddiittttoo will
                   store this data in Carbon-compatible ._ AppleDouble files
                   on filesystems that do not natively support resource forks.
                   As of Mac OS X 10.4, ----rrssrrcc is default behavior.

     ----nnoorrssrrcc      Do not preserve resource forks and HFS meta-data.  If both
                   ----nnoorrssrrcc and ----rrssrrcc are passed, whichever is passed last
                   will take precedence.  Both options override DITTONORSRC.
                   Unless explicitly specified, ----nnoorrssrrcc also implies
                   ----nnooeexxttaattttrr and ----nnooaaccll to match the behavior of Mac OS X
                   10.4.

     ----eexxttaattttrr     Preserve extended attributes (requires ----rrssrrcc). As of Mac
                   OS X 10.5, ----eexxttaattttrr is the default.

     ----nnooeexxttaattttrr   Do not preserve extended attributes (requires ----nnoorrssrrcc).

     ----qqttnn         Preserve quarantine information.  As of Mac OS X 10.5,
                   ----qqttnn is the default.

     ----nnooqqttnn       Do not preserve quarantine information.

     ----aaccll         Preserve Access Control Lists (ACLs).  As of Mac OS X 10.5,
                   ----aaccll is the default.

     ----nnooaaccll       Do not preserve ACLs.

     ----nnooccaacchhee     Do not perform copies using the Mac OS X Unified Buffer
                   Cache. Files read and written will not be cached, although
                   if the file is already present in the cache, the cached
                   information will be used.

     ----hhffssCCoommpprreessssiioonn
                   When copying files or extracting content from an archive,
                   if the destination is an HFS+ or APFS volume that supports
                   filesystem compression, all the content will be compressed
                   if appropriate. This is only supported on Mac OS X 10.6 or
                   later, and is only intended to be used in installation and
                   backup scenarios that involve system files. Since files
                   using filesystem compression are not readable on versions
                   of Mac OS X earlier than 10.6, this flag should not be used
                   when dealing with non-system files or other user-generated
                   content that will be used on a version of Mac OS X earlier
                   than 10.6.

     ----nnoohhffssCCoommpprreessssiioonn
                   Do not compress files with filesystem compression when
                   copying or extracting content from an archive unless the
                   content is already compressed with filesystem compression.
                   This flag is only supported on Mac OS X 10.6 or later.
                   ----nnoohhffssCCoommpprreessssiioonn is the default.

     ----pprreesseerrvveeHHFFSSCCoommpprreessssiioonn
                   When copying files to an HFS+ or APFS volume that supports
                   filesystem compression, ditto will preserve the compression
                   of any source files that were using filesystem compression.
                   This flag is only supported on Mac OS X 10.6 or later.
                   ----pprreesseerrvveeHHFFSSCCoommpprreessssiioonn is the default.

     ----nnoopprreesseerrvveeHHFFSSCCoommpprreessssiioonn
                   Do not preserve filesystem compression when copying files
                   that are already compressed with filesystem compression.
                   This is only supported on Mac OS X 10.6 or later.

     ----sseeqquueesstteerrRRssrrcc
                   When creating a PKZip archive, preserve resource forks and
                   HFS meta-data in the subdirectory __MACOSX.  PKZip
                   extraction will automatically find these resources.

     ----zzlliibbCCoommpprreessssiioonnLLeevveell _n_u_m
                   Sets the compression level to use when creating a PKZip
                   archive. The compression level can be set from 0 to 9,
                   where 0 represents no compression, and 9 represents optimal
                   (slowest) compression. By default, ditto will use the
                   default compression level as defined by zlib.

     ----ppaasssswwoorrdd    When extracting a password-encrypted ZIP archive, you must
                   specify --password to allow ditto to prompt for a password
                   to use to extract the contents of the file. If this option
                   is not provided, and a password-encrypted file is
                   encountered, ditto will emit an error message.

     ----ppeerrssiissttRRoooottlleessss
                   If a file being replaced has the SF_RESTRICTED flag or the
                   com.apple.rootless extended attribute set, retain it even
                   if the source file may not have had the same flag or
                   attribute.

     ----nnooppeerrssiissttRRoooottlleessss
                   Do not persist the SF_RESTRICTED flag or the
                   com.apple.rootless extended attribute for files being
                   replaced.

     ----nnoonnAAttoommiiccCCooppiieess
                   Do not perform atomic copies when replacing existing files.
                   By default ddiittttoo will atomically swap new files into place
                   when completing a copy.

     ----sseeggmmeennttLLaarrggeeFFiilleess
                   When copying files to a CPIO archive, segment files larger
                   than 8 gigabytes into multiple entries.

     ----kkeeeeppBBiinnaarriieess
                   When copying files ddiittttoo will set aside the original Mach-O
                   binary when it is being replaced.  The file name will be
                   changed to a random number preceeded by the prefix .BC.T_

     ----kkeeeeppBBiinnaarriieessLLiisstt _p_a_t_h
                   When ddiittttoo keeps binary files it will record the location
                   of the kept file in the file at the specified path.

     ----kkeeeeppBBiinnaarriieessPPaatttteerrnn _r_e_g_e_x
                   Keep any regular file that matches the specified regular
                   expression. Note that this file must not be a Mach-O
                   binary.

     ----llaanngg _l_a_n_g   When copying files with an index bom specified via --bb
                   option the user can specify language variants to filter
                   from the index bom.  By default ddiittttoo will create a new
                   index bom at /tmp/ditto.XXXXX representing the filtered
                   contents.  The user can direct the output bom via the --oo
                   flag.

     ----oouuttBBoomm _b_o_m  Specify an explicit path for the output bom.  This bom will
                   only be created if the user specified the --oo flag or the --ll
                   flags.

     ----cclloonnee       Attempt to clone regular files when copying.

     ----nnoocclloonnee     Do not attempt to clone files.

     ----ooppttiioonn _k_e_y_=_v_a_l_u_e
                   Specify an arbitrary key value pair to be passed to the
                   copier.  The value can be a string, boolean, or integer.
                   Booleans can be specified as 'true', 'false', 'yes', or
                   'no'.

EEXXAAMMPPLLEESS
     The command:
           ditto src_directory dst_directory
     copies the contents of src_directory into dst_directory, creating
     dst_directory if it does not already exist.

     The command:
           ditto src_directory dir/dst_directory
     copies the contents of src_directory into dir/dst_directory, creating dir
     and dst_directory if they don't already exist.

     The command:
           ditto src-1 ... src-n dst_directory
     copies the contents of all of the src directories into dst_directory,
     creating dst_directory if it does not already exist.

     The command:
           ditto --arch ppc universal_file thin_file
     copies the contents of universal_file into thin_file, thinning executable
     code to ppc-only on the fly.

     The command:
           ditto -c --norsrc Scripts -|ssh rhost ditto -x --norsrc - ./Scripts
     copies Scripts, skipping any resources or meta-data, to rhost.

     The command:
           pax -f archive.cpio
     will list the files in the CPIO archive archive.cpio.

     The command:
           pax -zf archive.cpgz
     will list the files in the compressed CPIO archive archive.cpgz.

     The command:
           ditto -c -k --sequesterRsrc --keepParent src_directory archive.zip
     will create a PKZip archive similarly to the Finder's Compress
     functionality.

     The command:
           unzip -l archive.zip
     will list the files in the PKZip archive archive.zip.

EERRRROORRSS
     ddiittttoo returns 0 if everything is copied, otherwise non-zero.  ddiittttoo
     almost never gives up, preferring to report errors along the way.
     Diagnostic messages will be printed to standard error.

EENNVVIIRROONNMMEENNTT
     DITTOABORT                If the environment variable DITTOABORT is set,
                               ddiittttoo will call abort(3) if it encounters a
                               fatal error.

     DITTONORSRC               If DITTONORSRC is set but ----rrssrrcc, ----eexxttaattttrr,
                               and ----aaccll are not specified, ddiittttoo will not
                               preserve those additional types of metadata.

     DITTOKEEPBINARIESPATTERN  If the environment variable
                               DITTOKEEPBINARIESPATTERN is set, ddiittttoo will
                               keep files that match the regular expression.
                               This matches the behavior of
                               ----kkeeeeppBBiinnaarriieessPPaatttteerrnn

     DITTOKEEPBINARIESDIR      By default, ddiittttoo will keep the original file
                               adjacent to its replacement.  If the
                               environment variable DITTOKEEPBINARIESDIR is
                               set, ddiittttoo will move kept files into the
                               specified directory path.  The files will be
                               renamed to a random UUID and the directory will
                               be kept balanced.

     DITTO_TEST_OPTIONS        If DITTO_TEST_OPTIONS is set to 1 ddiittttoo will
                               print the parameters to be passed to
                               BOMCopierCopyWithOptions for each source and
                               destination pair, including the contents of the
                               options dictionary. It will then exit without
                               performing any copy operation.

BBUUGGSS
     ddiittttoo doesn't copy directories into directories in the same way as cp(1).
     In particular,
           ditto foo bar
     will copy the contents of foo into bar, whereas
           cp -r foo bar
     copies foo itself into bar. Though this is not a bug, some may consider
     this bug-like behavior.  ----kkeeeeppPPaarreenntt for non-archive copies will
     eventually alleviate this problem.

SSEEEE AALLSSOO
     bom(5), lsbom(8), mkbom(8), cpio(1), zip(1), gzip(1), bzip2(1), tar(1).

HHIISSTTOORRYY
     ddiittttoo first appeared in Mac OS X (10.0)

macOS 14.0                      March 29, 2023                      macOS 14.0

```
