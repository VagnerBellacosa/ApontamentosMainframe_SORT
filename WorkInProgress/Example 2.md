[z/OS](https://www.ibm.com/docs/en/zos)[2.1.0](https://www.ibm.com/docs/en/zos/2.1.0)

[Feedback](mailto:ibmdocs@us.ibm.com?Subject=Feedback to IBM Documentation&body=URL: https%3A%2F%2Fwww.ibm.com%2Fdocs%2Fen%2Fzos%2F2.1.0%3Ftopic%3Dse-example-2-1)[Product list](https://www.ibm.com/docs/en/products)

![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zoshead.gif) **z/OS DFSORT Application Programming Guide** ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/zosspot.gif)

| [Previous topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_136.htm) \| [Next topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_317.htm) \| [Contents](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/toc.htm) \| [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) \| [Library](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.ice/ice.htm) \| [PDF](http://publibz.boulder.ibm.com/epubs/pdf/ice2ca00.pdf)  ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/c.gif) Example 2  z/OS DFSORT Application Programming Guide SC23-6878-00 |
| ------------------------------------------------------------ |
| ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/dblue_rule.gif)` * Method 1 SORT FROM(IN) TO(DEPT1) USING(DPT1) SORT FROM(IN) TO(DEPT2) USING(DPT2) SORT FROM(IN) TO(DEPT3) USING(DPT3)`` * Method 2 SORT FROM(IN) USING(ALL3)`This example shows two different methods for creating sorted subsets of an input data set. Assume that:The DPT1CNTL data set contains:` SORT FIELDS=(51,2,BI,A,18,5,CH,A,58,4,BI,A) INCLUDE COND=(5,3,CH,EQ,C'D01')`The DPT2CNTL data set contains:` SORT FIELDS=(51,2,BI,A,18,5,CH,A,58,4,BI,A) INCLUDE COND=(5,3,CH,EQ,C'D02')`The DPT3CNTL data set contains:` SORT FIELDS=(51,2,BI,A,18,5,CH,A,58,4,BI,A) INCLUDE COND=(5,3,CH,EQ,C'D03')`The ALL3CNTL data set contains:` SORT FIELDS=(51,2,BI,A,18,5,CH,A,58,4,BI,A) OUTFIL FNAMES=DEPT1,INCLUDE=(5,3,CH,EQ,C'D01') OUTFIL FNAMES=DEPT2,INCLUDE=(5,3,CH,EQ,C'D02') OUTFIL FNAMES=DEPT3,INCLUDE=(5,3,CH,EQ,C'D03')`Method 1 requires three calls to DFSORT and three passes over the input data set:The first SORT operator sorts the records from the IN data set that contain D01 in positions 5-7 to the DEPT1 data setThe second COPY operator sorts the records from the IN data set that contain D02 in positions 5-7 to the DEPT2 data setThe third COPY operator sorts the records from the IN data set that contain D03 in positions 5-7 to the DEPT3 data set.Method 2 accomplishes the same result as method 1 but, because it uses OUTFIL statements instead of TO operands, requires only one call to DFSORT and one pass over the input data set.**Parent topic:**[Sort examples](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_SORT_examples.htm)[![Go to the previous page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pageback.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_136.htm) ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagemid.gif) [![Go to the next page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/pagenext.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/ice2ca_Example_317.htm) |



[Notices](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zaddinfo.doc/notices.html) | [Terms of use](http://www.ibm.com/legal/us/) | [Support](http://www.ibm.com/servers/eserver/zseries/zos/support/) | [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) | [zFavorites](http://www-03.ibm.com/systems/z/os/zos/library/zfavorites/)   ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.icea100/copyright.gif)Copyright IBM Corporation 1990, 2014





PreviousExample 1

NextExample 3

Was this topic helpful?

YesNo



### 







### 















### 







### 



© Copyright IBM Corporation 2017, 2021