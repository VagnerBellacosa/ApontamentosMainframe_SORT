[z/OS](https://www.ibm.com/docs/en/zos)[2.1.0](https://www.ibm.com/docs/en/zos/2.1.0)

[Feedback](mailto:ibmdocs@us.ibm.com?Subject=Feedback to IBM Documentation&body=URL: https%3A%2F%2Fwww.ibm.com%2Fdocs%2Fen%2Fzos%2F2.1.0%3Ftopic%3Dexamples-example-10-sort-outfil)[Product list](https://www.ibm.com/docs/en/products)

![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zoshead.gif) **z/OS DFSORT Application Programming Guide** ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zosspot.gif)

| [Previous topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_9._Sort_with_the_extended_parameter_list_interface.htm) \| [Next topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_11._Sort_with_Pipes_and_OUTFIL_SPLIT.htm) \| [Contents](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/toc.htm) \| [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) \| [Library](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.ice/ice.htm) \| [PDF](http://publibz.boulder.ibm.com/epubs/pdf/ice2ca00.pdf)  ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/c.gif) Example 10. Sort with OUTFIL  z/OS DFSORT Application Programming Guide SC23-6878-00 |
| ------------------------------------------------------------ |
| ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/dblue_rule.gif)INPUTFixed-length record data setOUTPUTMultiple fixed-length record data setsWORK DATA SETSDynamically allocated (by default)USER EXITSNoneFUNCTIONS/OPTIONSOUTFIL`//EXAMP    JOB A400,PROGRAMMER                                  01 //OUTFIL   EXEC  PGM=SORT                                       02 //SYSOUT   DD  SYSOUT=A                                         03 //SORTIN   DD DSN=GRP.RECORDS,DISP=SHR                          04 //ALLGPS   DD DSN=GRP.ALLGRPS,DISP=OLD                          05 //ALLBU    DD DSN=GRP.BU,DISP=(NEW,CATLG,DELETE),               06 //            UNIT=3390,SPACE=(TRK,(10,10))                     07 //G1STATS  DD SYSOUT=A                                          08 //G2STATS  DD SYSOUT=A                                          09 //SYSIN    DD    *                                              10 SORT FIELDS=(6,5,CH,A)                                         11  OUTFIL FNAMES=(ALLGPS,ALLBU)                                   12  OUTFIL FNAMES=G1STATS,                                         13   INCLUDE=(1,3,CH,EQ,C'G01'),                                  14   HEADER2=(1:'GROUP 1 STATUS REPORT FOR ',&DATE,               15              ' - PAGE ',&PAGE,2/,                              16            6:'ITEM ',16:'STATUS      ',31:'PARTS',/,           17            6:'-----',16:'------------',31:'-----'),            18    OUTREC=(6:6,5,                                              19            16:14,1,CHANGE=(12,                                 20                            C'1',C'SHIP',                       21                            C'2',C'HOLD',                       22                            C'3',C'TRANSFER'),                  23                    NOMATCH=(C'*CHECK CODE*'),                  24            31:39,1,BI,M10,LENGTH=5,                            25            120:X)                                              26  OUTFIL FNAMES=G2STATS,                                         27   INCLUDE=(1,3,CH,EQ,C'G02'),                                  28   HEADER2=(1:'GROUP 2 STATUS REPORT FOR ',&DATE,               29              ' - PAGE ',&PAGE,2/,                              30            6:'ITEM ',16:'STATUS      ',31:'PARTS',/,           31            6:'-----',16:'------------',31:'-----'),            32    OUTREC=(6:6,5,                                              33            16:14,1,CHANGE=(12,                                 34                            C'1',C'SHIP',                       35                            C'2',C'HOLD',                       36                            C'3',C'TRANSFER'),                  37                    NOMATCH=(C'*CHECK CODE*'),                  38            31:39,1,BI,M10,LENGTH=5,                            39            120:X)                                              40`**Line****Explanation**01JOB statement. Introduces this job to the operating system.02EXEC statement. Calls DFSORT directly by its alias name SORT.03SYSOUT DD statement. Directs DFSORT messages and control statements to sysout class A.04SORTIN DD statement. The input data set is named GRP.RECORDS and is cataloged. DFSORT determines from the data set label that the RECFM is FB, the LRECL is 80 and the BLKSIZE is 23440.05ALLGPS DD statement. The first OUTFIL output data set is named GRP.ALLGRPS and is catalogued. DFSORT determines the RECFM, LRECL and BLKSIZE from the data set label.06-07ALLBU DD statement. The second OUTFIL output data set is named GRP.BU and is to be allocated on a 3390 and catalogued. DFSORT sets the RECFM and LRECL from SORTIN and selects an appropriate BLKSIZE.08G1STATS DD statement. The third OUTFIL output data set is directed to sysout class A. Because this is an OUTFIL report data set, DFSORT sets the RECFM to FBA (FB from SORTIN and A for ANSI control characters) and the LRECL to 121 (1 byte for the ANSI control character and 120 bytes for the data). DFSORT sets an appropriate BLKSIZE.09G2STATS DD statement. The fourth OUTFIL output data set is directed to sysout class A. Because this is an OUTFIL report data set, DFSORT sets the RECFM to FBA (FB from SORTIN and A for ANSI control characters) and the LRECL to 121 (1 byte for the ANSI control character and 120 bytes for the data). DFSORT sets an appropriate BLKSIZE.10SYSIN DD statement. DFSORT control statements follow.11SORT statement. FIELDS specifies an ascending 5-byte character control field starting at position 6.12OUTFIL statement. The sorted input records are written to the ALLGPS and ALLBU data sets.13-26OUTFIL statement. The subset of sorted input records containing 'G01' in positions 1 through 3 are used to produce a report, which is written to the G1STATS data set.27-40OUTFIL statement. The subset of sorted input records containing 'G02' in positions 1 through 3 are used to produce a report, which is written to the G2STATS data set.**Parent topic:**[Sort examples](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Sort_examples.htm)[![Go to the previous page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pageback.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_9._Sort_with_the_extended_parameter_list_interface.htm) ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagemid.gif) [![Go to the next page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagenext.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_11._Sort_with_Pipes_and_OUTFIL_SPLIT.htm) |



[Notices](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zaddinfo.doc/notices.html) | [Terms of use](http://www.ibm.com/legal/us/) | [Support](http://www.ibm.com/servers/eserver/zseries/zos/support/) | [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) | [zFavorites](http://www-03.ibm.com/systems/z/os/zos/library/zfavorites/)   ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/copyright.gif)Copyright IBM Corporation 1990, 2014





PreviousExample 9. Sort with the extended parameter list interface

NextExample 11. Sort with Pipes and OUTFIL SPLIT

Was this topic helpful?

YesNo



### 







### 















### 







### 



© Copyright IBM Corporation 2017, 2021