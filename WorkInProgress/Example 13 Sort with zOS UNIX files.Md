[z/OS](https://www.ibm.com/docs/en/zos)[2.1.0](https://www.ibm.com/docs/en/zos/2.1.0)

[Feedback](mailto:ibmdocs@us.ibm.com?Subject=Feedback to IBM Documentation&body=URL: https%3A%2F%2Fwww.ibm.com%2Fdocs%2Fen%2Fzos%2F2.1.0%3Ftopic%3Dexamples-example-13-sort-zos-unix-files)[Product list](https://www.ibm.com/docs/en/products)

![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zoshead.gif) **z/OS DFSORT Application Programming Guide** ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zosspot.gif)

| [Previous topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_12._Sort_with_INCLUDE_and_LOCALE.htm) \| [Next topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_14._Sort_with_IFTHEN.htm) \| [Contents](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/toc.htm) \| [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) \| [Library](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.ice/ice.htm) \| [PDF](http://publibz.boulder.ibm.com/epubs/pdf/ice2ca00.pdf)  ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/c.gif) Example 13: Sort with z/OS UNIX files  z/OS DFSORT Application Programming Guide SC23-6878-00 |
| ------------------------------------------------------------ |
| ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/dblue_rule.gif)INPUTConcatenated z/OS UNIX FilesOUTPUTz/OS UNIX FileWORK DATA SETSDynamically allocated (by default)USER EXITSNoneFUNCTIONS/OPTIONSNone`//EXAMP   JOB A400,PROGRAMMER                                   01 //S1      EXEC PGM=SORT                                         02 //SYSOUT  DD SYSOUT=A                                           03 //SORTIN  DD  PATH='/user/hfs.inp1.txt',PATHOPTS=ORDONLY,       04 //        LRECL=80,BLKSIZE=240,RECFM=FB,FILEDATA=TEXT           05 //        DD  PATH='/user/hfs.inp2.txt',PATHOPTS=ORDONLY,       06 //        LRECL=80,BLKSIZE=80,RECFM=F,FILEDATA=TEXT             07 //SORTOUT DD  PATH='/user/hfs.ut.txt',PATHOPTS=OWRONLY,         08 //        LRECL=80,BLKSIZE=80,RECFM=F,FILEDATA=TEXT             09 //SYSIN DD *                                                    10  SORT FIELDS=(10,8,CH,A)                                       11`**Line****Explanation**01JOB statement. Introduces this job to the operating system.02EXEC statement. Calls DFSORT directly by its alias name SORT.03SYSOUT DD statement. Directs DFSORT messages and control statements to system output class A.04-05SORTIN DD statement. The first input file is a z/OS UNIX file named /user/hfs.inp1.txt. Only read access is allowed. The file is defined as a text file. It has fixed-length records with a record size of 80 and a block size of 240.06-07The second input file is a z/OS UNIX file named /user/hfs.inp2.txt. Only read access is allowed. The file is defined as a text file. It has fixed-length records with a record size of 80 and a block size of 80.08-09SORTOUT DD statement. The output file is a z/OS UNIX file named /user/hfs.ut.txt. Only write access is allowed. The file is defined as a text file. It has fixed-length records with a record size of 80 and a block size of 80.10SYSIN DD statement. DFSORT control statements follow.11SORT statement. FIELDS specifies an ascending 8-byte character control field starting at position 10.**Parent topic:**[Sort examples](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Sort_examples.htm)[![Go to the previous page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pageback.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_12._Sort_with_INCLUDE_and_LOCALE.htm) ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagemid.gif) [![Go to the next page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagenext.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_14._Sort_with_IFTHEN.htm) |



[Notices](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zaddinfo.doc/notices.html) | [Terms of use](http://www.ibm.com/legal/us/) | [Support](http://www.ibm.com/servers/eserver/zseries/zos/support/) | [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) | [zFavorites](http://www-03.ibm.com/systems/z/os/zos/library/zfavorites/)   ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/copyright.gif)Copyright IBM Corporation 1990, 2014





PreviousExample 12. Sort with INCLUDE and LOCALE

NextExample 14. Sort with IFTHEN

Was this topic helpful?

YesNo



### 







### 















### 







### 



© Copyright IBM Corporation 2017, 2021