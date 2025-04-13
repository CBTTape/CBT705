# CBT705
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. GitHub repos will be deleted and created during this period...

```
//***FILE 705 is from David Cartwright and contains some tools      *   FILE 705
//*           to do performance tuning on a Flex-ES machine which   *   FILE 705
//*           is running z/OS.  These tools use TSSO console        *   FILE 705
//*           automation from File 404 of the CBT Tape.             *   FILE 705
//*                                                                 *   FILE 705
//*           email:  davecartwright@uk.agcocorp.com                *   FILE 705
//*                                                                 *   FILE 705
//*    A description of the content of this file follows:           *   FILE 705
//*                                                                 *   FILE 705
//*     This file illustrates some of the work done at AGCO UK      *   FILE 705
//*     Coventry to use TSSO from file 404 for the CBT tape to      *   FILE 705
//*     control an MVS system running under Flex-ES.  The           *   FILE 705
//*     members start with;                                         *   FILE 705
//*                                                                 *   FILE 705
//*     TIMER - this is the main clist which drives the other       *   FILE 705
//*     members. This is invoked by AOF processing by some          *   FILE 705
//*     message which appears at fixed intervals.  I have two       *   FILE 705
//*     main threads driven by this clist;                          *   FILE 705
//*                                                                 *   FILE 705
//*     PERFORMANCE MEASUREMENT                                     *   FILE 705
//*     =======================                                     *   FILE 705
//*     We were moving production off an IBM Multiprise 2003        *   FILE 705
//*     which had an excess of MIPS and which had a good disk       *   FILE 705
//*     subsystem of an EMC Symmetrix on four ESCON channels.       *   FILE 705
//*     Our IMS response times were variable and our overnight      *   FILE 705
//*     BMP jobs had very elongated run times.  These               *   FILE 705
//*     applications are very cache unfriendly, but the EMC box     *   FILE 705
//*     had so much cache it didn't matter.  We started to          *   FILE 705
//*     monitor the Flex-ES cachestatistics for our disk            *   FILE 705
//*     controllers.  Our best bet would be to scrap the            *   FILE 705
//*     individual track caches and assign cache at the Control     *   FILE 705
//*     Unit level.  This is then shared out by Flex-ES as          *   FILE 705
//*     demand requires.  I continue to collect Flex-ES cache       *   FILE 705
//*     statistics, although I now rarely bother to look at         *   FILE 705
//*     them.  The TSSO members used for this activity are;         *   FILE 705
//*                                                                 *   FILE 705
//*     CONFIG - Our Flex-ES configuration file which can be        *   FILE 705
//*     tied to the other stuff.  It illustrates our cache          *   FILE 705
//*     definitions.                                                *   FILE 705
//*                                                                 *   FILE 705
//*     CACHE - Every hour this TSSO clist runs commands on the     *   FILE 705
//*     Flex-ES system to collect Flex-ES cachestatistics for       *   FILE 705
//*     every disk controller defined in the config file and        *   FILE 705
//*     appends them to a Unixware file.                            *   FILE 705
//*                                                                 *   FILE 705
//*     FLEXJ01 - is a batch job that TIMER submits just before     *   FILE 705
//*     midnight each day.  It takes a snapshot of Unixware         *   FILE 705
//*     memory usage over the last 24 hours which is appended       *   FILE 705
//*     to the cachestatistics file.  This file is then FTP'd       *   FILE 705
//*     over to a mainframe GDG so I have a history that I can      *   FILE 705
//*     browse from ISPF.                                           *   FILE 705
//*                                                                 *   FILE 705
//*     REPORT - is a sample output from FLEXJ01.                   *   FILE 705
//*                                                                 *   FILE 705
//*     RESET - a clist which is called at the end of FLEJ01 to     *   FILE 705
//*     write an end-of-file at the start of the cachestastics      *   FILE 705
//*     file ready to collect another day's worth of data.          *   FILE 705
//*                                                                 *   FILE 705
//*     STORAGE MANAGEMENT                                          *   FILE 705
//*     ==================                                          *   FILE 705
//*     Another function of TIMER is to automate various HSM        *   FILE 705
//*     housekeeping commands such as DELVOL.                       *   FILE 705
//*     The Storage Management members are;                         *   FILE 705
//*                                                                 *   FILE 705
//*     STORAGE - This clist monitors the non-SMS disks and         *   FILE 705
//*     switches them from STORAGE to PRIVATE if they get too       *   FILE 705
//*     full and vice-versa as they empty.                          *   FILE 705
//*                                                                 *   FILE 705
//*     SYSDA - this REXX uses the VTOC command off the CBT         *   FILE 705
//*     tape to monitor allocations on a few disks that I           *   FILE 705
//*     called SYSDA.                                               *   FILE 705
//*                                                                 *   FILE 705
```
