<!-- loio5fc23232fe1447c09f0a17c876c63c54 -->

# Define EDI Extractor

EDI Extractor enables you to extract EDI headers and transfer to camel headers. This element extracts data from single incoming EDI document and adds it to the exchange such that this information can be used further in message processing. EDI extractor can read both flat file and XML format.



## Context

> ### Remember:  
> This component or some of its features might not be available in the Cloud Foundry environment. For more information on the limitations, see SAP Note [2752867](https://launchpad.support.sap.com/#/notes/2752867).

EDI Extractor supports EDIFACT, EANCOM, ODETTE, and ASC-X12 documents.



<a name="loio5fc23232fe1447c09f0a17c876c63c54__steps_hsv_5rn_35"/>

## Procedure

1.  In the graphical editor of integration flow, choose the *EDI Extractor* element.

2.  Define a parameter for the extractor.

3.  If you want to continue editing the integration package without exiting, choose *Save*.

4.  Choose *Save as version* to retain a copy of the current artifact.

5.  If you want to terminate the creation of package, choose *Cancel* before saving it.

    > ### Note:  
    > -   Any EDIFACT message is an interchange. An interchange can have multiple groups. And each group consists of message types. For EDIFACT message, the EDI elements in SAP Cloud Integration support only 1 message type per interchange but does not support any group segment \(GS\) per interchange segment.
    > -   Any ASC-X12 message is an interchange. An interchange can have multiple groups. And each group consists of transaction sets. For ASC-X12 message, the EDI elements in SAP Cloud Integration support only 1 group segment \(GS\) per interchange segment and only 1 transaction set \(ST\) per group segment.
    > -   SAP Cloud Integration does not support repetition characters. Repetition character is a single character which separates the instances of a repeating data element. For example, *^* \(caret sign\) is a repetition character.
    > -   In a ODETTE message payload, provide the value for *SAP\_EDI\_Document\_Standard* header as ***ODETTE***.




**EANCOM Document Standard**

The following segments are part of message payload of EANCOM, and the table below mentions the headers and values for the given payload.

UNB+UNOC:3+**4006501000002**:**14**+**5790000016839**:**14**+100818:0028+**0650**+++++XXXXX'

UNH+1+**INVOIC**:**D**:**96A**:**EN:EAN008**'

<a name="loio5fc23232fe1447c09f0a17c876c63c54__d468e52"/>Value for EANCOM Document Standard


<table>
<tr>
<th valign="top">

Header Name



</th>
<th valign="top">

Value



</th>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Document\_Standard



</td>
<td valign="top">

UN-EDIFACT



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Interchange\_Control\_Number



</td>
<td valign="top">

1



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Message\_Association\_Assign\_Code



</td>
<td valign="top">

EAN008



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Message\_Control\_Number



</td>
<td valign="top">

1



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Message\_Controlling\_Agency



</td>
<td valign="top">

UN



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Message\_Release



</td>
<td valign="top">

96A



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Message\_Type



</td>
<td valign="top">

ORDERS



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Message\_Version



</td>
<td valign="top">

D



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Payload\_Format



</td>
<td valign="top">

EDI\_FLAT



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Processing\_Priority\_Code



</td>
<td valign="top">

A



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Receiver\_ID



</td>
<td valign="top">

RECIPIENT ID



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Receiver\_Routing\_Address



</td>
<td valign="top">

INT ROUT



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Recipient\_Reference\_Password



</td>
<td valign="top">

PASSWORD RCV



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Receiver\_ID\_Qualifier



</td>
<td valign="top">

14



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Sender\_ID



</td>
<td valign="top">

SENDER ID



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Sender\_ID\_Qualifier



</td>
<td valign="top">

14



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Sender\_Reverse\_Routing\_Address



</td>
<td valign="top">

REV ROUT



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Syntax\_Identifier



</td>
<td valign="top">

UNOC



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Syntax\_Version\_Number



</td>
<td valign="top">

3



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Test\_Indicator



</td>
<td valign="top">

1



</td>
</tr>
</table>

**EDIFACT Document Standard**

The element creates camel headers and populates it with respective extracted values. For example, if following segments are part of message payload of EDIFACT, then respective headers and values for the same are given in the table below.

UNB+UNOC:3+**4006501000002**:**14**+**5790000016839**:**14**+100818:0028+**0650**+++++XXXXX'

UNH+1+**INVOIC**:**D**:**96A**:**UN**'

<a name="loio5fc23232fe1447c09f0a17c876c63c54__d468e397"/>Value for EDIFACT Document Standard


<table>
<tr>
<th valign="top">

Header Name



</th>
<th valign="top">

Value



</th>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Payload\_Format



</td>
<td valign="top">

XML or Flat-File



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Document\_Standard



</td>
<td valign="top">

UN-EDIFACT



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Sender\_ID



</td>
<td valign="top">

4006501000002



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Sender\_ID\_Qualifier



</td>
<td valign="top">

14



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Receiver\_ID



</td>
<td valign="top">

5790000016839



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Receiver\_ID\_Qualifier



</td>
<td valign="top">

14



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Interchange\_Control\_Number



</td>
<td valign="top">

0650



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Message\_Type



</td>
<td valign="top">

INVOIC



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Message\_Version



</td>
<td valign="top">

D



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Message\_Release



</td>
<td valign="top">

96A



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Message\_Controlling\_Agency



</td>
<td valign="top">

UN



</td>
</tr>
</table>

**ASC-X12 Document Standard**

If following segments are part of message payload of ASC-X12 , then respective headers and values for the same are given in the table below.

ISA\*00\* \*00\* \***ZZ**\***WWRESNDR** \***ZZ**\***WWRERCVR** \*020709\*0816\*U\*00401\***000046668**\*0\*P\*:~

GS\*IN\*GSRESNDR\*GSRERCVR\*20030709\*0816\*12345\*X\***004010**~

**810**\*0001~

<a name="loio5fc23232fe1447c09f0a17c876c63c54__d468e628"/>Value for ASC-X12 Document Standard


<table>
<tr>
<th valign="top">

Header Name



</th>
<th valign="top">

Value



</th>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Payload\_Format



</td>
<td valign="top">

XML or Flat-File



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Document\_Standard



</td>
<td valign="top">

ASC-X12



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Sender\_ID



</td>
<td valign="top">

WWRESNDR



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Sender\_ID\_Qualifier



</td>
<td valign="top">

ZZ



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Receiver\_ID



</td>
<td valign="top">

WWRERCVR



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Receiver\_ID\_Qualifier



</td>
<td valign="top">

ZZ



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Interchange\_Control\_Number



</td>
<td valign="top">

000046668



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Message\_Type



</td>
<td valign="top">

810



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Message\_Version



</td>
<td valign="top">

004010



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_GS\_Sender\_ID



</td>
<td valign="top">

GSRESNDR



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_Receiver\_ID



</td>
<td valign="top">

GSRERCVR



</td>
</tr>
<tr>
<td valign="top">

SAP\_EDI\_GS\_Control\_Number



</td>
<td valign="top">

12345



</td>
</tr>
<tr>
<td valign="top">

SAP\_GS\_Functional\_Id\_Code



</td>
<td valign="top">

IN



</td>
</tr>
<tr>
<td valign="top">

SAP\_GS\_Responsible\_Agency\_Code



</td>
<td valign="top">

X



</td>
</tr>
<tr>
<td valign="top">

SAP\_ISA\_Acknowledgment\_Requested



</td>
<td valign="top">

0



</td>
</tr>
<tr>
<td valign="top">

SAP\_ISA\_Auth\_Information\_Qualifier



</td>
<td valign="top">

00



</td>
</tr>
<tr>
<td valign="top">

SAP\_ISA\_Control\_Standards\_Identifier



</td>
<td valign="top">



</td>
</tr>
<tr>
<td valign="top">

SAP\_ ISA\_Security\_Information\_Qualifier



</td>
<td valign="top">

00



</td>
</tr>
<tr>
<td valign="top">

SAP\_ISA\_Usage\_Indicator



</td>
<td valign="top">

P



</td>
</tr>
<tr>
<td valign="top">

SAP\_ISA\_Version\_Number



</td>
<td valign="top">

004010



</td>
</tr>
<tr>
<td valign="top">

SAP\_MessageProcessingLogID



</td>
<td valign="top">



</td>
</tr>
<tr>
<td valign="top">

SAP\_ST\_Control\_Number



</td>
<td valign="top">



</td>
</tr>
</table>

