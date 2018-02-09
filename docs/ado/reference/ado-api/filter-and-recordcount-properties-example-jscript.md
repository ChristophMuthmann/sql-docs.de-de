---
title: Filter- und RecordCount Eigenschaften Beispiel (JScript) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
- RecordCount property [ADO], JScript example
- Filter property [ADO], JScript example
ms.assetid: 677fa67e-9cb9-4d7d-a786-beeb5bee5236
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5347f486c516a131f9dc2103ecd5a037a916f8eb
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="filter-and-recordcount-properties-example-jscript"></a>Filter- und RecordCount Eigenschaften Beispiel (JScript)
In diesem Beispiel öffnet ein **Recordset** für die Firmen-Tabelle der Northwind-Datenbank und anschließend verwendet der [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft, um die sichtbaren Datensätze einzuschränken, die an das CompanyName-Feld mit dem Buchstaben beginnt D. Ausschneiden und fügen Sie den folgenden Code in Editor oder einem anderen Texteditor und speichern Sie diese als **Northwind**.  
  
```  
<!-- BeginFilterJS -->  
<%@  Language=JavaScript %>  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<html>  
  
<head>  
<title>ADO Recordset.Filter Example</title>  
<style>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
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
  
<h1>ADO Recordset.Filter Example</h1>  
<!-- Page text goes here -->  
<%  
    // connection and recordset variables  
    var Cnxn = Server.CreateObject("ADODB.Connection")  
    var strCnxn = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='Northwind';Integrated Security='SSPI';";  
    var rsCustomers = Server.CreateObject("ADODB.Recordset");  
    var SQLCustomers = "select * from Customers;";  
    // record variables  
    var fld, filter  
    var showBlank = " ";  
    var showNull = "-NULL-";  
  
    try  
    {  
        //open connection   
        Cnxn.Open(strCnxn);  
  
        // create recordset client-side using object refs  
        rsCustomers.ActiveConnection = Cnxn;  
        rsCustomers.CursorLocation = adUseClient;  
        rsCustomers.CursorType = adOpenKeyset;  
        rsCustomers.LockType = adLockOptimistic;  
        rsCustomers.Source = SQLCustomers;  
        rsCustomers.Open();  
  
        rsCustomers.MoveFirst();  
  
        //set filter  
        filter = "CompanyName LIKE 'b*'";  
        rsCustomers.Filter = filter  
  
        if (rsCustomers.RecordCount == 0) {  
            Response.Write("No records matched ");  
            Response.Write (SQLCustomers + "So cannot make table...");  
            Cnxn.Close();  
            Response.End  
        }  
        else {  
        // show the data  
            Response.Write('<table width="100%" border="2">');      
            while(!rsCustomers.EOF) {  
                Response.Write('<tr class="tbody">');  
                for (var thisField = 0; thisField < rsCustomers.Fields.Count; thisField++) {  
                    fld = rsCustomers(thisField);  
                    fldValue = fld.Value;  
                    if (fldValue == null)  
                        fldValue = showNull;  
                    if (fldValue == "")  
                        thisField=showBlank;  
                    Response.Write("<td>" + fldValue + "</td>")  
                }  
                rsCustomers.MoveNext();  
                Response.Write("</tr>");  
            }  
            // close the table  
            Response.Write("</table>");  
        }  
    }      
    catch (e)  
    {  
        Response.Write(e.message);  
    }  
    finally  
    {  
        // clean up  
        if (rsCustomers.State == adStateOpen)  
            rsCustomers.Close;  
        if (Cnxn.State == adStateOpen)  
            Cnxn.Close;  
        rsCustomers = null;  
        Cnxn = null;  
    }  
%>  
  
</body>  
  
</html>  
<!-- EndFilterJS -->  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Filter-Eigenschaft](../../../ado/reference/ado-api/filter-property.md)   
 [RecordCount-Eigenschaft (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
