---
title: "Gro&#223;e XML-Schemaauflistungen und Bedingungen des Typs Nicht gen&#252;gend Arbeitsspeicher | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Bedingungen des Typs Nicht genügend Arbeitsspeicher"
  - "XML-Schemaauflistungen [SQL Server], groß"
ms.assetid: 29b9d839-aaaf-48fb-be17-840c751f36f1
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# Gro&#223;e XML-Schemaauflistungen und Bedingungen des Typs Nicht gen&#252;gend Arbeitsspeicher
  Während eines Aufrufs der integrierten XML_SCHEMA_NAMESPACE()-Funktion für eine große XML-Schemaauflistung oder beim Löschen großer XML-Schemaauflistungen kann eine Bedingung des Typs "Nicht genügend Arbeitsspeicher" auftreten. Mit den folgenden Lösungen kann dieses Problem behoben werden:  
  
-   Wenn die Systemlast hoch ist, verwenden Sie den DROP_XML_SCHEMA_COLLECTION-Befehl. Schlägt dies fehl, schalten Sie die Datenbank mithilfe der ALTER DATABASE-Anweisung in den Einzelbenutzermodus um und versuchen dann nochmals, DROP XML SCHEMA COLLECTION auszuführen. Wenn die XML-Schemaauflistung in **master**-, **model**- oder **tempdb**-Datenbanken vorhanden ist, ist ein Neustart des Servers für den Einzelbenutzermodus erforderlich.  
  
-   Wenn Sie XML_SCHEMA_NAMESPACE aufrufen, können Sie versuchen, einen einzelnen XML-Schemanamespace abzurufen. Sie können den Aufruf auch zu einem Zeitpunkt durchführen, wenn die Systemlast geringer ist, oder den Aufruf im Einzelbenutzermodus versuchen.  
  
## Siehe auch  
 [Anforderungen und Einschränkungen für XML-Schemaauflistungen auf dem Server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  