---
title: VBScript-ADO-Programmierung | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- ADO, VBScript
- VBScript [ADO]
ms.assetid: 6aaaf6d0-1376-4473-bea6-b81f2645a9ac
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bc40ecab95aa419ac81ada509133de6dd108a823
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="vbscript-ado-programming"></a>VBScript-ADO-Programmierung
## <a name="creating-an-ado-project"></a>Erstellen eines ADO-Projekts  
 Microsoft Visual Basic, Scripting Edition unterstützt keine Typbibliotheken, daher müssen Sie keine ADO in Ihrem Projekt zu verweisen. Daher werden keine zugehörigen Features wie z. B. über die Befehlszeile Abschluss unterstützt. Darüber hinaus sind ADO aufgezählt werden standardmäßig in VBScript nicht definiert.  
  
 ADO bietet jedoch, dass Sie mit zwei Includedateien, die mit den folgenden Definitionen mit VBScript verwendet werden soll:  
  
-   Verwenden, Sie für serverseitiges Skripting Adovbs.inc wird die im Ordner "c:\Programme\Microsoft Dateien\System\ADO\" standardmäßig installiert.  
  
-   Verwenden, Sie für die clientseitige Skripting Adcvbs.inc wird die standardmäßig im Ordner "c:\Program Files\Common Files\System\msdac\" installiert.  
  
 Sie können entweder kopieren und Einfügen Konstantendefinitionen aus diesen Dateien in ASP-Seiten, oder, wenn Sie serverseitige Skripts erstellen, kopieren Sie Adovbs.inc-Datei in einen Ordner auf Ihrer Website und verwiesen wird, aus der ASP-Seite wie folgt:  
  
```  
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>Erstellen von ADO-Objekten in VBScript  
 Sie können keine der **Dim** Anweisung, um einen bestimmten Typ in VBScript Objekte zugewiesen werden. VBScript unterstützt darüber hinaus nicht das **neu** mit verwendete Syntax der **Dim** -Anweisung in Visual Basic for Applications. Verwenden Sie stattdessen die **CreateObject** Funktionsaufruf:  
  
```  
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>VBScript-Beispiele  
 Der folgende Code ist ein allgemeines Beispiel VBScript serverseitige Programmierung in einer Datei (Active Server Pages):  
  
```  
<%  @LANGUAGE="VBSCRIPT" %>  
<%  Option Explicit %>  
<!--#include File="adovbs.inc"-->  
<HTML>  
    <BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
  
    <!-- Your ASP Code goes here -->  
<%  
Dim Source  
Dim Connect  
Dim Rs1  
  
Source = "SELECT * FROM Authors"  
Connect = "Provider=sqloledb;Data Source=srv;" & _  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
Rs1.Open Source, Connect, adOpenForwardOnly  
Response.Write("Success!")  
%>  
    </BODY>  
</HTML>  
```  
  
 Genauere VBScript-Beispiele sind in der ADO-Dokumentation enthalten. Weitere Informationen finden Sie unter [ADO-Codebeispiele in Microsoft Visual Basic Scripting Edition](../../../ado/reference/ado-api/ado-code-examples-vbscript.md).  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>Unterschiede zwischen VBScript und Visual Basic  
 Verwenden von ADO mit VBScript ähnelt der Verwendung von ADO mit Visual Basic in vielerlei Hinsicht, einschließlich der Verwendung der Syntax. Es gelten dabei jedoch einige deutliche Unterschiede:  
  
-   VBScript unterstützt nur den Variant-Datentyp, der verschiedene Datentypen enthalten kann. Können Sie die benötigten Daten in einen Variant-Datentyp speichern, und die Daten funktioniert ordnungsgemäß aufgrund der Umwandlung von VBScript ausgeführt. Er erkennt den ADO erforderlichen Typ und den Wert in der Variante entsprechend konvertiert.  
  
-   Sie können keine **auf Fehler Goto \<Bezeichnung >** in VBScript.  
  
-   VBScript unterstützt einige der integrierten Visual Basic-Funktionen wie z. B. **Msgbox**, **Datum**, und **IsNumeric**. Da VBScript eine Teilmenge von Visual Basic ist, werden jedoch nicht alle integrierte Funktionen unterstützt. Z. B. VBScript unterstützt nicht die **Format** Funktion und die-e/a-Dateifunktionen.

