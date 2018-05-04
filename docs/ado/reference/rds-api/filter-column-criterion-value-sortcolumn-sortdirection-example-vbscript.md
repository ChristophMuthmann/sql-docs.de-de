---
title: Legen Sie RDS. DataControl-Server und binden Sie HTML-Tabelle (VBScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- FilterColumn property [ADO], VBScript example
- FilterCriterion property [ADO], VBScript example
- SortDirection property [RDS], VBScript example
- Reset method [ADO], VBScript example
- SortColumn property [RDS], VBScript example
- FilterValue property [ADO], VBScript example
ms.assetid: 8a74802f-34d6-4676-bf94-07df5f8bff66
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3563a44e39ba7c5e83076350ad4346f6af661b3a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="filtercolumn-filtercriterion-filtervalue-sortcolumn-and-sortdirection-properties-and-reset-method-example-vbscript"></a>FilterColumn, FilterCriterion, FilterValue, SortColumn, SortDirection Eigenschaften und Reset-Methode (Beispiel) (VBScript)
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Der folgende Code veranschaulicht das Festlegen der [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) **Server** Parameter bei Designtime und es auf einen Daten-fähigen HTML Tabelle mithilfe einer Datenquelle binden. Ausschneiden und fügen Sie den folgenden Code in Editor oder einem anderen Texteditor, und speichern Sie diese als **FilterColumnVBS.asp**.  
  
```  
<!-- BeginFilterColumnVBS -->  
<HTML>  
<HEAD>  
<META name="VI60_DefaultClientScript" Content="VBScript">  
  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<TITLE>FilterColumn, FilterCriterion, FilterValue, SortColumn, and SortDirection   
Properties and Reset Method Example (VBScript)</TITLE>  
</HEAD>  
<BODY>  
<h1>FilterColumn, FilterCriterion, FilterValue, SortColumn, and SortDirection   
Properties and Reset Method Example (VBScript)</h1>  
  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDS HEIGHT=1 WIDTH=1>  
   <PARAM NAME="SQL" VALUE="Select FirstName, LastName, Title, ReportsTo, Extension from Employees">  
   <PARAM NAME="SERVER" VALUE="<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=SQLOLEDB;Initial Catalog=Northwind;Integrated Security=SSPI">  
</OBJECT>  
  
Sort Column: <SELECT NAME="cboSortColumn">   
              <OPTION VALUE=""></OPTION>  
                  <OPTION VALUE=ID>ID</OPTION>  
                  <OPTION VALUE=FirstName>FirstName</OPTION>  
                  <OPTION VALUE=LastName>LastName</OPTION>  
                  <OPTION VALUE=Title>Title</OPTION>  
                  <OPTION VALUE=Title>ReportsTo</OPTION>  
                  <OPTION VALUE=Phone>Extension</OPTION>  
             </SELECT>  
             <br>  
Sort Direction: <SELECT NAME="cboSortDir">   
              <OPTION VALUE=""></OPTION>  
                  <OPTION VALUE=TRUE>Ascending</OPTION>  
                  <OPTION VALUE=FALSE>Descending</OPTION>  
                </SELECT>  
<HR WIDTH="25%">  
Filter Column: <SELECT NAME="cboFilterColumn">   
              <OPTION VALUE=""></OPTION>  
                  <OPTION VALUE=FirstName>FirstName</OPTION>  
                  <OPTION VALUE=LastName>LastName</OPTION>  
                  <OPTION VALUE=Title>Title</OPTION>  
                  <OPTION VALUE=Room>ReportsTo</OPTION>  
                  <OPTION VALUE=Phone>Extension</OPTION>  
             </SELECT>  
             <br>  
Filter Criterion: <SELECT NAME="cboCriterion">   
                    <OPTION VALUE=""></OPTION>  
                    <OPTION VALUE="=">=</OPTION>  
                    <OPTION VALUE=">">></OPTION>  
                    <OPTION VALUE="<"><</OPTION>  
                    <OPTION VALUE=">=">>=</OPTION>  
                    <OPTION VALUE="<="><=</OPTION>  
                    <OPTION VALUE="<>"><></OPTION>  
                  </SELECT>   
              <br>  
Filter Value: <INPUT NAME="txtFilterValue">  
<HR WIDTH="25%">  
<INPUT TYPE=BUTTON NAME=Clear VALUE="CLEAR ALL">    
<INPUT TYPE=BUTTON NAME=SortFilter VALUE="APPLY">  
  
<HR>  
<TABLE DATASRC=#RDS ID="DataTable">  
<THEAD>  
  <TR>  
    <TH>FirstName</TH>  
    <TH>LastName</TH>  
    <TH>Title</TH>  
    <TH>Reports To</TH>  
    <TH>Extension</TH>  
  </TR>  
</THEAD>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
    <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
    <TD><SPAN DATAFLD="Title"></SPAN></TD>  
    <TD><SPAN DATAFLD="ReportsTo"></SPAN></TD>  
    <TD><SPAN DATAFLD="Extension"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
  
<Script Language="VBScript">  
<!--  
Const adFilterNone = 0  
  
Sub SortFilter_OnClick  
   Dim vCriterion  
   Dim vSortDir  
   Dim vSortCol  
   Dim vFilterCol  
  
   ' The value of SortColumn will be the   
   ' value of what the user picks in the  
   ' cboSortColumn box.  
   vSortCol = cboSortColumn.options(cboSortColumn.selectedIndex).value  
  
   If(vSortCol <> "") then  
      RDS.SortColumn = vSortCol  
   End If  
  
   ' The value of SortDirection will be the   
   ' value of what the user specifies in the  
   ' cboSortdirection box.  
  
   If (vSortCol <> "") then  
      vSortDir = cboSortDir.options(cboSortDir.selectedIndex).value  
      If (vSortDir = "") then  
         MsgBox "You must select a direction for the sort."  
         Exit Sub  
      Else  
         If vSortDir = "Ascending" Then vSortDir = "TRUE"  
         If vSortDir = "Descending" Then vSortDir = "FALSE"  
         RDS.SortDirection = vSortDir  
      End If  
   End If  
  
   ' The value of FilterColumn will be the   
   ' value of what the user specifies in the  
   ' cboFilterColumn box.  
   vFilterCol = cboFilterColumn.options(cboFilterColumn.selectedIndex).value  
  
   If(vFilterCol <> "") then  
      RDS.FilterColumn = vFilterCol  
   End If  
  
   ' The value of FilterCriterion will be the   
   ' text value of what the user specifies in the  
   ' cboCriterion box.  
   vCriterion = cboCriterion.options(cboCriterion.selectedIndex).value  
   If (vCriterion <> "") Then  
      RDS.FilterCriterion = vCriterion  
   End If  
  
   ' txtFilterValue is a rich text box  
   ' control. The value of FilterValue will be the   
   ' text value of what the user specifies in the  
   ' txtFilterValue box.  
   If (txtFilterValue.value <> "") Then  
      RDS.FilterValue = txtFilterValue.value  
   End If  
  
   ' Execute the sort and filter on a client-side  
   ' Recordset based on the specified sort and filter  
   ' properties. Calling Reset refreshes the result set  
   ' that is displayed in the data-bound controls to  
   ' display the filtered, sorted recordset.  
   RDS.Reset  
End Sub  
  
Sub Clear_onClick()  
   'clear the HTML input controls  
   cboSortColumn.selectedIndex = 0  
   cboSortDir.selectedIndex = 0  
   cboFilterColumn.selectedIndex = 0  
   cboCriterion.selectedIndex = 0  
   txtFilterValue.value = ""  
  
   'clear the filter  
   RDS.FilterCriterion = ""  
   RDS.Reset(FALSE)  
End Sub  
-->  
</Script>  
  
</BODY>  
</HTML>  
<!-- EndFilterColumnVBS -->  
```  
  
## <a name="see-also"></a>Siehe auch  
 [RDS (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [FilterColumn-Eigenschaft (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [FilterCriterion-Eigenschaft (RDS)](../../../ado/reference/rds-api/filtercriterion-property-rds.md)   
 [FilterValue-Eigenschaft (RDS)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [Reset-Methode (RDS)](../../../ado/reference/rds-api/reset-method-rds.md)   
 [SortColumn-Eigenschaft (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection-Eigenschaft (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


