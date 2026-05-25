# man osascript

```text
OSASCRIPT(1)                General Commands Manual               OSASCRIPT(1)

NNAAMMEE
     oossaassccrriipptt – execute OSA scripts (AppleScript, JavaScript, etc.)

SSYYNNOOPPSSIISS
     oossaassccrriipptt [--ll _l_a_n_g_u_a_g_e] [--ii] [--ss _f_l_a_g_s] [--ee _s_t_a_t_e_m_e_n_t | _p_r_o_g_r_a_m_f_i_l_e]
               [_a_r_g_u_m_e_n_t _._._.]

DDEESSCCRRIIPPTTIIOONN
     oossaassccrriipptt executes the given OSA script, which may be plain text or a
     compiled script (.scpt) created by Script Editor or osacompile(1).  By
     default, oossaassccrriipptt treats plain text as AppleScript, but you can change
     this using the --ll option.  To get a list of the OSA languages installed
     on your system, use osalang(1).

     oossaassccrriipptt will look for the script in one of the following three places:

     1.   Specified line by line using --ee switches on the command line.

     2.   Contained in the file specified by the first filename on the command
          line.  This file may be plain text or a compiled script.

     3.   Passed in using standard input.  This works only if there are no
          filename arguments; to pass arguments to a STDIN-read script, you
          must explicitly specify “-” for the script name.

     Any arguments following the script will be passed as a list of strings to
     the direct parameter of the “run” handler.  For example, in AppleScript:

           _a_._s_c_p_t_:
           on run argv
               return "hello, " & item 1 of argv & "."
           end run

           %% oossaassccrriipptt aa..ssccpptt wwoorrlldd
           hello, world.

     The options are as follows:

     --ee _s_t_a_t_e_m_e_n_t
           Enter one line of a script.  If --ee is given, oossaassccrriipptt will not
           look for a filename in the argument list.  Multiple --ee options may
           be given to build up a multi-line script.  Because most scripts use
           characters that are special to many shell programs (for example,
           AppleScript uses single and double quote marks, “(”, “)”, and “*”),
           the statement will have to be correctly quoted and escaped to get
           it past the shell intact.

     --ii    Interactive mode: oossaassccrriipptt will prompt for one line at a time, and
           print the result, if applicable, after each line.  Any script
           supplied as a command argument using --ee or _p_r_o_g_r_a_m_f_i_l_e will be
           loaded, but not executed, before starting the interactive prompt.

     --ll _l_a_n_g_u_a_g_e
           Override the language for any plain text files.  Normally, plain
           text files are compiled as AppleScript.

     --ss _f_l_a_g_s
           Modify the output style.  The _f_l_a_g_s argument is a string consisting
           of any of the modifier characters ee, hh, oo, and ss.  Multiple
           modifiers can be concatenated in the same string, and multiple --ss
           options can be specified.  The modifiers come in exclusive pairs;
           if conflicting modifiers are specified, the last one takes
           precedence.  The meanings of the modifier characters are as
           follows:

           hh  Print values in human-readable form (default).
           ss  Print values in recompilable source form.

              oossaassccrriipptt normally prints its results in human-readable form:
              strings do not have quotes around them, characters are not
              escaped, braces for lists and records are omitted, etc.  This is
              generally more useful, but can introduce ambiguities.  For
              example, the lists ‘{"foo", "bar"}’ and ‘{{"foo", {"bar"}}}’
              would both be displayed as ‘foo, bar’.  To see the results in an
              unambiguous form that could be recompiled into the same value,
              use the ss modifier.

           ee  Print script errors to stderr (default).
           oo  Print script errors to stdout.

              oossaassccrriipptt normally prints script errors to stderr, so downstream
              clients only see valid results.  When running automated tests,
              however, using the oo modifier lets you distinguish script
              errors, which you care about matching, from other diagnostic
              output, which you don't.

SSEEEE AALLSSOO
     osacompile(1), osalang(1), _A_p_p_l_e_S_c_r_i_p_t _L_a_n_g_u_a_g_e _G_u_i_d_e

HHIISSTTOORRYY
     oossaassccrriipptt in Mac OS X 10.0 would translate ‘\r’ characters in the output
     to ‘\n’ and provided cc and rr modifiers for the --ss option to change this.
     oossaassccrriipptt now always leaves the output alone; pipe through tr(1) if
     necessary.

     Prior to Mac OS X 10.4, oossaassccrriipptt did not allow passing arguments to the
     script.

Mac OS X                        April 24, 2014                        Mac OS X

```
