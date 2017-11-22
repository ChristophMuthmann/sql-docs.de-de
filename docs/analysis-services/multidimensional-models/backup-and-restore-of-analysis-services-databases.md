---
title: Sichern und Wiederherstellen von Analysis Services-Datenbanken | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.ssmsimbi.Restore.f1
- sql13.asvs.ssmsimbi.Backup.f1
helpviewer_keywords:
- backing up databases [Analysis Services]
- encryption [Analysis Services]
- databases [Analysis Services], restoring
- cryptography [Analysis Services]
- databases [Analysis Services], backing up
- restoring databases [Analysis Services]
- recovery [Analysis Services]
ms.assetid: 947eebd2-3622-479e-8aa6-57c11836e4ec
caps.latest.revision: "54"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 6f5db5fe3911767be37930fb7d195efffb826042
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="backup-and-restore-of-analysis-services-databases"></a>Sichern und Wiederherstellen von Analysis Services-Datenbanken
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verfügt über Sicherungs- und Wiederherstellungsfunktionen, weshalb Sie für eine Datenbank und ihre Objekte einen Zustand wiederherstellen können, der zu einem bestimmten Zeitpunkt gültig war. Die Sicherung und Wiederherstellung ist auch eine zulässige Methode zum Migrieren von Datenbanken zu aktualisierten Servern, zum Verschieben von Datenbanken zwischen Servern oder zum Bereitstellen einer Datenbank auf einem Produktionsserver. Zur Datenwiederherstellung sollten Sie, falls Sie noch nicht über einen Sicherungsplan verfügen und Ihre Daten wertvoll sind, so schnell wie möglich einen solchen Plan entwerfen und implementieren.  
  
 Die Befehle zur Sicherung und die Wiederherstellung werden in einer bereitgestellten Analysis Services-Datenbank ausgeführt. Für die Projekte und Projektmappen in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]sollten Sie mithilfe der Quellcodeverwaltung sicherstellen, dass Sie bestimmte Versionen der Quelldateien wiederherstellen können, und anschließend einen Datenwiederherstellungsplan für das Repository des von Ihnen verwendeten Quellcodeverwaltungssystems erstellen.  
  
 Eine vollständige Sicherung einschließlich der Quelldaten erfordert das Sichern der Datenbank, die Detaildaten enthält. Insbesondere, wenn Sie ROLAP- oder DirectQuery-Datenbankspeicher verwenden, werden Detaildaten in einer externen relationalen SQL Server-Datenbank gespeichert, die sich von der Analysis Services-Datenbank unterscheidet. Wenn alle Objekte demgegenüber tabellarisch oder mehrdimensional sind, schließt die Analysis Services-Sicherung sowohl die Metadaten als auch die Quelldaten ein.  
  
 Ein eindeutiger Vorzug der automatischen Sicherung besteht darin, dass die Datenmomentaufnahme stets so aktuell ist wie durch die automatisch gesteuerte Sicherungshäufigkeit vorgegeben. Automatische Planer stellen sicher, dass das Sichern nicht vergessen wird. Auch das Wiederherstellen einer Datenbank kann automatisiert werden. Dies ist gleichzeitig eine gute Möglichkeit zum Replizieren der Daten, doch achten Sie stets darauf, die Verschlüsselungsschlüsseldatei auf der Instanz, die die replizierten Daten erhält, ebenfalls zu sichern. Die Synchronisierungsfunktion ist für die Replizierung von Datenbanken von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bestimmt, doch sie erfasst nur veraltete Daten. Alle der hier genannten Funktionen können über die Benutzerschnittstelle implementiert werden, und zwar über XML/A-Befehle oder programmgesteuert über AMO. Weitere Informationen zu Sicherungsstrategien finden Sie unter [Backup Strategies with SQL Server 2005 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=81888)(Sicherungsstrategien mit SQL Server 2005 Analysis Services).  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Vorbereiten der Sicherung](#bkmk_prep)  
  
-   [Sichern einer mehrdimensionalen oder tabellarischen Datenbank](#bkmk_cube)  
  
-   [Wiederherstellen von Analysis Services-Datenbanken](#bkmk_restore)  
  
##  <a name="bkmk_prereq"></a> Erforderliche Komponenten  
 Sie müssen über Administratorberechtigungen für die Analysis Services-Instanz oder die Vollzugriffsberechtigungen (Administrator) für die Datenbank verfügen, die Sie sichern.  
  
 Der Wiederherstellungsort muss einer Analysis Services-Instanz entsprechen, die dieselbe Version oder eine neuere Version aufweist als die Instanz, auf der die Sicherung erstellt wurde. Obwohl Sie eine Datenbank von einer [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Instanz nicht auf einer früheren Version von Analysis Services wiederherstellen können, ist es üblich, eine Datenbank einer älteren Version, z.B. SQL Server 2012, auf einer neueren [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Instanz wiederherzustellen.  
  
 Der Wiederherstellungsort muss den gleichen Servertyp aufweisen. Tabellarische Datenbanken können nur auf einer Analysis Services-Instanz wiederhergestellt werden, die im tabellarischen Modus ausgeführt wird. Mehrdimensionale Datenbanken erfordern eine Instanz, die im mehrdimensionalen Modus ausgeführt wird.  
  
##  <a name="bkmk_prep"></a> Vorbereiten der Sicherung  
 Verwenden Sie die folgende Prüfliste, um die Sicherung vorzubereiten.  
  
-   Überprüfen Sie den Speicherort, an der die Sicherungsdatei gespeichert wird. Wenn Sie einen Remotestandort verwenden, müssen Sie es als UNC-Ordner angeben. Überprüfen Sie, ob Sie auf den UNC-Pfad zugreifen können.  
  
-   Überprüfen Sie die Berechtigungen für den Ordner, um sicherzustellen, dass das Analysis Services-Dienstkonto über Lese-/Schreibberechtigungen für den Ordner verfügt.  
  
-   Kontrollieren Sie den Zielserver auf ausreichenden Speicherplatz.  
  
-   Überprüfen Sie vorhandene Dateien mit gleichem Namen. Wenn bereits eine Datei mit dem gleichen Namen vorhanden ist, tritt ein Sicherungsfehler auf, sofern Sie keine Optionen zum Überschreiben der Datei festlegen.  
  
##  <a name="bkmk_cube"></a> Sichern einer mehrdimensionalen oder tabellarischen Datenbank  
 Administratoren können eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank unabhängig von der Datenbankgröße in einer einzelnen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Sicherungsdatei (.abf) sichern. Schritt-für-Schritt-Anweisungen finden Sie auf der TechMantra-Seite unter [How to Backup an Analysis Services Database](http://www.mytechmantra.com/LearnSQLServer/Backup_an_Analysis_Services_Database.html) (Sichern einer Analysis Services-Datenbank) und unter [Automate Backup an Analysis Services Database](http://www.mytechmantra.com/LearnSQLServer/Automate_Backup_of_Analysis_Services_Database.html)(Automatische Sicherung einer Analysis Services-Datenbank).  
  
> [!NOTE]  
>  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], zum Laden und Abfragen von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Datenmodelle in einer SharePoint-Umgebung werden die Modelle aus SharePoint-Inhaltsdatenbanken geladen. Diese Inhaltsdatenbanken sind relational und werden im relationalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankmodul ausgeführt. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bietet folglich keine Sicherungs-/Wiederherstellungsstrategie für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenmodelle. Wenn Sie einen Notfallwiederherstellungsplan für SharePoint-Inhalte eingerichtet haben, umfasst der Plan die in den Inhaltsdatenbanken gespeicherten [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenmodelle.  
  
 **Remotepartitionen**  
  
 Falls die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank Remotepartitionen enthält, sollten diese ebenfalls gesichert werden. Wenn Sie eine Datenbank mit Remotepartitionen sichern, werden alle Remotepartitionen auf jedem Remoteserver in einer einzigen Datei auf jedem der jeweiligen Remoteserver gesichert. Sollen diese Remotesicherungen also außerhalb der jeweiligen Hostcomputer erstellt werden, müssen Sie die zu sichernden Dateien manuell in die für sie bestimmten Speicherplatzbereiche kopieren.  
  
 **Inhalt einer Sicherungsdatei**  
  
 Beim Sichern einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank entsteht eine Sicherungsdatei, deren Inhalt je nach dem von den Datenbankobjekten verwendeten Speichermodus variiert. Dieser Unterschied beim Sicherungsinhalt geht auf den Umstand zurück, dass mit jedem Speichermodus eine andere Gruppe von Informationen innerhalb einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank gespeichert wird. So werden beispielsweise bei mehrdimensionalen, hybriden OLAP-Partitionen und -Dimensionen (HOLAP) sowohl Aggregationen als auch Metadaten in der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank gespeichert, während relationale OLAP-Partitionen und -Dimensionen (ROLAP) nur Metadaten in der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank speichern. Da der eigentliche Inhalt einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank je nach Speichermodus der einzelnen Partitionen variiert, variiert auch der Inhalt der Sicherungsdatei. Die folgende Tabelle ordnet den Inhalt der Sicherungsdatei dem von den Objekten verwendeten Speichermodus zu.  
  
|Speichermodus|Inhalt der Sicherungsdatei|  
|------------------|-----------------------------|  
|Multidimensionale MOLAP-Partitionen und -Dimensionen|Metadaten, Quelldaten und Aggregationen|  
|HOLAP-Partitionen und -Dimensionen (Multidimensionale OLAP)|Metadaten und Aggregationen|  
|ROLAP-Partitionen und -Dimensionen (Multidimensionale OLAP)|Metadaten|  
|Tabellarische, speicherinterne Modelle|Meta- und Quelldaten|  
|Tabellarische DirectQuery-Modelle|Nur Metadaten|  
  
> [!NOTE]  
>  Beim Sichern einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank werden nicht die Daten in den zugrunde liegenden Datenquellen, wie z. B. eine relationale Datenbank, gesichert. Nur der Inhalt der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank wird gesichert.  
  
 Wenn Sie eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank sichern, können Sie unter folgenden Optionen auswählen:  
  
-   Ob alle Datenbanksicherungen komprimiert werden sollen. Standardmäßig werden Sicherungen komprimiert.  
  
-   Ob der Inhalt der Sicherungsdateien verschlüsselt werden und für das Entschlüsseln und Wiederherstellen der Datei ein Kennwort erforderlich sein soll. Standardmäßig werden Sicherungsdateien nicht verschlüsselt.  
  
    > [!IMPORTANT]  
    >  Für jede Sicherungsdatei muss der Benutzer, der den Sicherungsbefehl ausführt, über die Berechtigung zum Schreiben in den für jede Datei angegebenen Sicherungsspeicherort verfügen. Dem Benutzer muss zudem eine der folgenden Rollen zugewiesen worden sein: Mitglied einer Serverrolle für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz oder Mitglied einer Datenbankrolle mit der Berechtigung „Vollzugriff“ (Administrator) für die wiederherzustellende Datenbank.  
  
 Weitere Informationen zum Sichern einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank finden Sie unter [Sicherungsoptionen](../../analysis-services/multidimensional-models/backup-options.md).  
  
##  <a name="bkmk_restore"></a> Wiederherstellen von Analysis Services-Datenbanken  
 Administratoren können eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank von einer oder mehreren Sicherungsdateien wiederherstellen.  
  
> [!NOTE]  
>  Falls die Sicherungsdatei verschlüsselt ist, können Sie sie erst für die Wiederherstellung einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank verwenden, nachdem Sie das beim Sichern verwendete Kennwort angegeben haben.  
  
 Während der Wiederherstellung stehen Ihnen folgende Optionen zur Verfügung:  
  
-   Sie können die Datenbank mit ihrem ursprünglichen Datenbanknamen wiederherstellen, oder Sie können einen neuen Datenbanknamen angeben.  
  
-   Sie können eine vorhandene Datenbank überschreiben. Falls Sie sich für das Überschreiben der Datenbank entscheiden, müssen Sie ausdrücklich angeben, dass die vorhandene Datenbank überschrieben werden soll.  
  
-   Sie können wählen, ob vorhandene Sicherheitsinformationen wiederhergestellt werden sollen oder ob Sie die Informationen zur Sicherheitsmitgliedschaft auslassen möchten.  
  
-   Sie können auswählen, ob der Wiederherstellungsbefehl den Wiederherstellungsordner für jede wiederherzustellende Partition ändern soll. Lokale Partitionen können an jedem Ordnerstandort wiederhergestellt werden, der für die Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , auf der die Datenbank wiederhergestellt wird, als lokal gilt. Remotepartitionen können in jedem Ordner und auf jedem Server außer dem lokalen Server wiederhergestellt werden. Remotepartitionen können nicht zu lokalen Partitionen werden.  
  
    > [!IMPORTANT]  
    >  Für jede Sicherungsdatei muss der Benutzer, der den Wiederherstellungsbefehl ausführt, über die Berechtigung zum Lesen von dem für jede Datei angegebenen Sicherungsspeicherort verfügen. Zum Wiederherstellen einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank, die nicht auf dem Server installiert ist, muss der Benutzer zusätzlich Mitglied der Serverrolle für die betreffende [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz sein. Zum Überschreiben einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank muss der Benutzer entweder Mitglied der Serverrolle für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz oder Mitglied einer Datenbankrolle mit der Berechtigung „Vollzugriff“ (Administrator) für die wiederherzustellende Datenbank sein.  
  
    > [!NOTE]  
    >  Nach dem Wiederherstellen einer vorhandenen Datenbank verliert der Benutzer, der die Datenbank wiederhergestellt hat, möglicherweise den Zugriff auf diese Datenbank. Dies ist u. U. der Fall, wenn der Benutzer zum Zeitpunkt der Sicherung kein Mitglied der Serverrolle oder der Datenbankrolle mit der Berechtigung "Vollzugriff (Administrator)" war.  
  
 Informationen zum Wiederherstellen einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank finden Sie unter [Wiederherstellungsoptionen](../../analysis-services/multidimensional-models/restore-options.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern, Wiederherstellen und Synchronisieren von Datenbanken &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)   

  
  
