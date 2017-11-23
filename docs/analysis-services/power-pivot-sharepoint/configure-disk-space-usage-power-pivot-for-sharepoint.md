---
title: "Konfigurieren der Speicherplatzverwendung (PowerPivot für SharePoint) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 201a3fda-f162-45d7-bf39-74dcb92fd0e6
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fa14e2c53a35ba1d8abe32766c6378d637a665ba
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configure-disk-space-usage-power-pivot-for-sharepoint"></a>Konfigurieren der Speicherplatzverwendung (Power Pivot für SharePoint)
  Eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Bereitstellung verwendet den verfügbaren Speicherplatz des Hostcomputers, um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbanken zum schnelleren Neuladen zwischenzuspeichern. Jede in den Arbeitsspeicher geladene [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbank wird zuerst auf einen Datenträger zwischengespeichert, damit sie später für neue Anforderungen schnell erneut geladen werden kann. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint nutzt standardmäßig den gesamten verfügbaren Speicherplatz zum Zwischenspeichern der zugehörigen Datenbanken. Sie können dieses Verhalten jedoch ändern, indem Sie Eigenschaften festlegen, durch die der verwendete Speicherplatz eingeschränkt wird.  
  
 In diesem Thema wird erklärt, wie Sie Grenzwerte für die Speicherplatzverwendung festlegen.  
  
 Dieses Thema stellt keine Anweisungen für die Speicherplatzverwaltung von (in Excel-Arbeitsmappen eingebetteten) [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbanken bereit, die in Inhaltsdatenbanken gespeichert werden. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Datenbanken können groß sein und dadurch neue Anforderungen an die Speicherkapazität der Farm stellen. Außerdem können bei aktivierter Versionsverwaltung schnell mehrere Kopien der Daten in derselben Inhaltsdatenbank vorhanden sein, wodurch sich der für die Inhaltsspeicherung erforderliche Speicherplatz weiter vergrößert. Obwohl [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbanken ein wichtiger Aspekt für die Datenträgerverwaltung sind, können sie nicht unabhängig von anderem in einer SharePoint-Farm gespeicherten Inhalt verwaltet werden. Sie müssen den Speicherplatz genauer überwachen, wenn Ihr Unternehmen verstärkt [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen verwendet. Sie können auch die Aktivität von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen im [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard nachverfolgen und nicht mehr verwendete Arbeitsmappen entfernen.  
  
## <a name="how-power-pivot-for-sharepoint-manages-cached-databases"></a>So verwaltet Power Pivot für SharePoint zwischengespeicherte Datenbanken  
 Zum Verwalten des Caches führt der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst in regelmäßigen Abständen einen Hintergrundauftrag zum Bereinigen nicht verwendeter oder veralteter Datenbanken aus, die neuere Versionen in einer Inhaltsbibliothek aufweisen. Der Zweck dieser Bereinigung ist, inaktive Datenbanken aus dem Arbeitsspeicher zu entladen und nicht verwendete, zwischengespeicherte Datenbanken aus dem Dateisystem zu löschen. Der Cleanupauftrag dient der langfristigen Wartung und stellt sicher, dass Datenbanken nicht unbegrenzt auf dem System bleiben. Auf einem aktiven Server können Datenbanken aufgrund von ungenügendem Arbeitsspeicher auf dem Server, des Löschens von Datenbanken in SharePoint oder neuerer Versionen der Datenbank in einer Inhaltsbibliothek öfter entfernt werden.  
  
 Obwohl Sie den Cleanupauftrag nicht planen können, können Sie die Verwaltung der Cachedatei anpassen, indem Sie Serverkonfigurationseigenschaften für folgende Aufgaben festlegen:  
  
-   Begrenzen des vom Cache verwendeten Speicherplatzes.  
  
-   Angeben der zu löschenden Datenmenge, wenn der maximale Speicherplatz erreicht wird.  
  
## <a name="how-to-check-disk-space-usage"></a>So überprüfen Sie die Speicherplatzverwendung  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint wird auf Anwendungsservern in einer SharePoint-Farm installiert. Jede Installation verfügt über ein Datenverzeichnis, das einen Sicherungsordner enthält. Der Sicherungsordner enthält alle Datendateien, die von der Analysis Services-Instanz auf dem Computer zwischengespeichert wurden. Standardmäßig befindet sich der Sicherungsordner im folgenden Pfad:  
  
 `%drive%:\Program Files\Microsoft SQL Server\MSAS10_50.PowerPivot\OLAP\Backup\Sandboxes\<serviceApplicationName>`  
  
 Um festzustellen, wie viel Gesamtspeicherplatz vom Cache verwendet wird, müssen Sie die Größe des Sicherungsordners überprüfen. Es gibt in der Zentraladministration keine Eigenschaft, die die aktuelle Cachegröße anzeigt.  
  
 Der Sicherungsordner stellt gemeinsam genutzten Cachespeicher für alle [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbanken bereit, die auf den lokalen Computer in den Arbeitsspeicher geladen werden. Wenn in der Farm mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen definiert sind, kann jede davon den lokalen Server verwenden, um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten zu laden und anschließend zwischenzuspeichern. Sowohl das Laden als auch das Zwischenspeichern von Daten sind Analysis Services-Servervorgänge. Die gesamte Speicherplatzverwendung wird somit auf Ebene der Analysis Services-Instanz im Sicherungsordner verwaltet. Konfigurationseinstellungen, die die Speicherplatzverwendung einschränken, werden daher für einzelne SQL Server Analysis Services-Instanzen festgelegt, die auf einem SharePoint-Anwendungsserver ausgeführt werden.  
  
 Der Cache enthält nur [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbanken. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Datenbanken werden in mehreren Dateien in einem einzelnen übergeordneten Ordner (dem Sicherungsordner) gespeichert. Da [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbanken als interne Daten für eine Excel-Arbeitsmappe verwendet werden sollen, sind Datenbanknamen GUID-basiert statt beschreibend. Ein GUID-Ordner unter  **\<ServiceApplicationName >** ist der übergeordnete Ordner einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Datenbank. Beim Laden von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbanken auf den Server werden zusätzliche Ordner für jede einzelne Datenbank erstellt.  
  
 Da [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten unter Umständen in jede Analysis Services-Instanz in einer Farm geladen werden, könnten die gleichen Daten auch auf mehreren Computern in der Farm zwischengespeichert werden. Dabei hat die Leistung Vorrang gegenüber der Speicherplatzauslastung, allerdings haben Benutzer schneller Zugriff auf Daten, wenn diese bereits auf dem Datenträger verfügbar sind.  
  
 Sie können Sie den Dienst beenden und eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbank aus dem Sicherungsordner löschen, um den Speicherplatzverbrauch sofort zu reduzieren. Das manuelle Löschen von Dateien ist eine temporäre Maßnahme, da bei der nächsten Abfrage der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten wieder eine neuere Kopie der Datenbank zwischengespeichert wird. Dauerhafte Lösungen sind z. B. das Beschränken des vom Cache verwendeten Speicherplatzes.  
  
 Auf Systemebene können Sie E-Mail-Warnungen erstellen, die Sie benachrichtigen, wenn der Speicherplatz gering ist. Microsoft System Center enthält eine E-Mail-Benachrichtigungsfunktion. Sie können Warnungen auch mithilfe des Ressourcen-Managers für Dateiserver, des Taskplaners oder PowerShell-Skripts einrichten. Unter den folgenden Links erhalten Sie nützliche Informationen zum Einrichten von Benachrichtigungen zu niedrigem Speicherplatz:  
  
-   [Neuigkeiten im Ressourcen-Manager für Dateiserver (File Server Resource Manager, FSRM)](http://technet.microsoft.com/library/hh831746.aspx) (http://technet.microsoft.com/library/hh831746.aspx).  
  
-   [File Server Resource Manager Step-by-Step Guide for Windows Server 2008 R2](http://go.microsoft.com/fwlink/?LinkID=204875) (Schritt-für-Schritt-Anleitung für den Ressourcen-Manager für Dateiserver für Windows Server 2008 R2) (http://go.microsoft.com/fwlink/?LinkID=204875).  
  
-   [Setting low disk space alerts on Windows Server 2008](http://go.microsoft.com/fwlink/?LinkID=204870) (Festlegen von Warnungen zu niedrigem Speicherplatz auf Windows Server 2008) (http://go.microsoft.com/fwlink/?LinkID=204870).  
  
## <a name="how-to-limit-the-amount-of-disk-space-used-for-storing-cached-files"></a>So schränken Sie den zum Speichern von zwischengespeicherten Dateien verwendeten Speicherplatz ein  
  
1.  Klicken Sie in der Zentraladministration unter „Anwendungsverwaltung“ auf **Dienste auf dem Server verwalten**.  
  
2.  Klicken Sie auf **SQL Server Analysis Services**.  
  
     Beachten Sie, dass Obergrenzen in der Analysis Services-Instanz festgelegt werden, die auf dem physischen Server ausgeführt wird, und nicht auf Dienstanwendungsebene. Für alle Dienstanwendungen, die die lokale Analysis Services-Instanz verwenden, gilt der für diese Instanz festgelegte maximale Speicherplatz.  
  
3.  Legen Sie unter „Datenträgerverwendung“ einen Wert für **Speicherplatz insgesamt** fest (in Gigabyte), um eine Obergrenze für den zum Zwischenspeichern verwendeten Speicherplatz festzulegen. Der Standardwert beträgt 0, d. h. Analysis Services kann den gesamten verfügbaren Speicherplatz verwenden.  
  
4.  Geben Sie unter „Datenträgerverwendung“ für die Einstellung **Delete cached databases in last ‘n’ hours** (In den letzten „n“ Stunden zwischengespeicherte Datenbanken löschen) Kriterien für die letzte Verwendung an, um den Cache bei Erreichen des maximalen Speicherplatzes zu leeren.  
  
     Der Standardwert sind 4 Stunden, d. h. alle Datenbanken, die für 4 Stunden oder mehr inaktiv waren, werden aus dem Dateisystem gelöscht. Datenbanken, die inaktiv, aber weiterhin im Arbeitsspeicher vorhanden sind, werden entladen und dann aus dem Dateisystem gelöscht.  
  
## <a name="how-to-limit-how-long-a-database-is-kept-in-the-cache"></a>So schränken Sie die Dauer ein, für die eine Datenbank zwischengespeichert wird  
  
1.  Klicken Sie in der Zentraladministration unter „Anwendungsverwaltung“ auf **Dienstanwendungen verwalten**.  
  
2.  Klicken Sie auf **Standard-[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Serviceanwendung**, um das Management-Dashboard zu öffnen.  
  
3.  Klicken Sie unter „Aktionen“auf **Einstellungen für Dienstanwendung konfigurieren**.  
  
4.  Im Abschnitt Datenträgercache können Sie angeben, wie lang eine inaktive Datenbank im Arbeitsspeicher bleibt, falls neue Anforderungen empfangen werden (standardmäßig 48 Stunden), und wie lang sie im Cache bleibt (standardmäßig 120 Stunden).  
  
     Unter**Inaktive Datenbank im Arbeitsspeicher behalten** wird angegeben, wie lang eine inaktive Datenbank im Arbeitsspeicher bleibt, falls neue Anforderungen für diese Daten empfangen werden. Eine aktive Datenbank wird immer im Arbeitsspeicher beibehalten, solange Sie sie abfragen. Wenn die Datenbank jedoch nicht mehr aktiv ist, behält das System sie für einen zusätzlichen Zeitraum im Arbeitsspeicher, falls weitere Anforderungen für diese Daten empfangen werden.  
  
     Da [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbanken zuerst zwischengespeichert und dann in den Arbeitsspeicher geladen werden, belegen Datenbankdateien sofort Speicherplatz. Während die Datenbank jedoch aktiv ist (und danach für 48 Stunden), werden alle Anforderungen zuerst an die Datenbank im Arbeitsspeicher weitergeleitet. Dabei wird die zwischengespeicherte Datenbank ignoriert. Nach 48 Stunden Inaktivität wird die Datei aus dem Arbeitsspeicher entladen, bleibt jedoch im Cache, wo sie schnell erneut geladen werden kann, wenn eine neue Verbindungsanforderung für diese Daten von der lokalen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Serverinstanz abgefangen wird. Verbindungsanforderungen an eine inaktive Datenbank werden vom Cache und nicht der Inhaltsbibliothek bedient, wodurch die Auswirkungen auf die Inhaltsdatenbanken minimiert werden.  
  
     Beachten Sie, dass die Inhaltsbibliothek der einzige dauerhafte Speicherort für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbanken ist. Zwischengespeicherte Kopien werden nur verwendet, wenn die Datenbank in der Bibliothek mit der Kopie auf dem Datenträger übereinstimmt.  
  
     Unter**Inaktive Datenbank im Cache behalten** wird angegeben, wie lange eine inaktive Datenbank im Dateisystem bleibt, nachdem sie aus dem Arbeitsspeicher entladen wurde. Der Cleanupauftrag verwendet diese Einstellung, um die zu löschenden Dateien zu bestimmen. Alle [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbanken, die 168 Stunden lang (48 Stunden im Arbeitsspeicher und 120 Stunden im Cache) inaktiv sind, werden durch den Cleanupauftrag vom Datenträger gelöscht.  
  
5.  Klicken Sie auf **OK** , um die Änderungen zu speichern.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Installation stellt Integritätsregeln bereit, sodass Sie Korrekturmaßnahmen ergreifen können, wenn Probleme bei Integrität, Konfiguration oder Verfügbarkeit des Servers erkannt werden. Einige dieser Regeln bestimmen mithilfe von Konfigurationseinstellungen die Bedingungen, unter denen Integritätsregeln ausgelöst werden. Beim aktiven Optimieren der Serverleistung können Sie auch diese Einstellungen überprüfen, um sicherzustellen, dass die Standardwerte für das System am besten geeignet sind. Weitere Informationen finden Sie unter [Konfigurieren von Power Pivot-Integritätsregeln](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-health-rules.md).  
  
## <a name="see-also"></a>Siehe auch  
 [PowerPivot-Serververwaltung und -konfiguration in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
