---
title: "&#220;berwachen von Datenebenenanwendungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-data-tier-apps"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Überwachung [SQL Server], Datenebenenanwendungen"
  - "Überwachen der Serverleistung [SQL Server], DACs"
  - "Datenebenenanwendung [SQL Server], Überwachung"
ms.assetid: d2765828-2385-4019-aef2-1de3ab7d1b26
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# &#220;berwachen von Datenebenenanwendungen
  Eine Datenebenenanwendung (DAC) kann vom **Hilfsprogramm-Explorer** und **Objekt-Explorer** zusammen mit Systemsichten und -tabellen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) überwacht werden. Zusätzlich können alle Objekte der in der DAC enthaltenen Datenbank mithilfe standardmäßiger Datenbank- und [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Überwachungsverfahren überwacht werden.  
  
## Vorbereitungen  
 Beim Bereitstellen einer DAC in einer verwalteten Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]werden Informationen über die bereitgestellte DAC in das SQL Server-Hilfsprogramm integriert, wenn der Hilfsprogramm-Sammlungssatz das nächste Mal von der Instanz an den Steuerungspunkt für das Hilfsprogramm gesendet wird. Sie können dann grundlegende Zustandsinformationen zur DAC mit dem [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Hilfsprogramm-Explorer**.  
  
 Der SSMS- **Objekt-Explorer** zeigt grundlegende Konfigurationsinformationen zu den einzelnen DACs an, die auf einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]bereitgestellt werden, unabhängig von, ob die Instanz im SQL Server-Hilfsprogramm verwaltet wird. Darüber hinaus kann die Datenbank, die mit einer bereitgestellten DAC verknüpft ist, mit den gleichen Prozeduren zum Überwachen aller Datenbanken überwacht werden.  
  
## Verwenden des SQL Server-Hilfsprogramms  
 Im **Hilfsprogramm-Explorer** von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] wird auf der Detailseite **Bereitgestellte Datenebenenanwendungen** ein Dashboard angezeigt, das Aufschluss über die Ressourcennutzung aller DACs gibt, die auf verwalteten [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanzen bereitgestellt wurden. Im oberen Bereich der Detailseite wird jede bereitgestellte DAC mit visuellen Indikatoren aufgeführt, die aufzeigen, ob die Nutzungswerte der CPU und der Dateiressourcen außerhalb der für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramm definierten Richtlinien liegen. Wenn Sie eine DAC in der Listenansicht auswählen, werden weitere Details auf Registerkarten im unteren Bereich der Seite angezeigt. Weitere Informationen zu den auf der Detailseite angezeigten Informationen finden Sie unter [Details zu bereitgestellten Datenebenenanwendungen &#40;SQL Server-Hilfsprogramm&#41;](../Topic/Deployed%20Data-tier%20Application%20Details%20\(SQL%20Server%20Utility\).md).  
  
 Nachdem Sie mithilfe der Detailseite **Bereitgestellte Datenebenenanwendungen** schnell die DACs ermittelt haben, bei denen eine Unter- oder Überauslastung der Hardwareressource vorliegt, können Sie Pläne zur Lösung eines bestimmten Problems erarbeiten. Mehrere DACs, die ihre aktuellen Hardwareressourcen nicht vollständig ausnutzen, könnten auf einem einzelnen Server konsolidiert werden, sodass einige der Server für andere Zwecke freigegeben werden. Wenn eine DAC die Ressourcen auf ihrem aktuellen Server überbeansprucht, kann sie auf einen größeren Server umgelagert werden, oder Sie können dem aktuellen Server weitere Ressourcen hinzufügen.  
  
 Die minimalen und maximalen Grenzwerte für die Ressourcenverwendung werden von Richtlinien zur Anwendungsüberwachung definiert, die auf der Detailseite **Hilfsprogrammverwaltung** festgelegt werden. Datenbankadministratoren können die Richtlinien an die von ihrem Unternehmen festgelegten Grenzwerte anpassen. Beispielweise könnte ein Unternehmen die maximale CPU-Auslastung für eine DAC auf 75 % festlegen, während ein anderes Unternehmen diesen Wert auf 80 % festlegt. Weitere Informationen zum Festlegen von Richtlinien für die Anwendungsüberwachung finden Sie unter [Hilfsprogrammverwaltung &#40;SQL Server-Hilfsprogramm&#41;](../Topic/Utility%20Administration%20\(SQL%20Server%20Utility\).md).  
  
 So zeigen Sie die Detailseite **Bereitgestellte Datenebenenanwendungen** an:  
  
1.  Wählen Sie das Menü **Ansicht/Hilfsprogramm-Explorer** aus.  
  
2.  Verbinden Sie den **Hilfsprogramm-Explorer** mit dem Steuerungspunkt für das Hilfsprogramm (UCP, Utitility Control Point).  
  
3.  Wählen Sie das Menü **Ansicht/Details zum Hilfsprogramm-Explorer** aus.  
  
4.  Wählen Sie im **Hilfsprogramm-Explorer** den Knoten **Bereitgestellte Datenebenenanwendungen** aus.  
  
 Die Informationen auf der Detailseite **Bereitgestellte Datenebenenanwendungen** stammen aus den Daten des UMDWs (Utility Management Data Warehouse), in dem die Daten standardmäßig alle 15 Minuten erfasst werden. Das Intervall kann ebenfalls auf der Detailseite **Hilfsprogrammverwaltung** angepasst werden.  
  
## Verwenden des Objekt-Explorers  
 Der **Objekt-Explorer** von SSMS zeigt grundlegende Konfigurationsinformationen zu jeder DAC an, die auf einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz bereitgestellt wurde. Dies schließt sowohl verwaltete Instanzen ein, die im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramm registriert wurden, als auch eigenständige Instanzen, die nicht im **Hilfsprogramm-Explorer** angezeigt werden können.  
  
 So zeigen Sie die Details einer auf einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz bereitgestellten DAC an:  
  
1.  Wählen Sie das Menü **Ansicht/Objekt-Explorer** aus.  
  
2.  Stellen Sie im Bereich "Objekt-Explorer" eine Verbindung mit der [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
3.  Wählen Sie das Menü **Ansicht/Details zum Objekt-Explorer** aus.  
  
4.  Wählen Sie den Serverknoten im **Objekt-Explorer** aus, der der Instanz zugeordnet ist, und navigieren Sie dann zum Knoten **Verwaltung\Datenebenenanwendungen**.  
  
5.  In der Listenansicht im oberen Bereich der Detailseite wird jede DAC aufgeführt, die auf der [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz bereitgestellt wurde. Wählen Sie eine DAC aus, um die Informationen im Detailbereich unten auf der Seite anzuzeigen.  
  
 Das Kontextmenü des Knotens **Datenebenenanwendungen** wird auch dazu verwendet, eine neue DAC bereitzustellen oder eine vorhandene zu löschen.  
  
## Verwenden von DAC-Systemsichten und -tabellen  
 In der Systemtabelle msdb.dbo.sysdac_history_internal wird aufgezeichnet, ob die für eine [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz ausgeführten DAC-Verwaltungsaktionen erfolgreich oder fehlerhaft waren. Die Tabelle enthält den Zeitpunkt jeder Aktion sowie den Anmeldenamen, unter dem die Aktion initiiert wurde. Weitere Informationen finden Sie unter [sysdac_history_internal &#40;Transact-SQL&#41;](../Topic/sysdac_history_internal%20\(Transact-SQL\).md).  
  
 Die DAC-Systemsichten enthalten grundlegende Kataloginformationen. Weitere Informationen finden Sie unter [Sichten von Datenebenenanwendungen &#40;Transact-SQL&#41;](../Topic/Data-tier%20Application%20Views%20\(Transact-SQL\).md).  
  
## Überwachen von DAC-Datenbanken  
 Nachdem eine DAC erfolgreich bereitgestellt wurde, funktioniert die in der DAC enthaltene Datenbank genauso wie jede andere Datenbank. Verwenden Sie die [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Standardtechniken und -tools zum Überwachen von Leistung, Protokollen, Ereignissen und Ressourcennutzung der Datenbank.  
  
## Siehe auch  
 [Datenebenenanwendungen](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Bereitstellen einer Datenebenenanwendung](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)  
  
  