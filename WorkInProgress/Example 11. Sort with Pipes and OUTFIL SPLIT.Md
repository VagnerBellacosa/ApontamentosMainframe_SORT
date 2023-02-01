[z/OS](https://www.ibm.com/docs/en/zos)[2.1.0](https://www.ibm.com/docs/en/zos/2.1.0)

[Feedback](mailto:ibmdocs@us.ibm.com?Subject=Feedback to IBM Documentation&body=URL: https%3A%2F%2Fwww.ibm.com%2Fdocs%2Fen%2Fzos%2F2.1.0%3Ftopic%3Dexamples-example-11-sort-pipes-outfil-split)[Product list](https://www.ibm.com/docs/en/products)

![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zoshead.gif) **z/OS DFSORT Application Programming Guide** ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zosspot.gif)

| [Previous topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_10._Sort_with_OUTFIL.htm) \| [Next topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_12._Sort_with_INCLUDE_and_LOCALE.htm) \| [Contents](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/toc.htm) \| [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) \| [Library](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.ice/ice.htm) \| [PDF](http://publibz.boulder.ibm.com/epubs/pdf/ice2ca00.pdf)  ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/c.gif) Example 11. Sort with Pipes and OUTFIL SPLIT  z/OS DFSORT Application Programming Guide SC23-6878-00 |
| ------------------------------------------------------------ |
| ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/dblue_rule.gif)INPUTPipesOUTPUTPipesWORK DATA SETSDynamically allocatedUSER EXITSNoneFUNCTIONS/OPTIONSFILSZ, OUTFIL, DYNALLOC`//EXAMP   JOB A400,PROGRAMMER                                   01 //RUNSORT EXEC PGM=ICEMAN                                       02 //SYSOUT  DD SYSOUT=H                                           03 //SORTIN  DD DSN=INPUT.PIPE,SUBSYS=PIPE,                        04 //           DCB=(LRECL=60,RECFM=FB,BLKSIZE=32760)              05 //OUT1    DD DSN=OUTPUT.PIPE1,SUBSYS=PIPE,                      06 //           DCB=(LRECL=60,RECFM=FB,BLKSIZE=32760)              07 //OUT2    DD DSN=OUTPUT.PIPE2,SUBSYS=PIPE,                      08 //           DCB=(LRECL=60,RECFM=FB,BLKSIZE=32760)              09 //SYSIN   DD *                                                  10  OPTION DYNALLOC,FILSZ=U1000000                                11  SORT FIELDS=(1,20,CH,A,25,4,BI,A)                             12  OUTFIL FNAMES=(OUT1,OUT2),SPLIT                               13`**Line****Explanation**01Job statement. Introduces this job to the operating system.02EXEC statement. Calls DFSORT directly.03SYSOUT DD statement. Directs DFSORT messages and control statements to system output class H.04-05SORTIN DD statement. The SUBSYS=PIPE parameter directs the allocation to the 'PIPE' subsystem for the pipe named INPUT.PIPE. The DCB statement describes the data set characteristics to subsystem PIPE.06-07OUT1 DD statement. The SUBSYS=PIPE parameter directs the allocation to the 'PIPE' subsystem for the pipe named OUTPUT.PIPE1. The DCB statement describes the data set characteristics to subsystem PIPE.08-09OUT2 DD statement. The SUBSYS=PIPE parameter directs the allocation to the 'PIPE' subsystem for the pipe named OUTPUT.PIPE2. The DCB statement describes the data set characteristics to subsystem PIPE.10SYSIN DD statement. DFSORT control statements follow.11OPTION statement. DYNALLOC specifies that work data sets are to be dynamically allocated using the installation defaults for type of device and number of devices. FILSZ=U1000000 specifies an estimate of one million input records.12SORT statement. FIELDS specifies an ascending 20-byte character control field starting at position 1 and an ascending 4 byte binary control field starting at position 25.13OUTFIL statement. The records from the SORTIN pipe are sorted and written alternatively to the OUT1 and OUT2 pipes (that is, the sorted records are split evenly between the two output pipes).**Parent topic:**[Sort examples](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Sort_examples.htm)[![Go to the previous page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pageback.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_10._Sort_with_OUTFIL.htm) ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagemid.gif) [![Go to the next page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagenext.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_12._Sort_with_INCLUDE_and_LOCALE.htm) |



[Notices](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zaddinfo.doc/notices.html) | [Terms of use](http://www.ibm.com/legal/us/) | [Support](http://www.ibm.com/servers/eserver/zseries/zos/support/) | [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) | [zFavorites](http://www-03.ibm.com/systems/z/os/zos/library/zfavorites/)   ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/copyright.gif)Copyright IBM Corporation 1990, 2014





PreviousExample 10. Sort with OUTFIL

NextExample 12. Sort with INCLUDE and LOCALE

Was this topic helpful?

YesNo



### 







### 















### 







### 



© Copyright IBM Corporation 2017, 2021