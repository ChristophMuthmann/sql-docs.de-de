---
title: Große XML-Schemaauflistungen und Bedingungen des Typs „Nicht genügend Arbeitsspeicher“ | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- out-of-memory conditions
- XML schema collections [SQL Server], large
ms.assetid: 29b9d839-aaaf-48fb-be17-840c751f36f1
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 555806bca983bf53461da0439a840e1103d42078
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="large-xml-schema-collections-and-out-of-memory-conditions"></a>Große XML-Schemaauflistungen und Bedingungen des Typs Nicht genügend Arbeitsspeicher
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Während eines Aufrufs der integrierten XML_SCHEMA_NAMESPACE()-Funktion für eine große XML-Schemaauflistung oder beim Löschen großer XML-Schemaauflistungen kann eine Bedingung des Typs "Nicht genügend Arbeitsspeicher" auftreten. Mit den folgenden Lösungen kann dieses Problem behoben werden:  
  
-   Wenn die Systemlast hoch ist, verwenden Sie den DROP_XML_SCHEMA_COLLECTION-Befehl. Schlägt dies fehl, schalten Sie die Datenbank mithilfe der ALTER DATABASE-Anweisung in den Einzelbenutzermodus um und versuchen dann nochmals, DROP XML SCHEMA COLLECTION auszuführen. Wenn die XML-Schemaauflistung in **master**-, **model**- oder **tempdb**-Datenbanken vorhanden ist, ist ein Neustart des Servers für den Einzelbenutzermodus erforderlich.  
  
-   Wenn Sie XML_SCHEMA_NAMESPACE aufrufen, können Sie versuchen, einen einzelnen XML-Schemanamespace abzurufen. Sie können den Aufruf auch zu einem Zeitpunkt durchführen, wenn die Systemlast geringer ist, oder den Aufruf im Einzelbenutzermodus versuchen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anforderungen und Einschränkungen für XML-Schemaauflistungen auf dem Server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
