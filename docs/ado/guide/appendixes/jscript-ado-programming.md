---
title: JScript-ADO-Programmierung | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
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
- JScript programming in ADO
- ADO, JScript programming
ms.assetid: 62273658-0fe7-4aac-b4d8-f725e6baf043
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6ae8137c2e5641594c3ddcf768c47b7fe844fafc
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="jscript-ado-programming"></a>JScript-ADO-Programmierung
## <a name="creating-an-ado-project"></a>Erstellen eines ADO-Projekts  
 Microsoft JScript unterstützt keine Typbibliotheken, damit Sie nicht in ADO-Verweis in Ihrem Projekt benötigen. Daher werden keine zugehörigen Features wie z. B. über die Befehlszeile Abschluss unterstützt. Darüber hinaus sind ADO aufgezählt wird standardmäßig in JScript nicht definiert.  
  
 ADO bietet jedoch, dass Sie mit zwei Includedateien, die mit den folgenden Definitionen mit JScript verwendet werden soll:  
  
-   Verwenden Sie für serverseitiges Skripting Adojavas.inc, die in den Ordnern der ADO-Bibliothek installiert ist.  
  
-   Verwenden Sie für die clientseitige Skripting Adcjavas.inc, die in den Ordnern der ADO-Bibliothek installiert ist.  
  
 Sie können entweder kopieren und Einfügen Konstantendefinitionen aus diesen Dateien in ASP-Seiten, oder, wenn Sie serverseitige Skripts erstellen, kopieren Sie Adojavas.inc-Datei in einen Ordner auf Ihrer Website und darauf verweist, aus der ASP-Seite wie folgt:  
  
```  
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>Erstellen von ADO-Objekten in JScript  
 Verwenden Sie stattdessen die **CreateObject** Funktionsaufruf:  
  
```  
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>JScript-Beispiel  
 Der folgende Code ist ein allgemeines Beispiel für JScript serverseitige Programmierung in eine Active Server Page (ASP)-Datei, die öffnet eine **Recordset** Objekt:  
  
```  
<%  @LANGUAGE="JScript" %>  
<!--#include File="adojavas.inc"-->  
<HTML>  
<BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
<%  
var Source = "SELECT * FROM Authors";  
var Connect =  "Provider=sqloledb;Data Source=srv;" +  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
var Rs1 = Server.CreateObject( "ADODB.Recordset.2.5" );  
Rs1.Open(Source,Connect,adOpenForwardOnly);  
Response.Write("Success!");  
%>  
</BODY>  
</HTML>  
```

