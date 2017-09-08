---
title: Power Pivot-Management-Dashboard und Verwendungsdaten | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 541c8b1f-c6c2-423d-a97d-65c379967e0c
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5833c1dae2cc6b5cf8f85a52bec088d96e609537
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="power-pivot-management-dashboard-and-usage-data"></a>PowerPivot-Management-Dashboard und Verwendungsdaten
  [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Management-Dashboard ist eine Sammlung vordefinierter Berichte und Webparts in der SharePoint-Zentraladministration, die Sie bei der Verwaltung einer SQL Server [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] für SharePoint-Bereitstellung unterstützen. Das Management-Dashboard bietet Informationen zum Serverstatus, zur Arbeitsmappenaktivität sowie zur Datenaktualisierung. Das Dashboard nutzt Daten aus der Sammlung von Verwendungsdaten in SharePoint.  
  
  
##  <a name="prereq"></a> Erforderliche Komponenten  
 Sie müssen Dienstadministrator sein, um das [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Management-Dashboard für eine von Ihnen verwaltete [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendung zu öffnen.  
  
##  <a name="items"></a> Übersicht über die Abschnitte des Dashboards  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Management-Dashboard enthält Webparts und eingebettete Berichte, die einen Drilldown in bestimmte Informationskategorien ermöglichen. In der folgenden Liste werden die einzelnen Bestandteile des Dashboards beschrieben:  
  
|Dashboard|Description|  
|---------------|-----------------|  
|Infrastruktur - Serverintegrität|Zeigt Trends zur CPU-Verwendung, Arbeitsspeichernutzung sowie zu Abfrageantwortzeiten im zeitlichen Verlauf an, damit Sie beurteilen können, ob die maximale Kapazität der Systemressourcen bald erreicht ist oder ob diese unterausgelastet sind.|  
|Aktionen|Enthält Links zu anderen Seiten in der Zentraladministration, darunter die aktuelle Dienstanwendung, eine Liste der Dienstanwendungen sowie die Verwendungsprotokollierung.|  
|Arbeitsmappenaktivität - Diagramm|Enthält Angaben zur Häufigkeit des Datenzugriffs. Hier können Sie erfahren, wie viele Verbindungen mit [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Datenquellen täglich oder wöchentlich hergestellt werden.|  
|Arbeitsmappenaktivität - Liste|Enthält Angaben zur Häufigkeit des Datenzugriffs. Hier können Sie erfahren, wie viele Verbindungen mit [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Datenquellen täglich oder wöchentlich hergestellt werden.|  
|Datenaktualisierung - Letzte Aktivität|Enthält Angaben zum Status von Datenaktualisierungsaufträgen, einschließlich fehlgeschlagener Aufträge. Dieser Bericht enthält eine zusammengesetzte Ansicht der Datenaktualisierungsvorgänge auf Anwendungsebene. Administratoren sehen auf einen Blick die Anzahl von Datenaktualisierungsaufträgen, die für die gesamte [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendung definiert wurden.|  
|Datenaktualisierung - Letzte Fehler|Listet die [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Arbeitsmappen auf, deren Datenaktualisierung nicht erfolgreich abgeschlossen wurde.|  
|Berichte|Enthält Links zu Berichten, die Sie in Excel öffnen können.|  
  
##  <a name="open"></a> Öffnen des PowerPivot-Management-Dashboards  
 Das Dashboard zeigt Informationen für jeweils eine [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendung an. Sie können das Management-Dashboard von zwei unterschiedlichen Orten aus öffnen.  
  
### <a name="open-the-dashboard-from-general-application-settings"></a>Öffnen des Dashboards über die allgemeinen Anwendungseinstellungen  
  
1.  Klicken Sie in der Zentraladministration in der Gruppe **Allgemeine Anwendungseinstellungen** auf **[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Management-Dashboard**.  
  
2.  Wählen Sie auf der Hauptseite die PowerPivot-Dienstanwendung aus, für die Sie Betriebsdaten anzeigen möchten.  
  
### <a name="open-the-dashboard-from-a-power-pivot-service-application"></a>Öffnen des Dashboards aus einer PowerPivot-Dienstanwendung  
  
1.  Klicken Sie in der Zentraladministration unter **Anwendungsverwaltung**auf **Dienstanwendungen verwalten**.  
  
2.  Klicken Sie auf den Namen der [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendung. Das [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Management-Dashboard zeigt operative Daten für die aktuelle Dienstanwendung an.  
  
### <a name="change-the-current-service-application"></a>Ändern Sie die aktuelle Dienstanwendung.  
 So ändern Sie die aktuelle [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendung im Management-Dashboard:  
  
1.  Notieren Sie sich den Namen der aktuellen Dienstanwendung, der im oberen Bereich des [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]-Management-Dashboards angezeigt wird, beispielsweise **[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]-Standarddienstanwendung**.  
  
2.  Klicken Sie im Dashboard **Aktionen** auf **Dienstanwendungen auflisten**.  
  
3.  Klicken Sie auf den Namen der [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendung, für die Management-Dashboard-Berichte angezeigt werden sollen.  
  
##  <a name="sourcedata"></a> Quelldaten in Dashboards  
 In Dashboards, Berichten und Webparts werden Daten aus einem internen Datenmodell angezeigt, das Daten aus den System- und [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Anwendungsdatenbanken abruft. Das interne Datenmodell ist in einer [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Arbeitsmappe eingebettet, die auf der Website der Zentraladministration gehostet wird. Das Datenmodell verfügt über eine feste Struktur. Obwohl Sie die PowerPivot-Arbeitsmappe als Datenquelle für neue Berichte verwenden können, darf die Struktur in keiner Weise geändert werden, die die vordefinierten Berichte beeinträchtigen würde, die die Struktur verwenden.  
  
 Im Folgenden finden Sie weitere Informationen dazu, wie Daten gesammelt werden:  
  
-   [Sammlung von Power Pivot-Verwendungsdaten](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)  
  
-   [Konfigurieren der Sammlung von Verwendungsdaten für Power Pivot für SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
 Achten Sie beim Sammeln von Daten zum PowerPivot-Serversystem darauf, dass für jede PowerPivot-Dienstanwendung Ereignismeldungen, Datenaktualisierungsverläufe und sonstige Verwendungsverläufe aktiviert sind. Die während des normalen Serverbetriebs gesammelten Server- und Verwendungsdaten bilden die Quelldaten, die in das interne Datenmodell übertragen werden. **Hinweis:** Wenn Sie Ereignismeldungen oder Verwendungsverläufe deaktivieren, enthalten die zusammengesetzten Berichte unvollständige oder fehlerhafte Angaben.  
  
##  <a name="edit"></a> Bearbeiten eines PowerPivot-Dashboards  
 Wenn Sie erfahren in der Dashboardentwicklung oder -anpassung sind, können Sie das Dashboard bearbeiten, um neue Webparts aufzunehmen. Sie können auch die Webparteigenschaften bearbeiten, die im Dashboard enthalten sind.  
  
##  <a name="reports"></a> Erstellen benutzerdefinierter Berichte für das PowerPivot-Management-Dashboard  
 Für Berichtszwecke werden [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Verwendungsdaten und -verlauf in einer internen [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Arbeitsmappe aufbewahrt, die zusammen mit dem Dashboard erstellt und konfiguriert wird. Wenn die Standardberichte die Informationen nicht enthalten, die Sie benötigen, können Sie benutzerdefinierte Berichte in Excel auf Grundlage der Arbeitsmappe erstellen. Sowohl die Arbeitsmappe als auch benutzerdefinierte Berichte, die Sie erstellen, bleiben erhalten, wenn Sie die [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Lösungsdateien später aktualisieren oder deinstallieren. Die Arbeitsmappe und die Berichte werden in der [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Verwaltungsbibliothek innerhalb der Website der Zentraladministration gespeichert. Diese Bibliothek ist standardmäßig nicht sichtbar. Sie können sie jedoch unter Websiteaktionen mithilfe der Aktion Alle Websiteinhalte einblenden anzeigen.  
  
 Um Ihnen den Einstieg in die benutzerdefinierte Berichterstellung zu erleichtern, bietet das [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Management-Dashboard eine ODC-Datei (Office Data Connection), über die eine Verbindung mit der Quellarbeitsmappe hergestellt werden kann. Beispielsweise können Sie die ODC-Datei in Excel verwenden, um zusätzliche Berichte zu erstellen.  
  
> [!NOTE]  
>  Bearbeiten Sie die Datei, um bei der Verwendung der ODC-Datei in Excel den folgenden Fehler zu vermeiden: "Fehler bei der Initialisierung der Datenquelle". Die automatisch generierte ODC-Datei enthält einen Parameter, der vom MSOLAP-OLE DB-Anbieter nicht unterstützt wird. Die folgenden Anweisungen stellen eine Problemumgehung zum Entfernen der Parameter bereit.  
  
 Sie müssen ein Farm- oder Dienstadministrator sein, um Berichte zu erstellen, die auf der [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Arbeitsmappe der Zentraladministration basieren.  
  
1.  Öffnen Sie das [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Management-Dashboard.  
  
2.  Führen Sie einen Bildlauf zum Abschnitt **Berichte** am unteren Rand der Seite durch.  
  
3.  Klicken Sie auf **[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Verwaltungsdaten**.  
  
4.  Speichern Sie die ODC-Datei in einem lokalen Ordner.  
  
5.  Öffnen Sie die ODC-Datei in einem Text-Editor.  
  
6.  In der  **\<ODC: ConnectionString >** -Element einen Bildlauf bis zum Ende der Zeile, und entfernen **Embedded Data = "false"**, und entfernen Sie dann **Edit Mode = 0**. Wenn das letzte Zeichen in der Zeichenfolge ein Semikolon ist, entfernen Sie es ebenfalls.  
  
7.  Speichern Sie die Datei. Die übrigen Schritte richten sich nach der verwendeten [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] - und Excel-Version.  
  
8.  1.  Starten von Excel 2013  
  
    2.  Klicken Sie im - **[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]** -Menüband auf **Verwalten**.  
  
    3.  Klicken Sie auf **Externe Daten abrufen** und dann auf **Vorhandene Verbindungen**.  
  
    4.  Klicken Sie auf die ODC-Datei, sofern sie angezeigt wird. Wenn die ODC-Datei nicht sichtbar ist, klicken Sie auf **Suche fortsetzen** und geben dann im Dateipfad die ODC-Datei an.  
  
    5.  Klicken Sie auf **Öffnen**.  
  
    6.  Klicken Sie auf **Verbindung testen** , um zu überprüfen, ob die Verbindung ordnungsgemäß arbeitet.  
  
    7.  Geben Sie einen Namen für die Verbindung ein, und klicken Sie dann auf **Weiter**.  
  
    8.  Klicken Sie im Bereich zum Angeben einer MDX-Abfrage auf **Entwerfen** , um den MDX-Abfrage-Designer zu öffnen und die Daten zusammenzustellen, mit denen Sie arbeiten möchten. **Wenn die Fehlermeldung** "Der Edit Mode-Eigenschaftsname weist das falsche Format auf" angezeigt wird, überprüfen Sie, ob die ODC-Datei ordnungsgemäß bearbeitet wurde.  
  
    9. Klicken Sie auf **OK** und dann auf **Fertig stellen**.  
  
    10. Erstellen Sie PivotTable- oder PivotChart-Berichte, um die Daten in Excel visuell darzustellen.  
  
9. 1.  Starten Sie Excel 2010.  
  
    2.  Klicken Sie im [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]-Menüband auf **[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]-Fenster starten**.  
  
    3.  Klicken Sie im Menüband „Entwurf“ im [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Fenster auf **Vorhandene Verbindungen**.  
  
    4.  Klicken Sie auf **Suche fortsetzen**.  
  
    5.  Geben Sie im Dateipfad die ODC-Datei an.  
  
    6.  Klicken Sie auf **Öffnen**. Der Tabellenimport-Assistent wird mithilfe der Verbindungszeichenfolge zur [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Arbeitsmappe, die die Verwendungsdaten enthält, gestartet.  
  
    7.  Klicken Sie auf **Verbindung testen** , um zu überprüfen, ob Sie Zugriff haben.  
  
    8.  Geben Sie einen Anzeigenamen für die Verbindung ein, und klicken Sie dann auf **Weiter**.  
  
    9. Klicken Sie im Bereich für das Angeben einer MDX-Abfrage auf **Entwurf** , um die Daten zusammenzutragen, mit denen Sie arbeiten möchten, und erstellen Sie dann PivotTable- oder PivotChart-Berichte, um die Daten in Excel visuell darzustellen.  
  
## <a name="see-also"></a>Siehe auch  
 [PowerPivot-Datenaktualisierung mit SharePoint 2010](http://msdn.microsoft.com/en-us/01b54e6f-66e5-485c-acaa-3f9aa53119c9)   
 [Konfigurieren der Sammlung von Verwendungsdaten für Power Pivot für SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
