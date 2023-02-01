[z/OS](https://www.ibm.com/docs/en/zos)[2.1.0](https://www.ibm.com/docs/en/zos/2.1.0)

[Feedback](mailto:ibmdocs@us.ibm.com?Subject=Feedback to IBM Documentation&body=URL: https%3A%2F%2Fwww.ibm.com%2Fdocs%2Fen%2Fzos%2F2.1.0%3Ftopic%3Dse-example-7-sort-cobol-e15-exec-parm-msgddn)[Product list](https://www.ibm.com/docs/en/products)

![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zoshead.gif) **z/OS DFSORT Application Programming Guide** ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zosspot.gif)

| [Previous topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_6._Sort_with_VSAM_input_output__DFSPARM_and_option_override_.htm) \| [Next topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_8._Sort_with_dynamic_link-editing_of_exits.htm) \| [Contents](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/toc.htm) \| [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) \| [Library](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.ice/ice.htm) \| [PDF](http://publibz.boulder.ibm.com/epubs/pdf/ice2ca00.pdf)  ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/c.gif) Example 7. Sort with COBOL E15, EXEC PARM and MSGDDN  z/OS DFSORT Application Programming Guide SC23-6878-00 |
| ------------------------------------------------------------ |
| ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/dblue_rule.gif)INPUTFixed-length records on diskOUTPUTFixed-length records on SYSDAWORK DATA SETSNoneUSER EXITSCOBOL E15FUNCTIONS/OPTIONSMSGDDN`//EXAMP    JOB A400,PROGRAMMER                                  01 //STEP1    EXEC PGM=SORT,PARM='MSGDDN=DFSOUT'                   02 //STEPLIB  DD DSN=SYS1.SCEERUN,DISP=SHR                         03 //SYSOUT   DD SYSOUT=A                                          04 //DFSOUT   DD SYSOUT=A                                          05 //EXITC    DD DSN=COBEXITS.LOADLIB,DISP=SHR                     06 //SORTIN   DD DSN=SORT1.IN,DISP=SHR                             07 //SORTOUT  DD DSN=&&OUT,DISP=(,PASS),SPACE=(CYL,(5,5)),         08 //  UNIT=SYSDA,DCB=(LRECL=120)                                  09 //SYSIN    DD *                                                 10  SORT FIELDS=(5,4,A,22,2,A),FORMAT=BI                          11  MODS E15=(COBOLE15,37000,EXITC,C)                             12  RECORD LENGTH=(,120)                                          13`**Line****Explanation**01JOB statement. Introduces this job to the operating system.02EXEC statement. Calls DFSORT directly by its alias name SORT. MSGDDN=DFSOUT specifies an alternate message data set for DFSORT messages and control statements to prevent the COBOL messages in SYSOUT from being interleaved with the DFSORT messages and control statements.03STEPLIB statement. Specifies the Language Environment library.04SYSOUT statement. Directs COBOL messages to system output class A.05DFSOUT statement. Directs DFSORT messages and control statements to system output class A (this is the alternate message data set specified by MSGDDN in the PARM field of the EXEC statement).06EXITC statement. Specifies the load library that contains the exit routine.07SORTIN DD statement. The input data set is named SORT1.IN and is cataloged. DFSORT determines from the data set label that the RECFM is F, the LRECL is 100 and the BLKSIZE is 100.08-09SORTOUT DD statement. The output data set is temporary and is to be allocated on SYSDA. Because the E15 exit changes the length of the records from 100 bytes to 120 bytes, LRECL=120 must be specified. DFSORT sets the RECFM from SORTIN and sets the BLKSIZE to the LRECL (unblocked records).10SYSIN DD statement. DFSORT control statements follow.11SORT statement. FIELDS specifies an ascending 4-byte control field starting at position 5 and an ascending 2-byte control field starting at position 22. FORMAT specifies that the control fields are binary.12MODS statement. E15 specifies a user exit routine named COBOLE15 written in COBOL. Approximately 37000 bytes are required for the exit, the system services (for example, GETMAIN and OPEN) it performs, and the COBOL library subroutines. COBOLE15 resides in the library defined by the EXITC DD statement.13RECORD statement. LENGTH specifies that the COBOL E15 routine changes the length of the records to 120 bytes.**Parent topic:**[Sort examples](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Sort_examples.htm)[![Go to the previous page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pageback.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_6._Sort_with_VSAM_input_output__DFSPARM_and_option_override_.htm) ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagemid.gif) [![Go to the next page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagenext.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_8._Sort_with_dynamic_link-editing_of_exits.htm) |



[Notices](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zaddinfo.doc/notices.html) | [Terms of use](http://www.ibm.com/legal/us/) | [Support](http://www.ibm.com/servers/eserver/zseries/zos/support/) | [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) | [zFavorites](http://www-03.ibm.com/systems/z/os/zos/library/zfavorites/)   ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/copyright.gif)Copyright IBM Corporation 1990, 2014





PreviousExample 6. Sort with VSAM input/output, DFSPARM and option override

NextExample 8. Sort with dynamic link-editing of exits

Was this topic helpful?

YesNo



### 







### 















### 







### 



© Copyright IBM Corporation 2017, 2021