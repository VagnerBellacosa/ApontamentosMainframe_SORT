[z/OS](https://www.ibm.com/docs/en/zos)[2.1.0](https://www.ibm.com/docs/en/zos/2.1.0)

[Feedback](mailto:ibmdocs@us.ibm.com?Subject=Feedback to IBM Documentation&body=URL: https%3A%2F%2Fwww.ibm.com%2Fdocs%2Fen%2Fzos%2F2.1.0%3Ftopic%3Dse-example-2-sort-omit-sum-outrec-dynalloc-zdprint)[Product list](https://www.ibm.com/docs/en/products)

![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zoshead.gif) **z/OS DFSORT Application Programming Guide** ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zosspot.gif)

| [Previous topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_1._Sort_with_ALTSEQ.htm) \| [Next topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_3._Sort_with_ASCII_tapes.htm) \| [Contents](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/toc.htm) \| [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) \| [Library](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.ice/ice.htm) \| [PDF](http://publibz.boulder.ibm.com/epubs/pdf/ice2ca00.pdf)  ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/c.gif) Example 2. Sort with OMIT, SUM, OUTREC, DYNALLOC and ZDPRINT  z/OS DFSORT Application Programming Guide SC23-6878-00 |
| ------------------------------------------------------------ |
| ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/dblue_rule.gif)INPUTBlocked fixed-length records on 3380 and 3390OUTPUTBlocked fixed-length records on 3390WORK DATA SETSDynamically allocatedUSER EXITSNoneFUNCTIONS/OPTIONSOMIT, OUTREC, SUM, DYNALLOC, ZDPRINT`//EXAMP    JOB A400,PROGRAMMER                                  01 //STEP1    EXEC PGM=SORT                                        02 //SYSOUT   DD SYSOUT=H                                          03 //SORTIN   DD DSN=INP1,DISP=SHR,UNIT=3380,VOL=SER=SCR001        04 //         DD DSN=INP2,DISP=SHR,UNIT=3390,VOL=SER=SYS351        05 //SORTOUT  DD DSN=&&OUTPUT,DISP=(,PASS),UNIT=3390,              06 //   SPACE=(CYL,(5,1)),DCB=(LRECL=22)                           07 //SYSIN    DD *                                                 08  OMIT COND=(5,1,CH,EQ,C'M')                                    09  SORT FIELDS=(20,8,CH,A,10,3,FI,D)                             10  SUM FIELDS=(16,4,ZD)                                          11  OPTION DYNALLOC,ZDPRINT                                       12  OUTREC FIELDS=(10,3,20,8,16,4,2Z,5,1,C' SUM')                 13`**Line****Explanation**01JOB statement. Introduces this job to the operating system.02EXEC statement. Calls DFSORT directly by its alias SORT.03SYSOUT DD statement. Directs DFSORT messages and control statements to system output class H.04-05SORTIN DD statement. Consists of a concatenation of two data sets. The first input data set is named INP1 and resides on 3380 volume SCR001. The second input data set is named INP2 and resides on 3390 volume SYS351. DFSORT determines from the data set labels that the record format is FB, the LRECL is 80 and the largest BLKSIZE is 27920.06-07SORTOUT DD statement. The output data set is temporary and is to be allocated on a 3390. Because the OUTREC statement results in a reformatted output record length of 22 bytes, LRECL=22 must be specified. DFSORT sets the RECFM from SORTIN and selects an appropriate BLKSIZE.08SYSIN DD statement. DFSORT control statements follow.09OMIT statement. COND specifies that input records with a character M in position 5 are to be omitted from the output data set.10SORT statement. FIELDS specifies an ascending 8-byte character control field starting at position 20 and a descending 3-byte fixed-point control field starting at position 10.11SUM statement. FIELDS specifies a 4-byte zoned-decimal summary field starting at position 16. Whenever two records with the same control fields (specified in the SORT statement) are found, their summary fields (specified in the SUM statement) are to be added and placed in one of the records, and the other record is to be deleted.12OPTION statement. DYNALLOC specifies that work data sets are to be dynamically allocated using the installation defaults for the type of device and number of devices. ZDPRINT specifies that positive ZD SUM fields are to be printable.13OUTREC statement. FIELDS specifies how the records are to be reformatted for output. The reformatted records are 22 bytes long and look as follows:**Position****Content**1-3Input positions 10 through 124-11Input positions 20 through 2712-15Input positions 16 through 1916-17Zeros18Input position 519-22The character string ' SUM'**Parent topic:**[Sort examples](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Sort_examples.htm)[![Go to the previous page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pageback.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_1._Sort_with_ALTSEQ.htm) ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagemid.gif) [![Go to the next page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagenext.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_3._Sort_with_ASCII_tapes.htm) |



[Notices](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zaddinfo.doc/notices.html) | [Terms of use](http://www.ibm.com/legal/us/) | [Support](http://www.ibm.com/servers/eserver/zseries/zos/support/) | [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) | [zFavorites](http://www-03.ibm.com/systems/z/os/zos/library/zfavorites/)   ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/copyright.gif)Copyright IBM Corporation 1990, 2014





PreviousExample 1. Sort with ALTSEQ

NextExample 3. Sort with ASCII tapes

Was this topic helpful?

YesNo



### 







### 















### 







### 



© Copyright IBM Corporation 2017, 2021