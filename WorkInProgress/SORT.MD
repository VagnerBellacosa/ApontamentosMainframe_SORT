[Feedback](mailto:ibmdocs@us.ibm.com?Subject=Feedback to IBM Documentation&body=URL: https%3A%2F%2Fwww.ibm.com%2Fdocs%2Fen%2Fzos%2F2.1.0%3Ftopic%3Dcommands-sort-sort-data)[Product list](https://www.ibm.com/docs/en/products)

![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/zoshead.gif) **z/OS ISPF Edit and Edit Macros** ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/zosspot.gif)

| [Previous topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/setund.htm) \| [Next topic](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/source.htm) \| [Contents](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/toc.htm) \| [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) \| [Library](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.isp/isp.htm) \| [PDF](http://publibz.boulder.ibm.com/epubs/pdf/isp2em00.pdf)  ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/c.gif) SORT—Sort Data  z/OS ISPF Edit and Edit Macros SC19-3621-00 |
| ------------------------------------------------------------ |
| ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/dblue_rule.gif)The SORT primary command puts data in a specified order.SyntaxLast Updated: 2021-03-22`![Read syntax diagram](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/c.gif)![Skip visual syntax diagram](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/c.gif)        .-.ZFIRST--.ZLAST-.                                  >>-SORT--+-----------------+--+----+--+--------------------+---><        '-*labela*--*labelb*--'  +-X--+  | .----------------. |                              '-NX-'  | V                | |                                      '---| sort_field |-+-'   sort_field   .-A-.                          |--+---+--*start_col*--+---------+--------------------------------|  '-D-'             '-*end_col*-'   `*labela*, *labelb*Labels identifying the start and end of the group of lines to be sorted.For more information about using labels to identify a group of lines, see [Labels and line ranges](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/linergn.htm#linergn).XSorts only lines that are excluded.NXSorts only lines that are not excluded.*sort_field*Specifies the field to be used in sorting data. You can specify up to five sort fields using these operands:ASpecifies ascending order. It can either precede or follow the column specification.DSpecifies descending order. It can either precede or follow the column specification.*start_col*Defines the starting column of the field that is to be compared. It must be within the current boundaries.*end_col*Defines the ending column of the field that is to be compared. It must be within the current boundaries. If it is not supplied, then the ending column is the current right boundary. For more information on boundaries, see [Edit boundaries](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/bounds.htm#bounds).If you specify several fields, you must specify both the starting and ending columns of each field. The fields cannot overlap. If you supply the sort order for one field, you must supply it for all fields.DescriptionLast Updated: 2021-03-22SORT operates in two different modes, based on the hexadecimal mode status. If hexadecimal mode is on, the data is ordered according to its hexadecimal representation. If hexadecimal mode is off, data is sorted in the collating sequence defined for the national language being used.Sorting data without operandsLast Updated: 2021-03-22For SORT with no operands, the editor compares the data within the current boundaries character by character, and then orders it line by line in the proper collating sequence. It ignores data outside the current boundaries during both operations. Therefore only the data inside the current boundaries is changed. Labels, excluded lines, line numbers, and change, error, and special line flags are considered associated with the data, and therefore point to the same data fields after the sort as they did before the sort.For example, if you issue a CHANGE ALL that changes the first, third, and sixth lines in a data set, these lines are flagged with the change flag, ==CHG>. If you then issue a SORT command that results in the former lines 1, 3, and 6 becoming the first, second and third lines of the sorted file, the changed line flags would now exist on the first, second and third lines of the sorted data set.It is important to properly set the boundaries before issuing SORT. SORT is a powerful tool for editing data that may be formatted in multiple columns. You can set the boundaries, for example, to the first half of a record and sort one column of data. Then you can set the boundaries to the last half of the record and sort a second column of data.Limiting the SORT commandLast Updated: 2021-03-22Sorting is limited to data within the current boundaries. You can specify up to five sort fields by labeling starting and ending columns. You can also identify each field as having data sorted in either ascending or descending order.Optionally, you can limit sorting to a range of lines by specifying the labels of the first and last lines of the range. You can also limit sorting to either excluded or non-excluded lines.If you have labels or line ranges that are between the labels or line ranges specified with SORT, you can keep SORT from rearranging them by:Excluding them before you enter SORTUsing the NX operand to sort only lines that are not excludedFor more information, see the definition of the NX operand and [EXCLUDE—Exclude Lines from the Display](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/exclude.htm#exclude).Sorting DBCS dataLast Updated: 2021-03-22When sorting data that contains DBCS character strings, you must ensure that no DBCS string crosses the boundaries. Also, all records must have the same format at the boundaries, although the format of the left and right boundaries can differ.If a boundary divides a DBCS character, or if all records do not have the same format at the boundaries, the result is unpredictable.ExamplesLast Updated: 2021-03-22This form of the SORT command sorts in ascending order. The start-column is the left boundary and the end-column is the right boundary:`SORT`This form of the SORT command sorts in descending order. The start-column is the left boundary and the end-column is the right boundary:`SORT D`This form of the SORT command sorts in ascending order. The start-column is column 5 and the end-column is the right boundary:`SORT 5`This form of the SORT command sorts in descending order. The start-column is column 5 and the end-column is the right boundary:`SORT 5 D`**Parent topic:**[Edit primary commands](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/prime.htm)[![Go to the previous page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/pageback.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/setund.htm) ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/pagemid.gif) [![Go to the next page](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/pagenext.gif)](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/source.htm) |



[Notices](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zaddinfo.doc/notices.html) | [Terms of use](http://www.ibm.com/legal/us/) | [Support](http://www.ibm.com/servers/eserver/zseries/zos/support/) | [Contact z/OS](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zcontact.doc/webqs.html) | [zFavorites](http://www-03.ibm.com/systems/z/os/zos/library/zfavorites/)   ![img](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.f54em00/copyright.gif)Copyright IBM Corporation 1990, 2014





PreviousSETUNDO-Set the UNDO Mode

NextSOURCE-describe format of data

Was this topic helpful?

YesNo



### 







### 















### 







### 



© Copyright IBM Corporation 2017, 2021