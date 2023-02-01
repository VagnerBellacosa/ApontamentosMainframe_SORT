[z/OS](https://www.ibm.com/docs/en/zos)[2.1.0](https://www.ibm.com/docs/en/zos/2.1.0)

[Feedback](mailto:ibmdocs@us.ibm.com?Subject=Feedback to IBM Documentation&body=URL: https%3A%2F%2Fwww.ibm.com%2Fdocs%2Fen%2Fzos%2F2.1.0%3Ftopic%3Dexamples-example-3-sort-ascii-tapes)[Product list](https://www.ibm.com/docs/en/products)

![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zoshead.gif) **z/OS DFSORT Application Programming Guide** ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zosspot.gif)

| [Previous topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_2._Sort_with_OMIT__SUM__OUTREC__DYNALLOC_and_ZDPRINT.htm) \| [Next topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_4._Sort_with_E15__E35__FILSZ__AVGRLEN_and_DYNALLOC.htm) \| [Contents](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/toc.htm) \| [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) \| [Library](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.ice/ice.htm) \| [PDF](http://publibz.boulder.ibm.com/epubs/pdf/ice2ca00.pdf)  ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/c.gif) Example 3. Sort with ASCII tapes  z/OS DFSORT Application Programming Guide SC23-6878-00 |
| ------------------------------------------------------------ |
| ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/dblue_rule.gif)INPUTVariable-length ASCII records on 3590OUTPUTVariable-length ASCII records on 3590WORK DATA SETSOne SYSDA data setUSER EXITSNoneFUNCTIONS/OPTIONSNone`//EXAMP    JOB A400,PROGRAMMER                                  01 //RUNIT    EXEC SORTD                                           02 //SORTIN   DD DSN=SRTFIL,DISP=(OLD,DELETE),UNIT=3590,           03 //  DCB=(RECFM=D,LRECL=400,BLKSIZE=404,OPTCD=Q,BUFOFF=L),       04 //  VOL=SER=311500,LABEL=(1,AL)                                 05 //SORTOUT  DD DSN=OUTFIL,UNIT=3590,LABEL=(,AL),DISP=(,KEEP),    06 //  DCB=(BLKSIZE=404,OPTCD=Q,BUFOFF=L),VOL=SER=311501           07 //SORTWK01 DD UNIT=SYSDA,SPACE=(CYL,(4))                        08 //SYSIN    DD *                                                 09  SORT FIELDS=(10,8,AC,D)                                       10  RECORD TYPE=D,LENGTH=(,,,20,80)                               11`**Line****Explanation**01JOB statement. Introduces this job to the operating system.02EXEC statement. Uses the SORTD cataloged procedure to call DFSORT directly.03-05SORTIN DD statement. The input data set is named SRTFIL and resides on 3590 volume 311500. It is to be deleted after this job step. It has a RECFM of D (variable-length ASCII records), a maximum LRECL of 400, a BLKSIZE of 404 and an ASCII label. For this job, the buffer offset is the block length indicator. The records are to be translated from ASCII to EBCDIC.06-07SORTOUT DD statement. The output data set is named OUTFIL and is to be allocated on 3590 volume 311501 and kept. It is to be written with an ASCII label. DFSORT sets the RECFM and LRECL from SORTIN and sets the BLKSIZE to 404 as indicated in the DD statement. For this job, the buffer offset is the block length indicator. The records are to be translated from EBCDIC to ASCII.08SORTWK01 DD statement. The work data set is allocated on SYSDA.09SYSIN DD statement. DFSORT control statements follow.10SORT statement. FIELDS specifies a descending 8-byte ASCII control field starting at position 10.11RECORD statement. TYPE specifies ASCII variable-length records. LENGTH specifies that the minimum record length is 20 and the average record length is 80.**Parent topic:**[Sort examples](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Sort_examples.htm)[![Go to the previous page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pageback.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_2._Sort_with_OMIT__SUM__OUTREC__DYNALLOC_and_ZDPRINT.htm) ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagemid.gif) [![Go to the next page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagenext.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_4._Sort_with_E15__E35__FILSZ__AVGRLEN_and_DYNALLOC.htm) |



[Notices](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zaddinfo.doc/notices.html) | [Terms of use](http://www.ibm.com/legal/us/) | [Support](http://www.ibm.com/servers/eserver/zseries/zos/support/) | [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) | [zFavorites](http://www-03.ibm.com/systems/z/os/zos/library/zfavorites/)   ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/copyright.gif)Copyright IBM Corporation 1990, 2014





PreviousExample 2. Sort with OMIT, SUM, OUTREC, DYNALLOC and ZDPRINT

NextExample 4. Sort with E15, E35, FILSZ, AVGRLEN and DYNALLOC

Was this topic helpful?

YesNo



### 







### 















### 







### 



© Copyright IBM Corporation 2017, 2021