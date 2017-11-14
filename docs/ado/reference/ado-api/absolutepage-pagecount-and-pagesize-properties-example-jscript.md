---
title: AbsolutePage "PageCount" und PageSize Eigenschaften Beispiel (JScript) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- JScript
helpviewer_keywords:
- PageCount property [ADO], JScript example
- AbsolutePage property [ADO], JScript example
- PageSize property [ADO], JScript example
ms.assetid: 2db6dd3f-5a9c-438c-ae62-d09242906c98
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a17b453028c97f8155a7ddf9897cc668d8571ece
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="absolutepage-pagecount-and-pagesize-properties-example-jscript"></a>AbsolutePage "PageCount" und PageSize Eigenschaften Beispiel (JScript)
Dieses Beispiel zeigt die Eigenschaften AbsolutePage-, "PageCount" und PageSize. Ausschneiden und fügen Sie den folgenden Code in Editor oder einem anderen Texteditor und speichern Sie diese als **AbsolutePageJS.asp**.  
  
```  
<!-- BeginAbsolutePageJS -->  
<%@LANGUAGE="JScript" %>  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<html>  
  
<head>  
<title>AbsolutePage, PageSize, and PageSize Properties (JScript)</title>  
<style>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</style>  
</head>  
  
<body bgcolor="White">  
<h1>AbsolutePage, PageSize, and PageSize Properties (JScript)</h1>  
<%  
    // connection and recordset variables  
    var Cnxn = Server.CreateObject("ADODB.Connection")  
    var strCnxn = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='Northwind';Integrated Security='SSPI';";  
    var rsEmployee = Server.CreateObject("ADODB.Recordset");  
    // display variables  
    var strMessage, iRecord, iPageCount;  
  
    try  
    {  
        // open connection  
        Cnxn.Open(strCnxn);  
  
        // Open a recordset on the Employee table using  
        // a client-side cursor to enable AbsolutePage property.  
        rsEmployee.CursorLocation = adUseClient;  
        rsEmployee.Open("employees", strCnxn, adOpenStatic, adLockOptimistic, adCmdTable);  
  
        // Set PageSize to five to display names and hire dates of five employees at a time  
        rsEmployee.PageSize = 5;   
        iPageCount = rsEmployee.PageCount;  
  
        // Write header information to the document  
        Response.Write('<p align="center">There are ' + iPageCount);  
        Response.Write(" pages, each containing ");  
        Response.Write(rsEmployee.PageSize + " or fewer records.</p>");  
        Response.Write('<table border="0" align="center">');  
        Response.Write('<tr class="thead2">');  
        Response.Write("<th>Page</th><th>Name</th><th>Hire Date</th></tr>");  
  
        for (var i=1; i<=iPageCount; i++)  
        {  
            rsEmployee.AbsolutePage = i;  
  
            for (iRecord = 1; iRecord <= rsEmployee.PageSize; iRecord++)  
            {  
                strMessage = "";  
  
                    // Start a new table row.  
                    strMessage = '<tr class="tbody">';  
  
                    // First column in row contains page number on  
                    // first record of each page. Otherwise, the column  
                    // contains a non-breaking space.  
                    if (iRecord == 1)  
                        strMessage += "<td>Page " + i + " of " + rsEmployee.PageCount + "</td>"  
                    else  
                        strMessage += "<td> </td>";  
  
                    // First and last name are in first column.  
                    strMessage += "<TD>" + rsEmployee.Fields("FirstName") + " ";  
                    strMessage += rsEmployee.Fields("LastName") + " " + "</td>";  
  
                    // Hire date in second column.  
                    strMessage += "<td>" + rsEmployee.Fields("HireDate") + "</td>";  
  
                    // End the row.  
                    strMessage += "</tr>";  
  
                    // Write line to document.  
                    Response.Write(strMessage);  
  
                    // Get next record.  
                    rsEmployee.MoveNext;  
  
                    if (rsEmployee.EOF)  
                        break;  
            }  
        }  
  
        // Finish writing table.  
        Response.Write("</table>");  
    }  
    catch (e)  
    {  
        Response.Write(e.message);  
    }  
    finally  
    {  
        // 'clean up  
        if (rsEmployee.State == adStateOpen)  
            rsEmployee.Close;  
        if (Cnxn.State == adStateOpen)  
            Cnxn.Close;  
        rsEmployee = null;  
        Cnxn = null;  
    }  
%>  
  
</body>  
  
</html>  
<!-- EndAbsolutePageJS -->  
```  
  
## <a name="see-also"></a>Siehe auch  
 [AbsolutePage-Eigenschaft (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 ["PageCount"-Eigenschaft (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [Die Eigenschaft PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

