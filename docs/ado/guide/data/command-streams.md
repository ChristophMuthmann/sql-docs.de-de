---
title: Befehl Streams | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- command streams [ADO]
- streams [ADO], command
ms.assetid: 0ac09dbe-2665-411e-8fbb-d1efe6c777be
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 46ef9db34ecfc7ee0ba3fbd41a052658a065a010
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="command-streams"></a>Befehl Streams
ADO unterstützt immer Eingabe des Befehls im Zeichenfolgenformat angegeben werden, indem Sie die **CommandText** Eigenschaft. Als Alternative können mit ADO 2.7 oder höher, Sie können auch einen Datenstrom von Informationen für die Eingabe des Befehls durch Zuweisen des Streams, der **CommandStream** Eigenschaft. Sie können eine ADO zuweisen **Stream** Objekt oder ein beliebiges Objekt aus, die COM unterstützt **IStream** Schnittstelle.  
  
 Der Inhalt des Streams, der Befehl wird einfach aus ADO an Ihren Anbieter übergeben, damit Ihren Anbieter unterstützen die Eingabe des Befehls vom Datenstrom für diese Funktion ordnungsgemäß arbeitet. SQL Server unterstützt z. B. Abfragen in Form von XML-Vorlagen oder OpenXML-Erweiterungen in Transact-SQL an.  
  
 Da vom Anbieter die Details des Datenstroms interpretiert werden müssen, müssen Sie der Befehlsdialekt angeben, durch Festlegen der **Dialekt** Eigenschaft. Der Wert der **Dialekt** ist eine Zeichenfolge mit einer GUID, die von Ihrem Anbieter definiert ist. Informationen zu gültigen Werten für **Dialekt** von Ihrem Anbieter unterstützt, finden Sie in der Dokumentation Ihres Anbieters.  
  
## <a name="xml-template-query-example"></a>XML-Vorlage Abfragebeispiel  
 Im folgende Beispiel wird in VBScript in der Northwind-Datenbank geschrieben.  
  
 Zunächst initialisiert werden, und öffnen Sie die **Stream** -Objekt, das verwendet wird, um den Abfrage-Datenstrom enthält:  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 Der Inhalt des Streams, der Abfrage wird eine XML-Vorlage Abfrage sein.  
  
 Die Vorlage Abfrage erfordert einen Verweis auf den XML-Namespace identifiziert, die vom Sql: Präfix der \<Beispielvorlage > Tag. Eine SQL SELECT-Anweisung wird als Inhalt der XML-Vorlage enthalten und an eine Zeichenfolgenvariable wie folgt zugewiesen:  
  
```  
sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME </sql:query>  
</ROOT>"  
```  
  
 Als Nächstes schreiben Sie die Zeichenfolge in den Stream:  
  
```  
adoStreamQuery.WriteText sQuery, adWriteChar  
adoStreamQuery.Position = 0  
```  
  
 AdoStreamQuery zum Zuweisen der **CommandStream** -Eigenschaft eines ADO **Befehl** Objekt:  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 Geben Sie den Befehlssprache **Dialekt**, die angibt, wie die SQL Server-OLE DB-Anbieter den befehlsdatenstrom interpretiert werden soll. Der Dialekt, der von einer anbieterspezifischen-GUID angegeben wird:  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 Abschließend führen Sie die Abfrage und Zurückgeben der Ergebnisse in einem **Recordset** Objekt:  
  
```  
Set objRS = adoCmd.Execute  
```
