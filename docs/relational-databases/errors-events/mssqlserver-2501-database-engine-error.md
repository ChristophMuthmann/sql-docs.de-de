---
title: MSSQLSERVER_2501 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2501 (Database Engine error)
ms.assetid: 895aafe3-a4e7-4ed8-acc5-93be76ef3664
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 56cd2c3d92ce8697664801feba4a0c262f3fa6c2
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver2501"></a>MSSQLSERVER_2501
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|2501|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBCC_NO_SUCH_TABLE_NAME|  
|Meldungstext|Eine Tabelle oder ein Objekt mit dem Namen 'NAME' wurde nicht gefunden. Überprüfen Sie den Systemkatalog.|  
  
## <a name="explanation"></a>Erklärung  
Das angegebene Objekt wurde nicht gefunden.  
  
### <a name="possible-causes"></a>Mögliche Ursachen  
Dieser Fehler kann durch eines der folgenden Probleme verursacht werden:  
  
-   Das Objekt ist nicht richtig angegeben.  
  
-   Das Objekt ist nicht vorhanden, oder das Objekt wurde entfernt, bevor von einer Anweisung versucht wurde, es zu verwenden.  
  
-   Das Objekt ist möglicherweise vorhanden, es konnte jedoch nicht für den Benutzer verfügbar gemacht werden. Beispielsweise besitzt der Benutzer möglicherweise keine Berechtigungen für das Objekt, oder das Objekt stellt eine interne Tabelle dar, die von einem Benutzer nicht angezeigt werden konnte.  
  
## <a name="user-action"></a>Benutzeraktion  
  
-   Überprüfen Sie, ob der aktuelle Datenbankkontext richtig ist. Weitere Informationen finden Sie unter [USE &#40;Transact-SQL&#41;](~/t-sql/language-elements/use-transact-sql.md).  
  
-   Überprüfen Sie, ob der Tabellen- oder Objektname richtig geschrieben wurde.  
  
-   Überprüfen Sie den Namen des Schemas, das das Objekt enthält. Wenn das Objekt zu einem anderen Schema als dem Standardschema (**dbo**) gehört, müssen Sie den Tabellen- bzw. Objektnamen im zweiteiligen Format *schema_name.object_name* angeben.  
  
-   Stellen Sie sicher, dass das Objekt in den Systemtabellen vorhanden ist. Wenn Sie überprüfen möchten, ob eine Tabelle oder ein anderes schemabezogenes Objekt vorhanden ist, fragen Sie die [sys.objects](~/relational-databases/system-catalog-views/sys-objects-transact-sql.md)-Katalogsicht ab. Wenn das Objekt in den Systemtabellen nicht vorhanden ist, wurde das Objekt gelöscht, oder der Benutzer besitzt keine Berechtigungen zum Anzeigen der Objektmetadaten. Weitere Informationen zu Berechtigungen zum Anzeigen von Objektmetadaten finden Sie unter [Konfiguration der Sichtbarkeit von Metadaten](~/relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
[Katalogsichten &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  

