---
title: Arbeitsauslastungsgruppe der Ressourcenkontrolle | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Resource Governor, workload group
- workload groups [SQL Server]
- workload groups [SQL Server], overview
ms.assetid: a84c3c3f-55b6-4a30-9c42-13f082d9281e
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f137c0861604399a5dba67b0575184a52580f6f0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="resource-governor-workload-group"></a>Arbeitsauslastungsgruppe der Ressourcenkontrolle
  In der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ressourcenkontrolle werden Arbeitsauslastungsgruppen als Container für Sitzungsanforderungen mit ähnlichen Klassifizierungskriterien verwendet. Arbeitsauslastungen ermöglichen die gemeinsame Überwachung der Sitzungen und definieren Richtlinien für die Sitzungen. Jede Arbeitsauslastungsgruppe ist Teil eines Ressourcenpools, der wiederum eine Teilmenge der physischen Ressourcen einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]darstellt. Wenn eine Sitzung gestartet wird, weist die Klassifizierungsfunktion der Ressourcenkontrolle die Sitzung einer bestimmten Arbeitsauslastungsgruppe zu, und die Sitzung muss mit den der Arbeitsauslastungsgruppe zugewiesenen Richtlinien und den für den Ressourcenpool definierten Ressourcen ausgeführt werden.  
  
## <a name="workload-group-concepts"></a>Konzepte zu Arbeitsauslastungsgruppen  
 Eine Arbeitsauslastungsgruppe fungiert als Container für Sitzungsanforderungen, die sich gemäß den auf die einzelnen Anforderungen angewendeten Klassifikationskriterien ähneln. Sie ermöglicht die Überwachung der aggregierten Ressourcenbelegung und die Anwendung einer einheitlichen Richtlinie auf alle Anforderungen in der Gruppe. Eine Gruppe definiert die Richtlinien für ihre Elemente.  
  
> [!NOTE]  
>  Benutzerdefinierte Arbeitsauslastungsgruppen können zwischen Ressourcenpools verschoben werden.  
  
 Die Ressourcenkontrolle verfügt über zwei vordefinierte Arbeitsauslastungsgruppen: die interne Gruppe und die Standardgruppe. Interne Gruppen können von Benutzern nicht geändert werden. Sie können jedoch überwacht werden. Anforderungen werden der Standardgruppe zugeordnet, wenn die folgenden Bedingungen erfüllt sind:  
  
-   Es sind keine Kriterien zum Klassifizieren einer Anforderung vorhanden.  
  
-   Es wurde versucht, die Anforderung einer nicht vorhandenen Gruppe zuzuordnen.  
  
-   Ein allgemeiner Klassifizierungsfehler ist aufgetreten.  
  
 Die Ressourcenkontrolle stellt auch DDL-Anweisungen zum Erstellen, Ändern und Löschen von Arbeitsauslastungsgruppen bereit.  
  
## <a name="workload-group-tasks"></a>Tasks zu Arbeitsauslastungsgruppen  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt, wie eine Arbeitsauslastungsgruppe erstellt wird.|[Erstellen einer Arbeitsauslastungsgruppe](../../relational-databases/resource-governor/create-a-workload-group.md)|  
|Beschreibt, wie Einstellungen für Arbeitsauslastungsgruppen geändert werden.|[Ändern der Einstellungen von Arbeitsauslastungsgruppen](../../relational-databases/resource-governor/change-workload-group-settings.md)|  
|Beschreibt, wie eine Arbeitsauslastungsgruppe gelöscht wird.|[Löschen von Arbeitsauslastungsgruppen](../../relational-databases/resource-governor/delete-a-workload-group.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Aktivieren der Ressourcenkontrolle](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Klassifizierungsfunktion der Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [Konfigurieren der Ressourcenkontrolle mit einer Vorlage](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [Anzeigen der Eigenschaften der Ressourcenkontrolle](../../relational-databases/resource-governor/view-resource-governor-properties.md)  
  
  
