---
title: Aktivieren der Ressourcenkontrolle | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Resource Governor, enabling
ms.assetid: 4d17af53-cf11-4ce4-aab4-deda94a49836
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d4bcec1331a7878bf261aea8923fa8f8e66e7299
ms.lasthandoff: 04/11/2017

---
# <a name="enable-resource-governor"></a>Aktivieren der Ressourcenkontrolle
  Die Ressourcenkontrolle ist standardmäßig deaktiviert. Sie können die Ressourcenkontrolle in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder mit Transact-SQL aktivieren.  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **To enable Resource Governorn, using:**  [Object Explorer](#RGOnObjEx), [Resource Governor Properties](#RGOnProp), [Transact-SQL](#RGOnTSQL)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
 Wenn Sie die Ressourcenkontrolle aktivieren, geschieht Folgendes:  
  
-   Die Klassifizierungsfunktion wird für neue Verbindungen ausgeführt, damit deren Arbeitsauslastungen Arbeitsauslastungsgruppen zugeordnet werden können.  
  
-   Die in der Konfiguration der Ressourcenkontrolle angegebenen Ressourcengrenzwerte werden überprüft und durchgesetzt.  
  
-   Alle Konfigurationsänderungen, die bei deaktivierter Ressourcenkontrolle vorgenommen wurden, wirken sich auf Anforderungen aus, die bereits bestanden, bevor die Ressourcenkontrolle aktiviert wurde.  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
 Mithilfe der **ALTER RESOURCE GOVERNOR** -Anweisung können Sie die Ressourcenkontrolle während einer Benutzertransaktion nicht aktivieren.  
  
###  <a name="Permissions"></a> Berechtigungen  
 Zum Aktivieren der Ressourcenkontrolle ist die CONTROL SERVER-Berechtigung erforderlich.  
  
##  <a name="RGOnObjEx"></a> Aktivieren der Ressourcenkontrolle im Objekt-Explorer  
 **So aktivieren Sie die Ressourcenkontrolle im Objekt-Explorer**  
  
1.  Öffnen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]den Objekt-Explorer, und erweitern Sie den Knoten **Verwaltung** rekursiv, bis **Ressourcenkontrolle**angezeigt wird.  
  
2.  Klicken Sie mit der rechten Maustaste auf den **Resource Governor**, und klicken Sie anschließend auf **Aktivieren**.  
  
##  <a name="RGOnProp"></a> Aktivieren der Ressourcenkontrolle über die Eigenschaften der Ressourcenkontrolle  
 **So aktivieren Sie die Ressourcenkontrolle auf der Eigenschaftenseite der Ressourcenkontrolle**  
  
1.  Öffnen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]den Objekt-Explorer, und erweitern Sie den Knoten **Verwaltung** rekursiv, bis **Ressourcenkontrolle**angezeigt wird.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Resource Governor** , und klicken Sie dann auf **Eigenschaften**. Damit öffnen Sie die Seite **Eigenschaften der Resource Governor** .  
  
3.  Aktivieren Sie das Kontrollkästchen **Ressourcenkontrolle aktivieren** , und klicken Sie dann auf **OK**.  
  
##  <a name="RGOnTSQL"></a> Aktivieren der Ressourcenkontrolle mit Transact-SQL  
 **So aktivieren Sie die Ressourcenkontrolle mit Transact-SQL**  
  
1.  Führen Sie die **ALTER RESOURCE GOVERNOR RECONFIGURE** -Anweisung aus.  
  
### <a name="example-transact-sql"></a>Beispiel (Transact-SQL)  
 Im folgenden Beispiel wird die Ressourcenkontrolle aktiviert.  
  
```  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)   
 [Deaktivieren der Ressourcenkontrolle](../../relational-databases/resource-governor/disable-resource-governor.md)   
 [Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Arbeitsauslastungsgruppe der Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Klassifizierungsfunktion der Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
