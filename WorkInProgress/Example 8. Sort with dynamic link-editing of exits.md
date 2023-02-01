[z/OS](https://www.ibm.com/docs/en/zos)[2.1.0](https://www.ibm.com/docs/en/zos/2.1.0)

[Feedback](mailto:ibmdocs@us.ibm.com?Subject=Feedback to IBM Documentation&body=URL: https%3A%2F%2Fwww.ibm.com%2Fdocs%2Fen%2Fzos%2F2.1.0%3Ftopic%3Dexamples-example-8-sort-dynamic-link-editing-exits)[Product list](https://www.ibm.com/docs/en/products)

![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zoshead.gif) **z/OS DFSORT Application Programming Guide** ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zosspot.gif)

| [Previous topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_7._Sort_with_COBOL_E15__EXEC_PARM_and_MSGDDN.htm) \| [Next topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_9._Sort_with_the_extended_parameter_list_interface.htm) \| [Contents](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/toc.htm) \| [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) \| [Library](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.ice/ice.htm) \| [PDF](http://publibz.boulder.ibm.com/epubs/pdf/ice2ca00.pdf)  ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/c.gif) Example 8. Sort with dynamic link-editing of exits  z/OS DFSORT Application Programming Guide SC23-6878-00 |
| ------------------------------------------------------------ |
| ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/dblue_rule.gif)INPUTBlocked fixed-length records on diskOUTPUTBlocked fixed-length records on 3380WORK DATA SETSOne SYSDA data setUSER EXITSE11, E15, E17, E18, E19, E31, E35, E38, E39FUNCTIONS/OPTIONSNone`//EXAMP    JOB A400,PROGRAMMER                                  01 //STEPA    EXEC SORT                                            02 //SORTIN   DD DSN=SMITH.INPUT,DISP=SHR                          03 //SORTOUT  DD DSN=SMITH.OUTPUT,DISP=(NEW,CATLG),                04 //  UNIT=3380,SPACE=(TRK,(10,2)),VOL=SER=XYZ003                 05 //SORTWK01 DD UNIT=SYSDA,SPACE=(CYL,(1,1))                      06 //EXIT     DD DSN=SMITH.EXIT.OBJ,DISP=SHR                       07 //EXIT2    DD DSN=SMITH.EXIT2.OBJ,DISP=SHR                      08 //SORTMODS DD UNIT=SYSDA,SPACE=(TRK,(10,,3))                    09 //SYSIN    DD *                                                 10  SORT FIELDS=(1,8,CH,A,20,4,BI,D)                              11  MODS E11=(EXIT11,1024,EXIT,S),                                12       E15=(E15,1024,SYSIN,T),                                  13       E17=(EXIT17,1024,EXIT2,T),                               14       E18=(EXIT18,1024,EXIT,T),                                15       E19=(E19,1024,SYSIN,T),                                  16       E31=(PH3EXIT,1024,EXIT,T),                               17       E35=(PH3EXIT,1024,EXIT,T),                               18       E38=(PH3EXIT,1024,EXIT,T),                               19       E39=(E39,1024,SYSIN,T)                                   20  END                                                           21 <object deck for E15 exit here>                                 22 <object deck for E19 exit here>                                 23 <object deck for E39 exit here>                                 24`**Line****Explanation**01JOB statement. Introduces this job to the operating system.02EXEC statement. Uses the SORT cataloged procedure to call DFSORT directly and supply the DD statements (not shown) required by the linkage editor.03SORTIN DD statement. The input data set is named SMITH.INPUT and is cataloged. DFSORT determines the RECFM, LRECL and BLKSIZE from the data set label.04-05SORTOUT DD statement. The output data set is named SMITH.OUTPUT and is to be allocated on 3380 volume XYZ003 and cataloged. DFSORT sets the RECFM and LRECL from SORTIN and selects an appropriate BLKSIZE.06SORTWK01 DD statement. The work data set is allocated on SYSDA.07EXIT DD statement. Specifies the partitioned data set containing the object decks for the E11, E18, E31, E35 and E38 exit routines.08EXIT2 DD statement. Specifies the partitioned data set containing the object deck for the E17 exit routine.09SORTMODS DD statement. The partitioned data set to hold exit routine object decks from SYSIN for input to the linkage editor is to be allocated on SYSDA.10SYSIN DD statement. DFSORT control statements, and object decks to be used by the linkage editor, follow.11SORT statement. FIELDS specifies an ascending 8-byte character control field starting at position 1 and a descending 4-byte binary control field starting at position 20.12-20MODS statement. Specifies the exit routines to be used, the approximate number of bytes required for each exit and that:The EXIT11 routine in the EXIT library is to be link-edited separately from other input phase exit routines and associated with user exit E11.The E15 and E19 routines in SYSIN, the EXIT17 routine in EXIT2, and the EXIT18 routine in EXIT are to be link-edited together and associated with user exits E15, E19, E17, and E18, respectively.The E31, E35, and E38 routines in the PH3EXIT object deck and the E39 routine in SYSIN are to be link-edited together and associated with user exits E31, E35, E38, and E39, respectively.21END statement. Marks the end of the DFSORT control statements and the beginning of the exit routine object decks.22-24Object decks. The three object decks for the E15, E19, and E39 exit routines follow the END statement.**Parent topic:**[Sort examples](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Sort_examples.htm)[![Go to the previous page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pageback.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_7._Sort_with_COBOL_E15__EXEC_PARM_and_MSGDDN.htm) ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagemid.gif) [![Go to the next page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagenext.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_9._Sort_with_the_extended_parameter_list_interface.htm) |



[Notices](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zaddinfo.doc/notices.html) | [Terms of use](http://www.ibm.com/legal/us/) | [Support](http://www.ibm.com/servers/eserver/zseries/zos/support/) | [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) | [zFavorites](http://www-03.ibm.com/systems/z/os/zos/library/zfavorites/)   ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/copyright.gif)Copyright IBM Corporation 1990, 2014





PreviousExample 7. Sort with COBOL E15, EXEC PARM and MSGDDN

NextExample 9. Sort with the extended parameter list interface

Was this topic helpful?

YesNo



### 







### 















### 







### 



© Copyright IBM Corporation 2017, 2021