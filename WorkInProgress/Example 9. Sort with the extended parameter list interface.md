[z/OS](https://www.ibm.com/docs/en/zos)[2.1.0](https://www.ibm.com/docs/en/zos/2.1.0)

[Feedback](mailto:ibmdocs@us.ibm.com?Subject=Feedback to IBM Documentation&body=URL: https%3A%2F%2Fwww.ibm.com%2Fdocs%2Fen%2Fzos%2F2.1.0%3Ftopic%3Dexamples-example-9-sort-extended-parameter-list-interface)[Product list](https://www.ibm.com/docs/en/products)

![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zoshead.gif) **z/OS DFSORT Application Programming Guide** ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zosspot.gif)

| [Previous topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_8._Sort_with_dynamic_link-editing_of_exits.htm) \| [Next topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_10._Sort_with_OUTFIL.htm) \| [Contents](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/toc.htm) \| [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) \| [Library](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.ice/ice.htm) \| [PDF](http://publibz.boulder.ibm.com/epubs/pdf/ice2ca00.pdf)  ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/c.gif) Example 9. Sort with the extended parameter list interface  z/OS DFSORT Application Programming Guide SC23-6878-00 |
| ------------------------------------------------------------ |
| ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/dblue_rule.gif)INPUTFixed-length records from E15OUTPUTBlocked fixed-length records on SYSDAWORK DATA SETSDynamically allocatedUSER EXITSE15FUNCTIONS/OPTIONSOMIT, FILSZ, RESINV, DYNALLOCThe JCL for running program MYSORT, and highlights of the code used by MYSORT to invoke DFSORT with the extended parameter list, are shown below. For purposes of illustration, assume that none of the standard installation defaults for batch program invocation of DFSORT have been changed by the site.`//EXAMP    JOB A400,PROGRAMMER                                  01 //STEP1    EXEC PGM=MYSORT                                      02 //SYSOUT   DD SYSOUT=C                                          03 //MSGOUT   DD SYSOUT=C                                          04 //STEPLIB  DD DSN=A123456.LOAD,DISP=SHR                         05 //SORTOUT  DD DSN=&&OUTPUT,DISP=(,PASS),UNIT=SYSDA,             06 //  SPACE=(CYL,(8,4))                                           07 //SORTCNTL DD *                                                 08 * Update file size estimate                                     09  OPTION FILSZ=E30000                                           10 ----------------------------------------------------------------------- ----------------------------------------------------------------------- MYSORT CSECT                                                    11       .       .       .       LA   R1,PL1            SET ADDRESS OF PARAMETER LIST     12 *                              TO BE PASSED TO DFSORT           13       ST   R2,PL4            SET ADDRESS OF GETMAINED AREA     14 *                              TO BE PASSED TO E15              15       LINK EP=SORT           INVOKE DFSORT                     16       .       .       . PL1    DC   A(CTLST)          ADDRESS OF CONTROL STATEMENTS     17 PL2    DC   A(E15)            ADDRESS OF E15 ROUTINE            18 PL3    DC   A(0)              NO E35 ROUTINE                    19 PL4    DS   A                 USER EXIT ADDRESS CONSTANT        20 PL5    DC   F'-1'             INDICATE END OF LIST              21 CTLST  DS   0H                CONTROL STATEMENTS AREA           22       DC   AL2(CTL2-CTL1)    LENGTH OF CHARACTER STRING        23 CTL1   DC   C' SORT FIELDS=(5,8,CSF,A)'                         24       DC   C' RECORD TYPE=F,LENGTH=80 '                        25       DC   C' OPTION FILSZ=E25000,DYNALLOC,'                   26       DC   C'RESINV=8000 '                                     27       DC   C' OMIT FORMAT=CSF,COND=(5,8,EQ,13,8) '             28 CTL2   EQU  *                                                   29 OUT    DCB  DDNAME=MSGOUT,...                                   30 E15    DS   0H                E15 ROUTINE                       31       .       .       .       L    R2,4(,R1)         GET ADDRESS OF GETMAINED AREA     32       .       .       .       BR   R14               RETURN TO DFSORT                  33       .       .       .`**Line****Explanation**01JOB statement. Introduces this job to the operating system.02EXEC statement. Calls a program named MYSORT that in turn calls DFSORT.03SYSOUT DD statement. Directs DFSORT messages and control statements to SYSOUT class C.04MSGOUT DD statement. Directs MYSORT messages to SYSOUT class C.05STEPLIB DD statement. Specifies the load library that contains MYSORT.06-07SORTOUT DD statement. The output data set is temporary and is to be allocated on SYSDA. Because SORTIN is not used, DFSORT sets the RECFM and LRECL from the RECORD statement and sets the BLKSIZE to the LRECL (unblocked records).08SORTCNTL DD statement. DFSORT control statements follow. Statements in SORTCNTL override or supplement statements passed by MYSORT in the extended parameter list it uses.09Comment statement. Printed but otherwise ignored.10OPTION statement. FILSZ=E30000 specifies an estimate of 30000 records, overriding FILSZ=E25000 in the OPTION statement of the extended parameter list. Because the E15 routine supplies all of the input records, DFSORT will not be able to determine the file size accurately; therefore, specifying FILSZ can make a significant difference in work space optimization when an E15 routine supplies all of the input records. It's important to change the FILSZ value whenever the number of input records increases significantly.11This is the start of program MYSORT. Assume that it GETMAINs a work area, saves its address in register 2, and initializes it with information to be used by the E15 routine.12-13MYSORT places the address of the extended parameter list to be passed to DFSORT in register 1.14-15MYSORT places the address of the GETMAINed work area in the user exit address constant field in the extended parameter list. DFSORT will pass this address to the E15 routine (in the second word of the E15 parameter list) when it is entered.16MYSORT calls DFSORT by it's alias SORT.17-21The extended parameter list specifies: the address of the control statements area, the address of the E15 routine, that no E35 routine is present, and the address of the GETMAINed work area. F'-1' indicates the end of the extended parameter list. Subsequent parameter list fields, such as the address of an ALTSEQ table, are not used in this application.Because the address of the E15 routine is passed in the parameter list, SORTIN cannot be used; if a SORTIN DD statement were present, it would be ignored.22-23This is the start of the control statements area. The total length of the control statements is specified.24SORT statement. FIELDS specifies an ascending 8-byte floating-sign control field starting at position 5.25RECORD statement. TYPE=F and LENGTH=80 specify that the E15 inserts fixed-length records of 80 bytes. In this case, TYPE=F could be omitted, because DFSORT would automatically set a record type of F. However, LENGTH must be specified when an E15 supplies all of the input records.26-27OPTION statement. FILSZ=E25000 specifies an estimate of 25000 records, which is overridden by FILSZ=E30000 in SORTCNTL's OPTION statement. DYNALLOC specifies that work data sets are to be dynamically allocated using the installation defaults for the type of device and number of devices. RESINV=8000 specifies that approximately 8000 bytes are required for the system services (for example, GETMAIN and OPEN) that MYSORT's E15 exit routine performs.28OMIT statement. FORMAT specifies that the compare fields are floating-sign. COND specifies that input records with equal 8-byte floating-sign compare fields starting in position 5 (also the control field) and position 13 are to be omitted from the output data set.29This is the end of the control statements area.30This is the DCB for MYSORT's MSGOUT output.31-33This is MYSORT's E15 routine. The E15 routine loads the address of the GETMAINed work area from the second word of the E15 parameter list. The E15 routine must supply each input record by placing its address in register 1 and placing a 12 (insert) in register 15. When all the records have been passed, the E15 routine must place an 8 ("do not return") in register 15.**Parent topic:**[Sort examples](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Sort_examples.htm)[![Go to the previous page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pageback.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_8._Sort_with_dynamic_link-editing_of_exits.htm) ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagemid.gif) [![Go to the next page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagenext.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_10._Sort_with_OUTFIL.htm) |



[Notices](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zaddinfo.doc/notices.html) | [Terms of use](http://www.ibm.com/legal/us/) | [Support](http://www.ibm.com/servers/eserver/zseries/zos/support/) | [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) | [zFavorites](http://www-03.ibm.com/systems/z/os/zos/library/zfavorites/)   ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/copyright.gif)Copyright IBM Corporation 1990, 2014





PreviousExample 8. Sort with dynamic link-editing of exits

NextExample 10. Sort with OUTFIL

Was this topic helpful?

YesNo



### 







### 















### 







### 



© Copyright IBM Corporation 2017, 2021