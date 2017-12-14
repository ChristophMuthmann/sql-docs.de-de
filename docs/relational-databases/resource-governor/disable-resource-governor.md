---
title: Deaktivieren der Ressourcenkontrolle | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: resource-governor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Resource Governor, disabling
ms.assetid: 2c2d2db0-34a5-4f50-b783-17693e3ce3f1
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 69ff08716168f02736aa5a4ce8eb340fba637bc0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="disable-resource-governor"></a>Deaktivieren der Ressourcenkontrolle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Sie können den Resource Governor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder mit Transact-SQL deaktivieren.  
  
-   **Vorbereitungen:**  [Einschränkungen](#LimitationsRestrictions), [Berechtigungen](#Permissions)  
  
-   **So deaktivieren Sie Resource Governor:**  [Objekt-Explorer](#RGOffObjEx), [Eigenschaften von Resource Governor](#RGOffProp), [Transact-SQL](#RGOffTSQL)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
 Wenn Sie die Ressourcenkontrolle deaktivieren, geschieht Folgendes:  
  
-   Die Klassifizierungsfunktion wird nicht ausgeführt.  
  
-   Alle neuen Verbindungen werden automatisch der Standardarbeitsauslastungsgruppe zugewiesen.  
  
-   Vom System initiierte Anforderungen werden der internen Arbeitsauslastungsgruppe zugewiesen.  
  
-   Alle Einstellungen für bestehende Arbeitsauslastungsgruppen und Ressourcenpools werden auf die Standardwerte zurückgesetzt. In diesem Fall werden keine Ereignisse ausgelöst, wenn Grenzwerte erreicht werden.  
  
-   Die reguläre Systemüberwachung bleibt unbeeinflusst.  
  
-   Sie können die Konfiguration ändern, die Änderungen treten jedoch erst in Kraft, wenn die Ressourcenkontrolle wieder aktiviert wird.  
  
-   Beim Neustart von SQL Server lädt die Ressourcenkontrolle nicht ihre Konfiguration, sondern enthält lediglich die Standardarbeitsauslastungsgruppen und -pools sowie die internen Gruppen und Ressourcenpools.  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
 Mithilfe der **ALTER RESOURCE GOVERNOR** -Anweisung können Sie die Ressourcenkontrolle während einer Benutzertransaktion nicht deaktivieren.  
  
###  <a name="Permissions"></a> Berechtigungen  
 Zum Deaktivieren der Ressourcenkontrolle ist die CONTROL SERVER-Berechtigung erforderlich.  
  
##  <a name="RGOffObjEx"></a> Deaktivieren der Ressourcenkontrolle im Objekt-Explorer  
 **So deaktivieren Sie die Ressourcenkontrolle im Objekt-Explorer**  
  
1.  Öffnen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]den Objekt-Explorer, und erweitern Sie den Knoten **Verwaltung** rekursiv, bis **Ressourcenkontrolle**angezeigt wird.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Resource Governor**, und klicken Sie dann auf **Deaktivieren**.  
  
##  <a name="RGOffProp"></a> Deaktivieren der Ressourcenkontrolle über die Eigenschaften der Ressourcenkontrolle  
 **So deaktivieren Sie die Ressourcenkontrolle auf der Eigenschaftenseite der Ressourcenkontrolle**  
  
1.  Öffnen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]den Objekt-Explorer, und erweitern Sie den Knoten **Verwaltung** rekursiv, bis **Ressourcenkontrolle**angezeigt wird.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Resource Governor** , und klicken Sie dann auf **Eigenschaften**. Damit öffnen Sie die Seite **Eigenschaften der Resource Governor** .  
  
3.  Aktivieren Sie das Kontrollkästchen **Ressourcenkontrolle aktivieren** , stellen Sie sicher, dass Kontrollkästchen nicht aktiviert ist, und klicken Sie dann auf **OK**.  
  
##  <a name="RGOffTSQL"></a> Deaktivieren der Ressourcenkontrolle mit Transact-SQL  
 **So deaktivieren Sie die Ressourcenkontrolle mit Transact-SQL**  
  
1.  Führen Sie die Anweisung **ALTER RESOURCE GOVERNOR DISABLE** aus.  
  
### <a name="example-transact-sql"></a>Beispiel (Transact-SQL)  
 Im folgenden Beispiel wird die Ressourcenkontrolle aktiviert.  
  
```  
ALTER RESOURCE GOVERNOR DISABLE;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Aktivieren der Ressourcenkontrolle](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Arbeitsauslastungsgruppe der Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Klassifizierungsfunktion der Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
