[z/OS](https://www.ibm.com/docs/en/zos)[2.1.0](https://www.ibm.com/docs/en/zos/2.1.0)

[Feedback](mailto:ibmdocs@us.ibm.com?Subject=Feedback to IBM Documentation&body=URL: https%3A%2F%2Fwww.ibm.com%2Fdocs%2Fen%2Fzos%2F2.1.0%3Ftopic%3Dse-example-6-sort-vsam-inputoutput-dfsparm-option-override)[Product list](https://www.ibm.com/docs/en/products)

![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zoshead.gif) **z/OS DFSORT Application Programming Guide** ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zosspot.gif)

| [Previous topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_5._Called_sort_with_SORTCNTL__CHALT__DYNALLOC_and_FILSZ.htm) \| [Next topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_7._Sort_with_COBOL_E15__EXEC_PARM_and_MSGDDN.htm) \| [Contents](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/toc.htm) \| [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) \| [Library](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.ice/ice.htm) \| [PDF](http://publibz.boulder.ibm.com/epubs/pdf/ice2ca00.pdf)  ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/c.gif) Example 6. Sort with VSAM input/output, DFSPARM and option override  z/OS DFSORT Application Programming Guide SC23-6878-00 |
| ------------------------------------------------------------ |
| ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/dblue_rule.gif)INPUTVSAM TYPE=V recordsOUTPUTVSAM TYPE=V recordsWORK DATA SETSDynamically allocatedUSER EXITSNoneFUNCTIONS/OPTIONSOverride of Various Options`//EXAMP    JOB A400,PROGRAMMER                                  01 //S1       EXEC PGM=SORT                                        02 //SYSOUT   DD SYSOUT=A                                          03 //SORTIN   DD DSN=TEST.SORTIN.FILE,DISP=SHR                     04 //SORTOUT  DD DSN=TEST.SORTOUT.FILE,DISP=SHR                    05 //DFSPARM  DD *                                                 06  RECORD TYPE=V                                                 07  SORT FIELDS=(30,4,BI,A)                                       08  OPTION HIPRMAX=10,DYNALLOC=3390,MAINSIZE=3M,                  09    MSGPRT=CRITICAL,NOLIST                                      10`For purposes of illustration, assume that none of the standard installation defaults for batch direct invocation of DFSORT have been changed by the site.**Line****Explanation**01JOB statement. Introduces this job to the operating system.02EXEC statement. Calls DFSORT directly by its alias SORT.03SYSOUT DD statement. Directs DFSORT messages and control statements to system output class A.04SORTIN DD statement. The input data set is TEST.SORTIN.FILE. DFSORT determines that it is a VSAM data set and obtains its attributes from the catalog.05SORTOUT DD statement. The output data set is TEST.SORTOUT.FILE. DFSORT determines that it is a VSAM data set and obtains its attributes from the catalog.06DFSPARM DD statement. DFSORT control statements follow. DFSPARM can be used for both direct-invocation and program-invocation of DFSORT and overrides options and statements from all other sources. Certain operands, such as MSGPRT and LIST/NOLIST, are used if supplied in DFSPARM, the EXEC PARM or the invocation parameter list, but not used if supplied in SYSIN or SORTCNTL.07RECORD statement. TYPE=V specifies that DFSORT is to treat the VSAM records as variable-length. In this case, the RECORD statement could be omitted, because DFSORT would automatically set a record type of V due to the use of VSAM data sets for SORTIN and SORTOUT.08SORT statement. FIELDS specifies an ascending 4-byte binary control field starting at position 30. This position corresponds to a specification of KEYS(4 25) for the VSAM CLUSTER (4 bytes at offset 25, which is equivalent to position 26 with 4 bytes added for the RDW that DFSORT supplies at input and removes at output for VSAM TYPE=V records).09-10OPTION statement. HIPRMAX=10 specifies that up to 10 MBs of Hiperspace can be used for Hipersorting, overriding the standard installation default of HIPRMAX=OPTIMAL. DYNALLOC=3390 specifies that work data sets are to be allocated on 3390s, overriding the standard installation default of SYSDA. The standard installation default of four work data sets is not overridden. MAINSIZE=3M specifies that up to 3 MBs of storage can be used, overriding the standard installation default of MAINSIZE=MAX. MSGPRT=CRITICAL specifies that only error messages are to be printed, overriding the standard installation default of MSGPRT=ALL. NOLIST specifies that control statements are not to be printed, overriding the standard installation default of LIST=YES.**Parent topic:**[Sort examples](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Sort_examples.htm)[![Go to the previous page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pageback.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_5._Called_sort_with_SORTCNTL__CHALT__DYNALLOC_and_FILSZ.htm) ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagemid.gif) [![Go to the next page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagenext.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_7._Sort_with_COBOL_E15__EXEC_PARM_and_MSGDDN.htm) |



[Notices](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zaddinfo.doc/notices.html) | [Terms of use](http://www.ibm.com/legal/us/) | [Support](http://www.ibm.com/servers/eserver/zseries/zos/support/) | [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) | [zFavorites](http://www-03.ibm.com/systems/z/os/zos/library/zfavorites/)   ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/copyright.gif)Copyright IBM Corporation 1990, 2014





PreviousExample 5. Called sort with SORTCNTL, CHALT, DYNALLOC and FILSZ

NextExample 7. Sort with COBOL E15, EXEC PARM and MSGDDN

Was this topic helpful?

YesNo



### 







### 















### 







### 



© Copyright IBM Corporation 2017, 2021