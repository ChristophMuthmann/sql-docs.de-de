---
title: Erstellen einer Arbeitsauslastungsgruppe | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: resource-governor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Resource Governor, workload group create
- workload groups [SQL Server], create
ms.assetid: 072868ec-ceff-4db6-941b-281af731a067
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 957dee75abdbe09455972bc28fc89a40af892a0f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-workload-group"></a>Erstellen einer Arbeitsauslastungsgruppe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Sie können Arbeitsauslastungsgruppen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder mit [!INCLUDE[tsql](../../includes/tsql-md.md)]erstellen.  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **Zum Erstellen einer Arbeitsauslastungsgruppe mit:**  [SQL Server Management Studio](#CreRPProp), [Transact-SQL](#CreRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 Der durch die Indexerstellung für eine nicht ausgerichtete partitionierte Tabelle belegte Arbeitsspeicher ist proportional zur Anzahl der beteiligten Partitionen. Wenn der insgesamt erforderliche Arbeitsspeicher die Grenze übersteigt, die pro Abfrage von der Arbeitsauslastungsgruppe festgelegt wurde (REQUEST_MAX_MEMORY_GRANT_PERCENT), kann bei dieser Indexerstellung ein Fehler auftreten. Da die Standardarbeitsauslastungsgruppe Abfragen zulässt, die die pro Abfrage festgelegte Grenze mit dem mindestens für eine Kompatibilität mit SQL Server 2005 erforderlichen Arbeitsspeicher übersteigen, können Benutzer dieselbe Indexerstellung in der Standardarbeitsauslastungsgruppe ausführen. Voraussetzung ist, dass der Standardressourcenpool über ausreichend Gesamtarbeitsspeicher verfügt, um eine solche Abfrage ausführen zu können.  
  
 Bei der Indexerstellung darf mehr Arbeitsbereichsspeicher verwendet werden, als ursprünglich zugewiesen, um eine bessere Leistung zu erzielen. Die Ressourcenkontrolle unterstützt diese besondere Behandlung, die ursprüngliche und alle weiteren Speicherzuweisungen werden jedoch durch die Einstellungen für Arbeitsauslastungsgruppe und Ressourcenpool begrenzt.  
  
###  <a name="Permissions"></a> Berechtigungen  
 Zum Erstellen einer Arbeitsauslastungsgruppe ist die CONTROL SERVER-Berechtigung erforderlich.  
  
##  <a name="CreRPProp"></a> Erstellen einer Arbeitsauslastungsgruppe in SQL Server Management Studio  
 **So erstellen Sie Arbeitsauslastungsgruppen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  Erweitern Sie im Objekt-Explorer rekursiv den Knoten **Verwaltung** , bis einschließlich zum Ressourcenpool mit der zu ändernden Arbeitsauslastungsgruppe.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Arbeitsauslastungsgruppen** , und klicken Sie dann auf **Neue Arbeitsauslastungsgruppe**.  
  
3.  Stellen Sie im Raster **Ressourcenpools** sicher, dass der Ressourcenpool, dem Sie die Arbeitsauslastungsgruppe hinzufügen möchten, markiert ist.  
  
4.  Das Raster **Arbeitsauslastungsgruppen für Ressourcenpool** weist eine neue Zeile mit einem leeren Namen und Standardwerten in den anderen Spalten auf.  
  
5.  Klicken Sie auf die Zelle **Name** , und geben Sie einen Namen für die Arbeitsauslastungsgruppe ein.  
  
6.  Klicken oder doppelklicken Sie auf beliebige andere Zellen in der Zeile, deren Standardeinstellungen Sie aufheben möchten, und geben Sie jeweils die neuen Werte ein.  
  
7.  Klicken Sie auf **OK**, um die Änderungen zu speichern.  
  
##  <a name="CreRPTSQL"></a> Erstellen einer Arbeitsauslastungsgruppe mit Transact-SQL  
 **So erstellen Sie Arbeitsauslastungsgruppen in [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  Führen Sie die CREATE WORKLOAD GROUP-Anweisung aus, und geben Sie dabei die festzulegenden Eigenschaftswerte an.  
  
2.  Führen Sie die ALTER RESOURCE GOVERNOR RECONFIGURE-Anweisung aus.  
  
### <a name="example-transact-sql"></a>Beispiel (Transact-SQL)  
 Im folgenden Beispiel wird im Ressourcenpool `groupAdhoc` die Arbeitsauslastungsgruppe `poolAdhoc`erstellt.  
  
```  
CREATE WORKLOAD GROUP groupAdhoc  
USING poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Aktivieren der Ressourcenkontrolle](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Erstellen eines Ressourcenpools](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Ändern der Einstellungen von Arbeitsauslastungsgruppen](../../relational-databases/resource-governor/change-workload-group-settings.md)   
 [Erstellen und Testen einer benutzerdefinierten Klassifizierungsfunktion](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)  
  
  
