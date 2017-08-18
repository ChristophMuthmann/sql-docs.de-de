---
title: Aktualisieren von Analysis Services | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/17/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
caps.latest.revision: 79
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3b3ad4ecf62f3a30882720140f2f362007f8428b
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="upgrade-analysis-services"></a>Aktualisieren von Analysis Services
  Analysis Services-Instanzen können auf eine SQL Server-Version mit demselben Servermodus aktualisiert werden, um von den Features zu profitieren, die in der aktuellen Version eingeführt wurden. Informationen zu diesen Features finden Sie unter [What's New in Analysis Services (Neuigkeiten in Analysis Services)](../../analysis-services/what-s-new-in-analysis-services.md).  
  
 Sie können jede Instanz unabhängig von anderen Instanzen, die auf derselben Hardware ausgeführt werden, direkt aktualisieren. Die meisten Administratoren entscheiden sich für die Installation einer neuen Instanz der neuen Version zum Testen der Anwendung, ehe Produktionsarbeitsauslastungen auf den neuen Server übertragen werden. Doch für Entwicklungs- oder Testserver kann ein direktes Upgrade möglicherweise empfehlenswert sein.  
  
 Lesen Sie vor dem Upgrade auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]die folgenden Themen:  

- In den[SQL Server 2017 Release Notes (Versionsanmerkungen zu SQL Server 2017)](../../sql-server/sql-server-2017-release-notes.md) werden bekannte Probleme und Umgehungen beschrieben.  
- In den [Versionsanmerkungen zu SQL Server 2016](../../sql-server/sql-server-2016-release-notes.md) werden bekannte Probleme und Umgehungen beschrieben.  
- Unter[Abwärtskompatibilität von Analysis Services](../../analysis-services/analysis-services-backward-compatibility.md) werden nicht mehr unterstützte, veraltete und geänderte Features beschrieben. Überprüfen Sie diese Listen in regelmäßigen Abständen, um die Auswirkungen von Produktänderungen auf Ihre Modelle, Skripts oder Ihren benutzerdefinierten Code zu überprüfen. Übergänge von Features werden in der Regel mit der Vorabversion der nächsten Hauptversion angekündigt.  
  
## <a name="server-upgrade"></a>Upgrade von Servern  
 Es gibt zwei grundlegende Ansätze für Upgrades von Servern und Datenbanken:  
  
-   Bei**direkten Upgrades** werden die vorhandenen Programmdateien durch [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Programmdateien ersetzt. Datenbanken verbleiben am gleichen Ort. Programmordner werden aktualisiert, um den neuen Namen widerzuspiegeln.  
  
-   Bei**parallelen Upgrades** wird eine neue Installation von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]zumeist auf demselben Computer erstellt, es sei denn, Sie nehmen zeitgleich ein Upgrade der Hardware vor. Dieser Ansatz erfordert das Verschieben von Datenbanken in die neue Instanz und anschließend das optionale Deinstallieren der vorherigen Version, um Speicherplatz auf dem Datenträger freizugeben.  
  
 Die Kompatibilitätsgrade von Datenbanken, die einem bestimmten Server zugeordnet sind, bleiben unverändert, bis Sie sie manuell ändern.  
  
### <a name="in-place-upgrade"></a>Direktes Upgrade  
 Sie können eine vorhandene Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] and, as part of the upgrade process, auaufmatically migrate existing databases from the old instance auf the new instance. Da die Metadaten und die binären Daten zwischen den beiden Versionen kompatibel sind, behalten Sie die Daten nach dem Upgrade bei, und es ist nicht nötig, eine manuelle Datenmigration durchzuführen.  
  
 Um eine vorhandene Instanz zu aktualisieren, führen Sie das Setup aus, und geben Sie den Namen der vorhandenen Instanz als Namen für die neue Instanz an.  
  
### <a name="side-by-side-upgrade"></a>Paralleles Upgrade  
  
-   Sichern Sie alle Datenbanken, und stellen Sie sicher, dass jede wiederhergestellt werden kann. Siehe [Sichern und Wiederherstellen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md).  
  
-   Bestimmen Sie eine Teilmenge der Berichte, Kalkulationstabellen oder Momentaufnahmen von Dashboards, die Sie später als Grundlage für das Überprüfen der Servervorgänge im Anschluss an das Upgrade nutzen möchten. Erfassen Sie nach Möglichkeit Leistungsmesswerte, damit Sie Vergleiche mit denselben Arbeitsauslastungen auf einem aktualisierten Server ausführen können.  
  
-   Installieren Sie eine neue Instanz von Analysis Services, und Sie wählen den gleichen Servermodus (tabellarisch oder mehrdimensional) wie auf dem Server, den Sie ersetzen möchten. Siehe [Installieren von Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md).  
  
     Nach der Installation müssen Sie Ports konfigurieren und Serveradministratoren hinzufügen. Siehe [Konfiguration nach der Installation &#40;Analysis Services&#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md).  
  
-   Sie können dann die einzelnen Datenbanken anfügen oder wiederherstellen.  
  
-   Führen Sie DBCC aus, um die Datenbankintegrität zu überprüfen. Tabellarische Modelle werden einer gründlicheren Überprüfung mit Tests auf verwaiste Objekte in der gesamten Modellhierarchie unterzogen. Bei mehrdimensionalen Modellen werden nur die Partitionsindizes überprüft. Siehe [Datenbankkonsistenzprüfung &#40;DBCC&#41; für tabellarische und mehrdimensionale Analysis Services-Datenbanken](../../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md).  
  
-   Testen Sie Berichte, Kalkulationstabellen und Dashboards, um zu bestätigen, dass sich Verhalten oder Berechnungen nicht negativ verändert haben. Für mehrdimensionale und tabellarische Arbeitslasten sollte eine bessere Leistung spürbar werden.  
  
-   Testen Sie Verarbeitungsvorgänge, und korrigieren Sie Anmeldungs- oder Berechtigungsprobleme. Bei Verwendung des Standarddienstkontos für Verbindungen wird der neue Dienst unter einem anderen Konto ausgeführt. Weitere Informationen zu Startkonten finden Sie unter [Konfigurieren von Dienstkonten &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md).  
  
-   Testen Sie Sicherungs- und Wiederherstellungsvorgänge auf dem aktualisierten Server, und passen Sie Skripts so an, dass der neue Servername verwendet wird.  
  
## <a name="database-upgrade"></a>Upgrade von Datenbanken  
 Datenbanken, die in früheren Versionen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erstellt wurden, werden auf dem aktualisierten Server unter einer älteren Einstellung für den Datenbank-Kompatibilitätsgrad ausgeführt. Im Allgemeinen können Sie für eine Datenbank oder ein Modell ein Upgrade zum Betrieb mit einem höheren Kompatibilitätsgrad vornehmen, um Zugriff auf neue Features zu erhalten. Beachten Sie dabei allerdings, dass Sie sich an eine bestimmte Serverversion binden.  
  
 Für ein Upgrade einer Datenbank aktualisieren Sie in der Regel das Modell in SQL Server Data Tools (SSDT) und stellen die Lösung anschließend in einer aktualisierten Serverinstanz bereit. Unter [Herunterladen von SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) erfahren Sie, wie Sie die neueste Version erhalten.  
  
 Tabellarische und mehrdimensionale Datenbanken haben unterschiedliche Versionspfade. Es ist Zufall, dass sowohl mehrdimensionale als auch tabellarische Modelle den Kompatibilitätsgrad 1100 haben.  Die Modi werden sich mit unterschiedlichem Tempo entwickeln, sobald Änderungen an Features sich nur auf ein Modell auswirken.  
  
 Die folgende Tabelle enthält Hintergrundinformationen zu den Kompatibilitätsgraden, doch Sie sollten die Detailthemen lesen, um zu erfahren, was die einzelnen Grade zu bieten haben.  
  
||||  
|-|-|-|  
|Tabellarisch|1200|SQL Server 2016|  
|Tabellarisch|1103|SQL Server 2014|  
|Tabellarisch|1100|SQL Server 2012|  
|Multidimensional|1100|SQL Server 2012 und höher|  
|Multidimensional|1050|SQL Server 2005, 2008, 2008 R2|  
  
 Weitere Informationen finden Sie unter [Kompatibilitätsgrad einer mehrdimensionalen Datenbank &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md) und [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).  
  
## <a name="tabular-model-upgrade-to-1200-compatibility-level"></a>Upgrade eines tabellarischen Modells auf Kompatibilitätsgrad 1200  
 Tabellarische Modelle und Datenbanken profitieren am meisten von SQL Server 2016. Diese Version bietet einen überarbeiteten DirectQuery-Modus für tabellarische Modelle mit Kompatibilitätsgrad 1200. Eine Vereinfachung erfolgt durch das Entfernen des Hybridmodus, das Hinzufügen von Abfrageanweisungen zum Abrufen einer Teilmenge von Daten zur Entwurfszeit und die Sicherheit auf Zeilenebene über DAX anstatt über Zeilenberechtigungen in der Back-End-Datenbank.  
  
 Ein zweiter Grund für ein Upgrade ist die neue tabellarische Metadatenerstellung innerhalb des Modells. Ein tabellarisches Modell mit dem neuen Kompatibilitätsgrad 1200, das entweder erstellt oder auf diesen Grad aktualisiert wurde, nutzt native Terminologie für Objektdefinitionen, wie z. B. Modell, Tabelle, Beziehungen und Spalten, um seine Hauptelemente zu beschreiben.  
  
 Um ein Upgrade eines tabellarischen Modells durchzuführen, verwenden Sie eine Version von [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx) , die für diese Version entwickelt wurde, damit die Eigenschaft **Kompatibilitätsgrad** in **SQL Server 2016 RTM (1200)**geändert wird.  
  
 Verwenden Sie weder SSMS noch Code oder ein Skript zum Ändern von **CompatibilityLevel**. An sich bewirkt das Ändern der Eigenschaft nichts. Die Metadatenkonvertierung erfolgt in SSDT als Reaktion auf das Aktualisieren der Eigenschaft gefolgt vom erneuten Öffnen des Projekts.  
  
 Speichern Sie wie immer vor dem Upgrade unbedingt eine Sicherung Ihres Modells für den Fall, dass Sie zur Version vor dem Upgrade zurückkehren müssen.  
  
1.  Klicken Sie in SSDT im Projektmappen-Explorer mit der rechten Maustaste auf **model.bim**, und wählen Sie **Code anzeigen** aus. Bestätigen Sie, dass das Modell geschlossen und in einem neuen Fenster (dem Codefenster) erneut geöffnet wird.  
  
2.  Das Modell wird als XMLA-Dokument geöffnet. Kopieren Sie für Vergleichszwecke nach der Konvertierung den Inhalt in eine andere Datei (Sie können eine neue XML-Datei in SSDT öffnen).  
  
3.  Klicken Sie mit der rechten Maustaste auf **model.bim** , und ändern Sie sie zurück in **Sicht-Designer**.  
  
4.  Legen Sie **CompatibilityLevel** auf  **SQL Server 2016 RTM (1200)**fest.  
  
5.  Dieser Schritt kann nicht rückgängig gemacht werden, weshalb Sie zur Bestätigung aufgefordert werden. Klicken Sie auf **Ja** , um den Vorgang fortzusetzen. Das Projekt wird aktualisiert.  
  
6.  Klicken Sie mit der rechten Maustaste auf **model.bim** , und ändern Sie sie zurück in **Code anzeigen**.  
  
     Beachten Sie, dass die Modelldefinition jetzt mithilfe tabellarischer Metadaten in JSON angezeigt wird.  
  
 **Metadatenkonvertierung**  
  
 Beim Vergleichen der Metadaten vor und nach der Konvertierung werden Sie feststellen, dass Metadaten in JSON konvertiert wurden, wobei redundante Definitionen entfernt wurden.  
  
 Das Modell bietet weiterhin alle Funktionen. Datenbindungen, Partitionsslices, Ausdrücke, Objektbezeichner, Objektnamen, Beschreibungen, Beschriftungen, Übersetzungen und Anmerkungen sind intakt. Wenn Sie jedoch Code oder Skripts mit Verweisen auf bestimmte Objekte haben, besteht ein Teil der Umgestaltung des Codes im Entfernen der Verweise auf nicht mehr vorhandene Objekte. Ein Modell des Typs 1050 oder 1103 enthält beispielsweise Abschnitte für Dimensionen, die sich außerhalb des Cubes befinden, während ein Modell des Typs 1200 eine Tabelle als einzelnes Objekt definiert.  
  
> [!NOTE]  
>  Ältere tabellarische Kompatibilitätsgrade wie 1050 und 1103 werden unterstützt, sind aber veraltet. In künftigen Versionen von SQL Server werden tabellarische Modelle, die in mehrdimensionale Objekte umgewandelt werden, nicht mehr unterstützt. Die entsprechenden Ankündigung finden Sie unter [Veraltete Analysis Services-Funktionen in SQL Server 2016](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md) .  
  
## <a name="post-upgrade-for-tabular-models-at-1200-compatibilitylevel"></a>Aufgaben nach dem Upgrade tabellarischer Modelle auf Kompatibilitätsgrad 1200  
 Nachdem das Modell konvertiert wurde, verwenden Sie TMSL statt XMLA zum Schreiben von Skripts für Datenbankvorgänge. Näheres dazu finden Sie unter [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md). TMSL wird in SSMS automatisch generiert, wenn das Modell 1200 ist. Benutzerdefinierter Code für tabellarische Datenbanken des Typs 1200 müssen die im Namespace „Microsoft.AnalysisServces.Tabular“ definierte API verwenden. Skripts und Code müssen neu geschrieben werden. Es gibt keinen Mechanismus für eine integrierte Konvertierung. Weitere Informationen finden Sie in der [Dokumentation für Analysis Services-Entwickler](../../analysis-services/analysis-services-developer-documentation.md) .  
  
 Sie können einem tabellarischen Modell auch die folgenden Features hinzufügen, die nur vom Kompatibilitätsgrad 1200 unterstützt werden:  
  
-   Ein DirectQuery-Implementierung, die Sicherheit auf Zeilenebene über DAX im Modell, weitere Datenquellen, Teilmengen von Daten für Modellierungszwecke und eine einfachere Konfiguration unterstützt.  
  
-   Berechnete Spalten  
  
-   Anzeigeordner  
  
## <a name="upgrade-tabular-models-in-directquery-mode"></a>Upgrade von tabellarischen Modellen im DirectQuery-Modus  
 Ein direktes Upgrade älterer tabellarischer Modelle, die für DirectQuery konfiguriert sind, ist nicht möglich. Die neue Implementierung von DirectQuery hat eine kleinere Konfiguration, und nicht alle Einstellungen können portiert werden.  
  
1.  Deaktivieren Sie in SSDT den **DirectQuery** -Modus, damit das Modell In-Memory-Speicherplatz verwendet. Anweisungen dazu finden Sie unter [Aktivieren des DirectQuery-Entwurfsmodus (SSAS – tabellarisch)](https://msdn.microsoft.com/library/hh270245.aspx) .  
  
2.  Legen Sie **CompatibilityLevel** auf „SQL Server 2016 (RTM) 1200“ fest.  
  
3.  Speichern Sie das Modell, um es erneut zu erstellen oder bereitzustellen.  
  
4.  Aktivieren Sie **DirectQuery** erneut. Weitere Informationen finden Sie unter [DirectQuery für tabellarische 1200-Modelle](http://msdn.microsoft.com/library/4227977e-7368-4d45-b78f-24076882e7a8) .  
  
## <a name="see-also"></a>Siehe auch  
 [DirectQuery-Modus &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Neuigkeiten in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [Planen einer SQL Server-Installation](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Upgraden von PowerPivot für SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Installieren von Analysis Services im mehrdimensionalen Modus und im Data Mining-Modus](http://msdn.microsoft.com/library/8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60)   
 [Aktualisieren auf SQL Server 2016 mithilfe des Installations-Assistenten &#40;Setup&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  

