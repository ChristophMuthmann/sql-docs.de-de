---
title: Datentypen von Oracle CDC-Instanzen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eec13d8d-c15a-4542-bfc4-da66b1a6bfe0
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c8494efb40093d0a29b98d16e05fcaf764ee0f22
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="oracle-cdc-instance-data-types"></a>Datentypen von Oracle CDC-Instanzen
  Die Oracle CDC-Instanz unterstützt die meisten Oracle-Datentypen. In den folgenden Abschnitten werden die unterstützten Datentypen und die nicht unterstützten Datentypen beschrieben.  
  
## <a name="supported-data-types"></a>Unterstützte Datentypen  
 In der folgenden Tabelle werden die Oracle-Datentypen, die aufgezeichnet werden können, sowie ihre Standardzuordnung zu SQL Server-Datentypen in den Änderungstabellen beschrieben. Beim Hinzufügen einer Aufzeichnungsinstanz für eine Oracle-Quelltabelle können Sie einige dieser Zuordnungen überschreiben.  
  
|Datentyp der Oracle-Datenbank|SQL Server-Datentyp|  
|-------------------------------|--------------------------|  
|BINARY_FLOAT|real|  
|BINARY_DOUBLE|GLEITKOMMAZAHL|  
|CHAR|NVARCHAR|  
|DATE|DATETIME|  
|GLEITKOMMAZAHL|GLEITKOMMAZAHL|  
|INT|NUMERIC (38)|  
|INTERVAL|DATETIME|  
|NCHAR|NVARCHAR|  
|NUMBER|GLEITKOMMAZAHL|  
|NAVARCHAR2|NVARCHAR|  
|RAW|VARBINARY|  
|real|GLEITKOMMAZAHL|  
|TIMESTAMP|DATETIME2|  
|TIMESTAMP WITH TIME ZONE|VARCHAR (37)|  
|TIMESTAMP WITH LOCAL TIME ZONE|VARCHAR (37)|  
|VARCHAR2|VARCHAR|  
|XMLTYPE|NVARCHAR (MAX)|  
  
## <a name="non-supported-data-types"></a>Nicht unterstützte Datentypen  
 Oracle-Quelltabellen, die Spalten mit den folgenden Oracle-Datentypen enthalten, können nicht aufgezeichnet werden. Aufgezeichnete Spalten mit diesen Datentypen werden als NULL-Werte angezeigt. Eine Änderung des Werts wird jedoch in der Änderungsmaske der aufgezeichneten Tabellen angegeben.  
  
-   LONG  
  
-   XMLTYPE  
  
-   BLOB  
  
-   CLOB  
  
 Oracle-Quelltabellen, die Spalten mit den folgenden Oracle-Datentypen enthalten, können nicht aufgezeichnet werden.  
  
-   BFILE  
  
-   ROWID  
  
-   REF  
  
-   UROWID  
  
-   Geschachtelte Tabelle  
  
 Wenn die folgenden Datentypen in einer Tabelle vorhanden sind, verhindern sie, dass der LogMinder Daten für eine beliebige Spalte der Tabelle abruft:  
  
-   Benutzerdefinierte Datentypen  
  
-   VARRAY  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Change Data Capture Designer für Oracle von Attunity](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)   
 [Oracle CDC-Instanz](../../integration-services/change-data-capture/the-oracle-cdc-instance.md)  
  
  
