# man spctl

```text
SPCTL(8)                    System Manager's Manual                   SPCTL(8)

NNAAMMEE
     ssppccttll – SecAssessment system policy security

SSYYNNOOPPSSIISS
     ssppccttll _-_-_a_s_s_e_s_s [--tt _t_y_p_e] [--] _f_i_l_e _._._.
     ssppccttll _-_-_s_t_a_t_u_s
     ssppccttll _-_-_g_l_o_b_a_l_-_e_n_a_b_l_e
     ssppccttll _-_-_g_l_o_b_a_l_-_d_i_s_a_b_l_e | _-_-_d_i_s_a_b_l_e_-_s_t_a_t_u_s

DDEESSCCRRIIPPTTIIOONN
     ssppccttll manages the security assessment policy subsystem.

     This subsystem maintains and evaluates rules that determine whether the
     system allows the installation, execution, and other operations on files
     on the system.

     ssppccttll requires one command option that determines its principal
     operation:

     --aa,, ----aasssseessss
              Requests that ssppccttll perform an assessment on the _f_i_l_e_s given.

     ----gglloobbaall--eennaabbllee
              Enable the assessment subsystem.  Operations that are denied by
              system policy will fail; assessment APIs report the truth.
              Requires root access.

     ----gglloobbaall--ddiissaabbllee
              Reveal the option to allow applications downloaded from anywhere
              in the Privacy & Security settings pane.

     ----ddiissaabbllee--ssttaattuuss
              Query whether the option to allow applications downloaded from
              anywhere in the Privacy & Security settings pane is available.

     ----ssttaattuuss
              Query whether the assessment subsystem is enabled or disabled.

     In addition, the following options are recognized:

     ----ccoonnttiinnuuee
              If the assessment of a file fails, continue assessing additional
              file arguments.  Without this option, the first failed
              assessment terminates operation.

     ----iiggnnoorree--ccaacchhee
              Do not query or use the assessment object cache.  This may
              significantly slow down operation.  Newly generated assessments
              may still be stored in the cache.

     ----nnoo--ccaacchhee
              Do not place the outcome of any assessments into the assessment
              object cache.  No other assessment may reuse this outcome.  This
              option not prohibit the use of existing cache entries.

     ----rraaww    When displaying the outcome of an assessment, write it as a
              "raw" XML plist instead of parsing it in somewhat more friendly
              form.  This is useful when used in scripts, or to access newly
              invented assessment aspects that ssppccttll does not yet know about.

     --tt,, ----ttyyppee
              Specify which type of assessment is desired: _e_x_e_c_u_t_e to assess
              code execution, _i_n_s_t_a_l_l to assess installation of an installer
              package, and _o_p_e_n to assess the opening of documents.  The
              default is to assess execution.

     --vv,, ----vveerrbboossee
              Requests more verbose output.  Repeat the option or give it a
              higher numeric value to increase verbosity.

DDEEPPRREECCAATTEEDD OOPPTTIIOONNSS
     As of MacOS 15.0, operations that modify the rule database or the global
     state of the assessment subsystem will no longer be supported.

     To add rules with configuration profiles, please see
     https://developer.apple.com/documentation/devicemanagement/systempolicyrule

     To modify the global state with configuration profiles, please see
     https://developer.apple.com/documentation/devicemanagement/systempolicycontrol

     ----aadddd    Add rule(s) to the system-wide assessment rule database.

     ----ddiissaabbllee
              Disable one or more rules in the assessment rule database.
              Disabled rules are not considered when performing assessment,
              but remain in the database and can be re-enabled later.

     ----eennaabbllee
              Enable rule(s) in the assessment rule database, counteracting
              earlier disabling.

     ----rreemmoovvee
              Remove rule(s) from the assessment rule database.

     ----rreesseett--ddeeffaauulltt
              Unconditionally reset the system policy database to its default
              value. This discards all changes made by administrators. It also
              heals any corruption to the database. It does not implicitly
              either enable or disable the facility. This must be done as the
              super user. Reboot after use.

     ----aanncchhoorr
              In rule update operations, indicates that the arguments are
              hashes of anchor certificates.

     ----hhaasshh   In rule update operations, indicates that the arguments are code
              directory hashes.

     ----llaabbeell _l_a_b_e_l
              Specifies a string label to attach to new rules, or find in
              existing rules.  Labels are arbitrary strings that are assigned
              by convention.  Rule labels are optional.

     ----ppaatthh   In rule update operations, indicates that the argument(s) denote
              paths to files on disk.

     ----pprriioorriittyy _p_r_i_o_r_i_t_y
              In rule update operations, specifies the priority of the rule(s)
              created or changed.  Priorities are floating-point numbers.
              Higher numeric values indicate higher priority.

     ----rreeqquuiirreemmeenntt
              In rule update operations, indicates that the argument(s) are
              code requirement source.

     ----rruullee   In rule update operations, indicates that the argument(s) are
              the index numbers of existing rules.

RRUULLEE SSUUBBJJEECCTTSS
     The system assessement rule database contains entries that match
     candidates based on Code Requirements.  ssppccttll allows you to specify these
     requirements directly using the ----rreeqquuiirreemmeenntt option.  In addition,
     individual programs on disk can be addressed with the --path option
     (which uses their Designated Requirement).  The ----aanncchhoorr option takes the
     hash of a (full) certificate and turns it into a requirement matching any
     signature based on that anchor certificate.  Alternatively, it can take
     the absolute path of a certificate file on disk, containing the DER form
     of an anchor certificate.  Finally, the ----hhaasshh option generates a code
     requirement that denotes only and exactly one program whose CodeDirectory
     hash is given.  The means of specifying subjects does not affect the
     remaining processing.

FFIILLEESS
     _/_v_a_r_/_d_b_/_S_y_s_t_e_m_P_o_l_i_c_y_C_o_n_f_i_g_u_r_a_t_i_o_n_/_S_y_s_t_e_m_P_o_l_i_c_y           The system
                                                              policy database.
     _/_v_a_r_/_d_b_/_S_y_s_t_e_m_P_o_l_i_c_y_C_o_n_f_i_g_u_r_a_t_i_o_n_/_._S_y_s_t_e_m_P_o_l_i_c_y_-_d_e_f_a_u_l_t  A copy of the
                                                              initial
                                                              distribution
                                                              version of the
                                                              system policy
                                                              database.
                                                              Useful for
                                                              starting over if
                                                              the database
                                                              gets messed up
                                                              beyond
                                                              recognition.

EEXXAAMMPPLLEESS
     To check whether Mail.app is allowed to run on the local system:
           spctl -a /Applications/Mail.app
     To check whether the assessment subsystem is enabled:
           spctl --status

DDIIAAGGNNOOSSTTIICCSS
     ssppccttll exits zero on success, or one if an operation has failed.  Exit
     code two indicates unrecognized or unsuitable arguments.  If an
     assessment operation results in denial but no other problem has occurred,
     the exit code is three. Exit code four indicates the operation is now
     deprecated.

SSEEEE AALLSSOO
     codesign(1), syspolicyd(1)

HHIISSTTOORRYY
     The system policy facility and ssppccttll command first appeared in Mac OS X
     Lion 10.7.3 as a limited developer preview.

macOS 26.3                     January 19, 2012                     macOS 26.3

```
