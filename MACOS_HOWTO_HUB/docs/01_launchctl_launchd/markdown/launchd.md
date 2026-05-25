# man launchd

```text
launchd(8)                  System Manager's Manual                 launchd(8)

NNAAMMEE
     llaauunncchhdd – System wide and per-user daemon/agent manager

DDEESSCCRRIIPPTTIIOONN
     llaauunncchhdd manages processes, both for the system as a whole and for
     individual users.

     The primary and preferred interface to llaauunncchhdd is via the launchctl(1)
     tool which (among other options) allows the user or administrator to load
     and unload jobs. Where possible, it is preferable for jobs to launch on
     demand based on criteria specified in their respective configuration
     files.

     llaauunncchhdd also manages XPC services that are bundled within applications
     and frameworks on the system.

     During boot llaauunncchhdd is invoked by the kernel to run as the first process
     on the system and to further bootstrap the rest of the system.

     You cannot invoke llaauunncchhdd directly.

NNOOTTEESS
     On Darwin operating systems, the canonical way to launch a daemon is
     through llaauunncchhdd as opposed to traditional POSIX and POSIX-like mechanisms
     or mechanisms provided in earlier versions of OS X. These alternate
     methods should be considered deprecated and not suitable for new
     projects.

     In the llaauunncchhdd lexicon, a daemon is, by definition, a system-wide service
     of which there is one instance for all clients. An agent is a service
     that runs on a per-user basis.  Daemons should not attempt to display UI
     or interact directly with a user's login session. Any and all work that
     involves interacting with a user should be done through agents.

     XPC services which are marked with a ServiceType of System are
     functionally equivalent to daemons and run in the same environment,
     sharing the same Mach bootstrap namespace. XPC services which are marked
     with a ServiceType of User are equivalent to agents with the
     LimitLoadToSessionType key specifying the Background session and run in
     the same environment, sharing the same Mach bootstrap namespace. See
     launchd.plist(5) for more information about user sessions.

     On Darwin platforms, a user environment includes a specific Mach
     bootstrap subset, audit session and other characteristics not recognized
     by POSIX.  Therefore, making the appropriate setuid(2) and setgid(2)
     system calls is not sufficient to completely assume the identity for a
     given user. Running a service as a llaauunncchhdd agent or a per-user XPC
     service is the only way to run a process with a complete identity of that
     user.

FFIILLEESS
     _~_/_L_i_b_r_a_r_y_/_L_a_u_n_c_h_A_g_e_n_t_s         Per-user agents provided by the user.
     _/_L_i_b_r_a_r_y_/_L_a_u_n_c_h_A_g_e_n_t_s          Per-user agents provided by the
                                    administrator.
     _/_L_i_b_r_a_r_y_/_L_a_u_n_c_h_D_a_e_m_o_n_s         System-wide daemons provided by the
                                    administrator.
     _/_S_y_s_t_e_m_/_L_i_b_r_a_r_y_/_L_a_u_n_c_h_A_g_e_n_t_s   Per-user agents provided by Apple.
     _/_S_y_s_t_e_m_/_L_i_b_r_a_r_y_/_L_a_u_n_c_h_D_a_e_m_o_n_s  System-wide daemons provided by Apple.

SSEEEE AALLSSOO
     launchctl(1), launchd.plist(5),

DDEEVVEELLOOPPEERR DDOOCCUUMMEENNTTAATTIIOONN
     The Daemons and Services Programming Guide can be found at the following
     URL:

     hhttttppss::////ddeevveellooppeerr..aappppllee..ccoomm//lliibbrraarryy//ccoonntteenntt//ddooccuummeennttaattiioonn//MMaaccOOSSXX//CCoonncceeppttuuaall//BBPPSSyysstteemmSSttaarrttuupp//CChhaapptteerrss//IInnttrroodduuccttiioonn..hhttmmll

Darwin                         25 November, 2013                        Darwin

```
