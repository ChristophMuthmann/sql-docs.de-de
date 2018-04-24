---
title: Verwaltungsaufgaben für die arbeitsauslastung - Analyseplattformsystem | Microsoft Docs
description: Workload-Verwaltungsaufgaben in Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 16206cb5cefd68b19e1640592b903890808b5a31
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>Workload-Verwaltungsaufgaben im Analyseplattformsystem
Workload-Verwaltungsaufgaben in Analytics Platform System.

## <a name="view-login-members-of-each-resource-class"></a>Ansicht Anmeldung Mitglied jeder Ressourcenklasse
Beschreibt, wie die Anmeldung Member jeder Ressource Klasse-Serverrolle in SQL Server PDW anzeigen. Verwenden Sie diese Abfrage, um zu ermitteln, die Klasse der Ressourcen, die für jede Anmeldung übermittelten Anforderungen zulässig.  
  
Beschreibung der Klasse, finden Sie unter [Arbeitsauslastungsverwaltung](workload-management.md).  
  
Diese Abfrage zeigt die Mitgliederliste für jede Ressourcenklasse. Es gibt drei Ressourcenklassen, Mediumrc Largerc und Xlargerc.  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  ( l.[type] = 'S' OR l.[type] = 'U' OR l.[type] = 'G' )  
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
```  
  
Wenn eine Anmeldung nicht in dieser Liste enthalten ist, erhält seine Anforderungen die Standardressourcen. Wenn ein Anmeldename Mitglied von mehr als eine Ressourcenklasse ist, hat die größte Klasse Vorrang.  
  
Die Ressource Zuordnungen sind in aufgeführt [Arbeitsauslastungsverwaltung](workload-management.md).  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>Ändern Sie die Systemressourcen, die eine Anforderung zugeordnet
Beschreibt, wie Sie herausfinden, welche Ressource Klasse, die über eine SQL Server PDW-Anforderung ausgeführt wird, und klicken Sie dann so ändern Sie die Systemressourcen für diese Anforderung. Ändern die Ressourcen aus, für eine Anforderung erfordert das Ändern der Ressource Mitgliedschaft des Anmeldenamens mit übermitteln der Anforderung, die [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) Anweisung.  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>Schritt 1: Ermitteln der Ressourcenklasse für die Anmeldung, die Ausführung der Anforderung.  
Diese Abfrage zeigt die Anmeldungen, die Mitglieder der serverrollenmitgliedschaften der Resource-Klasse. Es gibt drei Ressourcenklassen, **Mediumrc**, **Largerc**, und **Xlargerc**.  
  
> [!IMPORTANT]  
> Diese Abfrage muss ausgeführt werden, indem Sie eine Anmeldung **CONTROL SERVER** Berechtigung. Wenn durch eine Anmeldung ohne ausgeführt **CONTROL SERVER** Berechtigung, diese Abfrage gibt nur zurück, die Rollenmitgliedschaften für die aktuelle Anmeldung.  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  l.[type] = 'S'   
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
GO  
```  
  
Wenn es keine Anmeldungen, die Mitglieder einer Ressource Klasse-Serverrolle sind sind, wird die daraus resultierende Tabelle leer sein. In diesem Fall, wenn die Abfrage eine Anmeldung mit dem Namen Ching zurückgibt, erhalten klicken Sie dann beim Ching eine Anforderung übermittelt die Anforderung die Standardressourcen System die kleiner als die Systemressourcen des Ressource-Klasse sind. Wenn ein Anmeldename Mitglied von mehr als eine Ressourcenklasse ist, hat die größte Klasse Vorrang.  
  
Eine Liste der Ressourcen-Zuordnungen für jede Ressourcenklasse, finden Sie unter [Arbeitsauslastungsverwaltung](workload-management.md).  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>Schritt 2: Ausführen die Anforderung unter eine Anmeldung mit verschiedenen Mitgliedschaft  
Es gibt zwei Möglichkeiten zum Ausführen einer Anforderung mit entweder größer oder kleiner Systemressourcen:  
  
-   Führen Sie die Anforderung unter einer anderen Anmeldung, die eine größere oder kleinere Ressourcenklasse angehört.  
  
-   Fügen Sie den erforderlichen Benutzernamen auf eine Ressource Klasse Rollen hinzu. Wählen Sie diese Option mit Vorsicht; durch das Ändern der Ressourcenklasse für die Anmeldung wird der Systemebene für die Ressource für alle Anforderungen, die von der Anmeldung übermittelt.  
  
Nehmen Sie an, dass Ching ein Mitglied der Serverrolle Largerc ist. Das folgende Beispiel zeigt, wie Anmeldenamen Ching Xlargerc-Serverrolle hinzufügen.  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching ist jetzt ein Mitglied der Largerc und Xlargerc-Serverrollen. Wenn Ching Anforderungen sendet, erhalten die Anforderungen die Xlargerc Systemressourcen.  
  
Im folgenden Beispiel wird Ching zurück, der Mediumrc-Serverrolle.  Um die neue Rolle ändern, die Anmeldung muss aus entfernt Xlargerc und Largerc-Serverrollen, und der Mediumrc-Serverrolle hinzugefügt.  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching ist jetzt ein Mitglied der Serverrolle Mediumrc.  Im folgende Beispiel ändert Ching haben Sie die System-Standardressourcen für Anforderungen.  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
Weitere Informationen zu Ressourcen Klasse Rollenmitgliedschaft zu ändern, finden Sie unter [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md).  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>Ändern Sie eine Anmeldung in der System-Standardressourcen für ihre Anforderungen
Beschreibt, wie das System Ressource Zuordnungen zugewiesen werden, um ein SQL Server PDW-Anmeldekennwort für die Standardbeträge zu ändern. 
  
Beschreibung der Klasse, finden Sie unter [Arbeitsauslastungsverwaltung](workload-management.md)  
  
Wenn eine Anmeldung nicht Mitglied einer Serverrolle des Ressource-Klasse ist, erhalten Anforderungen, die von der Anmeldung übermittelt die Standarddauer an Systemressourcen verfügbar sind.  
  
Nehmen Sie an der Anmeldung, die Matt derzeit Mitglied aller Ressourcen Klasse Serverrollen und möchte, müssen nur die Standardressourcen empfangen Anforderungen wiederherstellen.  Im folgende Beispiel Matt Anforderungen durch das Löschen von seiner Mitgliedschaft aus allen drei Resource-Klasse-Serverrollen die Standardressourcen zugewiesen.  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>Anzeigen, die die Anzahl der Slots Parallelität für einen wartenden anfordern erforderlich
Beschreibt, wie die Anzahl der Parallelität zu ermitteln, Slots von einer Anforderung, die darauf warten erforderlich sind, auf SQL Server PDW ausgeführt werden.  
  
Weitere Informationen finden Sie unter [Arbeitsauslastungsverwaltung](workload-management.md).  
  
Eine Anforderung konnte auf lange ohne die erste Ausführung warten. Eine der Methoden, um anforderungsprobleme zu behandeln ist, können Sie die Anzahl der Slots Parallelität einsehen, die die Anforderung benötigt.  Das folgende Beispiel zeigt die Anzahl der Parallelität Slots von jeder der Anforderungsstatus Waiting benötigt.  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>Siehe auch  
[Arbeitsauslastungsverwaltung](workload-management.md)  
  
