**z/OS DFSORT Application Programming Guide** ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zosspot.gif)

| [Previous topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_4._Sort_with_E15__E35__FILSZ__AVGRLEN_and_DYNALLOC.htm) \| [Next topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_6._Sort_with_VSAM_input_output__DFSPARM_and_option_override_.htm) \| [Contents](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/toc.htm) \| [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) \| [Library](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.ice/ice.htm) \| [PDF](http://publibz.boulder.ibm.com/epubs/pdf/ice2ca00.pdf)  ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/c.gif) Example 5. Called sort with SORTCNTL, CHALT, DYNALLOC and FILSZ  z/OS DFSORT Application Programming Guide SC23-6878-00 |
| ------------------------------------------------------------ |
| ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/dblue_rule.gif)INPUTBlocked fixed-length records on diskOUTPUTBlocked fixed-length records on diskWORK DATA SETSDynamically allocatedUSER EXITSNoneFUNCTIONS/OPTIONSCHALT, DYNALLOC, FILSZ`//EXAMP    JOB A400,PROGRAMMER                                  01 //RUNSORT  EXEC PGM=MYPGM                                       02 //STEPLIB  DD DSN=M999999.LOAD,DISP=SHR                         03 //SYSOUT   DD SYSOUT=A                                          04 //SYSPRINT DD SYSOUT=A                                          05 //SORTIN   DD DSN=M999999.INPUT(MASTER),DISP=OLD                06 //SORTOUT  DD DSN=M999999.OUTPUT.FILE,DISP=OLD                  07 //SORTCNTL DD *                                                 08   OPTION  CHALT,DYNALLOC=(,3),FILSZ=U25000                     09`**Line****Explanation**01JOB statement. Introduces this job to the operating system.02EXEC statement. Calls a program named MYPGM that in turn calls DFSORT.03STEPLIB DD statement. Specifies the load library that contains MYPGM.04SYSOUT DD statement. Directs DFSORT messages and control statements to system output class A.05SYSPRINT DD statement. Directs MYPGM output to system output class A.06SORTIN DD statement. The input data set is member MASTER in the cataloged partitioned data set M999999.INPUT. DFSORT determines the RECFM, LRECL and BLKSIZE from the data set label.07SORTOUT DD statement. The output data set is named M999999.OUTPUT.FILE and is cataloged. DFSORT determines the RECFM, LRECL and BLKSIZE from the data set label.08SORTCNTL DD statement. DFSORT control statements follow. Statements in SORTCNTL override or supplement statements passed by MYPGM in the DFSORT parameter list it uses.09OPTION statement. CHALT specifies that character format control fields (specified in the SORT statement passed by MYPGM) are to be sorted using the ALTSEQ installation option. DYNALLOC=(,3) specifies that three work data sets are to be dynamically allocated using the installation default for the type of device. FILSZ=U25000 specifies a file size of 25000 records is to be used by DFSORT to determine the amount of work space needed. Because the input data set is a member of a PDS, specifying FILSZ helps DFSORT optimize work data set space.**Parent topic:**[Sort examples](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Sort_examples.htm)[![Go to the previous page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pageback.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_4._Sort_with_E15__E35__FILSZ__AVGRLEN_and_DYNALLOC.htm) ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagemid.gif) [![Go to the next page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagenext.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_6._Sort_with_VSAM_input_output__DFSPARM_and_option_override_.htm) |



[Notices](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zaddinfo.doc/notices.html) | [Terms of use](http://www.ibm.com/legal/us/) | [Support](http://www.ibm.com/servers/eserver/zseries/zos/support/) | [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) | [zFavorites](http://www-03.ibm.com/systems/z/os/zos/library/zfavorites/)   ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/copyright.gif)Copyright IBM Corporation 1990, 2014





PreviousExample 4. Sort with E15, E35, FILSZ, AVGRLEN and DYNALLOC

NextExample 6. Sort with VSAM input/output, DFSPARM and option override

Was this topic helpful?

YesNo



### 







### 















### 







### 



© Copyright IBM Corporation 2017, 2021