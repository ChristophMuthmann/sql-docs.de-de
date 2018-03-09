---
title: Klassifizierungsfunktion der Ressourcenkontrolle | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: resource-governor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Resource Governor, classifier function
- user-defined functions [SQL Server], classifier function
- classifier function [SQL Server]
- classifier function [SQL Server], overview
ms.assetid: 64c25012-7068-476f-afa2-0b4f3adde9a4
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd888ee38d5afb60fc6a071af2f6e072d31ff290
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="resource-governor-classifier-function"></a>Resource Governor Classifier Function
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Beim Klassifizierungsprozess von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Resource Governor werden eingehende Sitzungen auf Grundlage der Eigenschaften der Sitzung einer Arbeitsauslastungsgruppe zugewiesen. Sie können die Klassifizierungslogik anpassen, indem Sie eine benutzerdefinierte Funktion schreiben, die als Klassifizierungsfunktion bezeichnet wird.  
  
## <a name="classification"></a>Klassifizierung  
 Die Ressourcenkontrolle unterstützt die Klassifikation eingehender Sitzungen. Die Klassifikation basiert auf einer Reihe von benutzerspezifischen Kriterien, die in einer Funktion enthalten sind. Anhand der Ergebnisse der Funktionslogik kann die Ressourcenkontrolle Sitzungen in vorhandene Arbeitsauslastungsgruppen klassifizieren.  
  
> [!NOTE]  
>  Die interne Arbeitsauslastungsgruppe wird mit Anforderungen gefüllt, die nur für die interne Verwendung bestimmt sind. Die zum Weiterleiten dieser Anforderungen verwendeten Kriterien können nicht geändert werden, und es können keine Anforderungen der internen Arbeitsauslastungsgruppe zugeordnet werden.  
  
 Sie können eine Skalarfunktion schreiben, die die Logik enthält, auf deren Grundlage eingehende Sitzungen einer Arbeitsauslastungsgruppe zugewiesen werden. Bevor Sie diese Funktion verwenden können, müssen Sie folgende Aktionen ausführen:  
  
-   Erstellen und registrieren Sie die Funktion mit der ALTER RESOURCE GOVERNOR-Anweisung. Weitere Informationen finden Sie unter [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).  
  
-   Aktualisieren Sie die Konfiguration der Ressourcenkontrolle mit der ALTER RESOURCE GOVERNOR-Anweisung und dem RECONFIGURE-Parameter.  
  
 Nachdem Sie die Funktion erstellt und die Konfigurationsänderungen übernommen haben, verwendet die Klassifizierungsfunktion der Ressourcenkontrolle den von der Funktion zurückgegebenen Arbeitsauslastungsgruppennamen, um eine neue Anforderung an die entsprechende Arbeitsauslastungsgruppe zu senden.  
  
> [!IMPORTANT]  
>  Die Clientsitzung kann in einen Timeout laufen, falls die Klassifizierungsfunktion nicht innerhalb des festgelegten Timeouts für die Anmeldung abgeschlossen wird. Da der Anmeldetimeout eine Eigenschaft des Clients ist, wird dieser Timeout vom Server nicht beachtet. Eine Klassifizierungsfunktion mit langer Laufzeit kann auf dem Server zu lang andauernden verwaisten Verbindungen führen. Daher ist es wichtig, Klassifizierungsfunktionen zu erstellen, deren Ausführung vor einem Verbindungstimeout beendet ist.  
  
 Die benutzerdefinierte Funktion weist die folgenden Merkmale und Verhaltensweisen auf:  
  
-   Die benutzerdefinierte Funktion wird für jede neue Sitzung ausgewertet, auch dann, wenn Verbindungspooling aktiviert ist.  
  
-   Die benutzerdefinierte Funktion stellt einen Arbeitsauslastungsgruppenkontext für die Sitzung bereit. Nachdem die Gruppenmitgliedschaft bestimmt ist, wird die Sitzung für ihre Lebensdauer an die Arbeitsauslastungsgruppe gebunden.  
  
-   Falls die benutzerdefinierte Funktion NULL, "default" oder den Namen einer nicht vorhandenen Gruppe zurückgibt, wird die Sitzung dem Kontext für die Standardarbeitsauslastungsgruppe zugeordnet. Die Sitzung wird dem Standardkontext auch zugeordnet, falls die Funktion fehlschlägt.  
  
-   Die Funktion sollte für den Serverbereich (Masterdatenbank) definiert werden.  
  
-   Die Bestimmung der Funktion als benutzerdefinierte Klassifizierungsfunktion wird erst nach Ausführung von ALTER RESOURCE GOVERNOR RECONFIGURE wirksam.  
  
-   Es kann immer nur eine benutzerdefinierte Funktion als Klassifizierungsfunktion bestimmt werden.  
  
-   Die benutzerdefinierte Klassifizierungsfunktion kann nicht gelöscht oder geändert werden. Ihr kann lediglich der Klassifizierungsstatus entzogen werden.  
  
-   Falls keine benutzerdefinierte Klassifizierungsfunktion ausgewiesen wurde, werden alle Sitzungen der Standardgruppe zugeordnet.  
  
-   Die von der Klassifizierungsfunktion zurückgegebene Arbeitsauslastungsgruppe liegt außerhalb des Bereichs der Schemabindungseinschränkung. So können Sie z. B. keine Tabelle löschen, aber Sie können eine Arbeitsauslastungsgruppe löschen.  
  
> [!IMPORTANT]  
>  Es wird empfohlen, die dedizierte Administratorverbindung (Dedicated Administrator Connection, DAC) auf dem Server zu aktivieren. Die DAC unterliegt nicht der Klassifizierung der Ressourcenkontrolle und kann daher zum Überwachen einer Klassifizierungsfunktion und für die entsprechende Problembehandlung verwendet werden. Weitere Informationen finden Sie unter [Diagnoseverbindung für Datenbankadministratoren](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md). Wenn keine DAC für die Problembehandlung verfügbar ist, können Sie alternativ das System im Einzelbenutzermodus neu starten. Der Einzelbenutzermodus unterliegt zwar nicht der Klassifizierung, allerdings haben Sie in diesem Modus nicht die Möglichkeit, die Klassifizierung der Ressourcenkontrolle während der Ausführung zu diagnostizieren.  
  
### <a name="classification-process"></a>Klassifizierungsprozess  
 Im Kontext der Ressourcenkontrolle besteht der Anmeldevorgang für eine Sitzung aus den folgenden Schritten:  
  
1.  Anmeldeauthentifizierung  
  
2.  Ausführung von LOGON-Triggern  
  
3.  Klassifizierung  
  
 Wenn die Klassifizierung gestartet wird, führt die Ressourcenkontrolle die Klassifizierungsfunktion aus und verwendet den von der Funktion zurückgegebenen Wert, um Anforderungen an die entsprechende Arbeitsauslastungsgruppe zu senden.  
  
> [!NOTE]  
>  Informationen zum Ausführen der Klassifizierungsfunktion und der LOGON-Trigger werden in [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) und [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)verfügbar gemacht.  
  
## <a name="classification-function-tasks"></a>Tasks der Klassifizierungsfunktion  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt, wie benutzerdefinierte Klassifizierungsfunktionen erstellt und getestet werden.|[Erstellen und Testen einer benutzerdefinierten Klassifizierungsfunktion](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Aktivieren der Ressourcenkontrolle](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Arbeitsauslastungsgruppe der Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Konfigurieren der Ressourcenkontrolle mit einer Vorlage](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [Anzeigen der Eigenschaften der Ressourcenkontrolle](../../relational-databases/resource-governor/view-resource-governor-properties.md)  
  
  
