---
title: "Wartungspl&#228;ne | Microsoft Docs"
ms.custom: ""
ms.date: "08/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.AG.MAINTPLAN.LEGACY.F1"
helpviewer_keywords: 
  - "Wartungspläne [SQL Server-Agent], Informationen zu Datenbank-Wartungsplänen"
  - "Wartungspläne [SQL Server], im Designer angezeigter Datenbank-Kompatibilitätsgrad"
  - "Wartungspläne [SQL Server]"
ms.assetid: 5982ca65-74fe-44e3-aef9-00a65a0db169
caps.latest.revision: 44
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 44
---
# Wartungspl&#228;ne
  Mit Wartungsplänen wird ein Workflow der Tasks erstellt, die erforderlich sind, um sicherzustellen, dass Ihre Datenbank optimiert und regelmäßig gesichert wird und dass sie keine Inkonsistenzen aufweist. Mit dem Wartungsplanungs-Assistenten werden zudem zentrale Wartungspläne erstellt, doch durch das manuelle Erstellen von Plänen steht Ihnen eine sehr viel höhere Flexibilität zur Verfügung.  
  
## Vorteile von Wartungsplänen  
 In [!INCLUDE[ssDECurrent](../../includes/ssdecurrent-md.md)]wird mit Wartungsplänen ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket erstellt, das durch einen Auftrag des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents ausgeführt wird. Wartungspläne können manuell oder automatisch in bestimmten Zeitabständen ausgeführt werden.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Wartungspläne bieten folgende Funktionen:  
  
-   Workflowerstellung mithilfe einer Reihe typischer Wartungstasks. Außerdem können Sie benutzerdefinierte [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts erstellen.  
  
-   Konzeptionelle Hierarchien. Mit jedem Plan können Sie Workflows mit Tasks erstellen und bearbeiten. Die Tasks in den einzelnen Plänen können in Unterpläne gruppiert werden, die zu unterschiedlichen Zeiten nach einem Zeitplan ausgeführt werden können.  
  
-   Es werden Multiserverpläne unterstützt, die in Masterserver-/Zielserverumgebungen verwendet werden können.  
  
-   Die Protokollierung von Planverläufen auf Remoteservern wird unterstützt.  
  
-   Windows-Authentifizierung und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung werden unterstützt. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## Funktionalität von Wartungsplänen  
 Wartungspläne können zum Ausführen der folgenden Tasks erstellt werden:  
  
-   Erneutes Organisieren der Daten auf den Daten- und Indexseiten durch erneutes Erstellen von Indizes mit einem neuen Füllfaktor. Durch das erneute Erstellen von Indizes mit einem neuen Füllfaktor wird sichergestellt, dass für den Inhalt von Datenbankseiten das Verhältnis zwischen der Menge an Daten und freiem Speicherplatz ausgewogen ist. Darüber hinaus wird das zukünftige Wachstum beschleunigt. Weitere Informationen finden Sie unter [Angeben des Füllfaktors für einen Index](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).  
  
-   Komprimieren von Datendateien durch Entfernen leerer Datenbankseiten.  
  
-   Aktualisieren der Indexstatistik, um sicherzustellen, dass der Abfrageoptimierer über aktuelle Informationen zur Verteilung der Datenwerte in den verschiedenen Tabellen verfügt. Auf diese Weise kann der Abfrageoptimierer die optimale Methode für den Zugriff auf die Daten besser ermitteln, da mehr Informationen über die in der Datenbank gespeicherten Daten zur Verfügung stehen. Die Indexstatistik wird zwar automatisch in regelmäßigen Abständen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisiert, hierdurch erhalten Sie jedoch die Möglichkeit, das sofortige Update der Statistik zu erzwingen.  
  
-   Ausführen interner Konsistenzprüfungen für die Daten und Datenseiten innerhalb der Datenbank, um sicherzustellen, dass ein System- oder Softwareproblem nicht zur Beschädigung von Daten geführt hat.  
  
-   Sichern der Datenbank und Transaktionsprotokolldateien. Datenbank- und Protokollsicherungen können für einen angegebenen Zeitraum beibehalten werden. Dies ermöglicht Ihnen die Erstellung eines Sicherungsverlaufs, anhand dessen Sie eine Version der Datenbank wiederherstellen können, die weiter zurückliegt als die letzte Datenbanksicherung. Darüber hinaus können Sie eine differenzielle Sicherung vornehmen.  
  
-   Ausführen von Aufträgen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents. Auf diese Weise können Aufträge, die eine Vielzahl von Aktionen durchführen, und die Wartungspläne für die Ausführung dieser Aufträge erstellt werden.  
  
 Die von den Wartungstasks generierten Ergebnisse können als Bericht in eine Textdatei oder in die Wartungsplantabellen (**sysmaintplan_log** und **sysmaintplan_logdetail**) in **msdb** geschrieben werden. Um die Ergebnisse im Protokolldatei-Viewer anzuzeigen, klicken Sie mit der rechten Maustaste auf **Wartungspläne**, und klicken Sie anschließend auf **Verlauf anzeigen**.  
  
## Verwandte Aufgaben  
 Erste Schritte mit Wartungsplänen mithilfe der folgenden Themen:  
  
|||  
|-|-|  
|**Beschreibung**|**Thema**|  
|Konfigurieren der **Agent XPs**-Serverkonfigurationsoption, um erweiterte gespeicherte Prozeduren für SQL Server Agent zu aktivieren.|[Agent XPs (Serverkonfigurationsoption)](../../database-engine/configure-windows/agent-xps-server-configuration-option.md)|
|Beschreibt, wie ein Wartungsplan mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] erstellt wird.|[Erstellen eines Wartungsplans](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)|  
|Beschreibt, wie ein Wartungsplan mithilfe der Wartungsplan-Entwurfsbenutzeroberfläche erstellt wird.|[Erstellen eines Wartungsplans &#40;Entwurfsoberfläche für Wartungspläne&#41;](../../relational-databases/maintenance-plans/create-a-maintenance-plan-maintenance-plan-design-surface.md)|  
|Dokumentiert die Funktionalität von Wartungsplänen im Objekt-Explorer.|[Knoten Wartungspläne &#40;Objekt-Explorer&#41;](../../relational-databases/maintenance-plans/maintenance-plans-node-object-explorer.md)|  
  
  