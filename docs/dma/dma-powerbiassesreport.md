---
title: "Bericht über die konsolidierten Bewertungen mithilfe von Power BI (SQL Server Data Migration Assistant) | Microsoft Docs"
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords: Data Migration Assistant, Assess
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 62f3ed0802a0a7570109bdae99151c8c6ce4fa01
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="report-on-your-consolidated-assessments-by-using-power-bi-data-migration-assistant"></a>Bericht über die konsolidierten Bewertungen mithilfe von Power BI (Data Migration Assistant)

Dieser Artikel beschreibt, wie Power BI-Berichten für konsolidierte Migrations-Bewertungen zu erstellen.

Informationen zum Konsolidieren von Bewertungen Migration mithilfe des Migrations-Assistenten für Daten, finden Sie unter [Bewertungsberichte konsolidieren](../dma/dma-consolidatereports.md).

## <a name="sample-power-bi-reports"></a>Beispiel-Power BI-Berichten

Sie können Beispiele für Power BI-Berichten für konsolidierte Migrations-Bewertungen aus diesem [Github-Repository](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant).

Die folgenden Berichte sind enthalten: 

- [Dashboard](#dashboard--details)

  Enthält Statistiken Momentaufnahme und einen Drilldown-Bericht.

- [Lokaler upgrade Bereitschaft](#on-premises-upgrade-readiness--details)

  Die Datenquelle ist die UpgradeSuccessRanking-Ansicht in der Datenbank DMAReporting.  Dieser Bericht zeigt den Erfolg der Prozentsatz Upgrade für Ihre Datenbanken bewerteten.

- [Lokaler Funktionsparität](#on-premise-feature-parity--details)

  Zeigt die Funktion Empfehlungen für die SQL Server-Zielversion.

- [Upgradebereitschaft der Azure SQL-Datenbank](#azure-sql-db-upgrade-readiness--details)

  Die Datenquelle ist die UpgradeSuccessRanking-Ansicht in der Datenbank DMAReporting.  Dieser Bericht zeigt den Prozentsatz Upgrade Erfolg für Datenbanken, die für Azure SQL-Datenbank-Migrationen bewertet.

- [Azure SQL-Datenbank nicht unterstützte Funktionen](#azure-sql-db-unsupported-features--details)

  Zeigt Funktionen in Ihre vorhandenen Datenbanken, die in Azure SQL-Datenbank (V12) nicht unterstützt werden.

Sie können diese Berichte sind durch Ändern der Datenquelle in Power BI mit Ihrer Umgebung arbeiten. 

1. Wählen Sie den Pfeil nach unten neben **Abfragen bearbeiten**, und wählen Sie **datenquelleneinstellungen**.

   ![Bearbeiten von Abfragen im Menü datenquelleneinstellungen](../dma/media/DataSourceSettings.png)

1. Wählen Sie **Datenquelle ändern...** , und geben Sie die Server- und -Werte.

   ![Ändern der Quelle, Server und Datenbank](../dma/media/ChangeSource.png)

1. Wählen Sie **OK**, und wählen Sie dann **schließen**.

1. Aktualisieren Sie Ihre Berichte.

   ![Aktualisieren von Power BI-Bericht](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>Dashboardbericht

![Dashboardbericht](../dma/media/DashboardReport.png)

Das Dashboard zeigt Details aller Ihrer Einschätzung. Sie können die Slicer auf der linken Seite verwenden, um von Instanz oder Datenbank zu filtern. Sie können das Balkendiagramm verwenden, um einen Drilldown in bestimmte Kategorien, um festzustellen, wo die Probleme liegen.

Um einen Drilldown ausführen möchten, wählen Sie den Kreis mit dem Pfeil nach unten der oberen rechten Ecke des Balkendiagramms.

![Kategorie Drilldownaktion](../dma/media/CategoryDrillDown.png)

Die Drilldown-Sequenz wird festgelegt, wie in der folgenden Abbildung gezeigt (unter **Achse**). Um die Reihenfolge zu ändern, ziehen Sie Spalten in die gewünschte Reihenfolge.

![Visualisierungen Balkendiagramm Achse](../dma/media/VisualizationsAxis.png)

In dieser Ansicht wird noch leistungsfähiger, wenn Sie zuerst nach einer bestimmten Datenbank filtern und dann einen zum bestimmten Kategorie Probleme Drilldown. Im folgenden Beispiel ist die HR-Datenbank für die Instanz ausgewählt **SQL01** zur Anzeige aller Objekte, die Migrationen (wichtige Änderungen) verhindern.

![Wichtige Änderungen für Personaldatenbank](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>Lokaler upgrade Bericht "Testfallbereitschaft"

![Lokaler upgrade Bericht "Testfallbereitschaft"](../dma/media/OnPremisesUpgradeReadinessReport.png)

Dieser Bericht enthält eine Momentaufnahme Ihrer Datenbanken wie bereit sind, um auf eine höhere Version von SQL Server zu migrieren. Die Daten in diesem Bericht stammen aus das "Dbo". UpgradeSuccessFactor\_lokale Ansicht in der Datenbank DMAReporting.

Filtern nach Instanz und Datenbankname und die Bewertung Karten oben verwenden, können Sie feststellen, welcher Version die Datenbank zu migriert werden konnte. Z. B. Wenn Sie von der Datenbank AdventureWorks 2012 filtern, können Sie sehen, dass die Datenbank bereit, um für alle SQL Server-Versionen, die im Bericht aufgeführten wechseln. Dies wird bestimmt, indem Sie sicherstellen, dass es sind keine aktuellen Änderungen für diese Datenbank und die Kompatibilität Hierarchieebene.

![Upgrade Erfolgsfaktor für AdventureWorks-Datenbank](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>Lokaler feature Parität-Bericht

![Lokaler feature Parität-Bericht](../dma/media/OnPremisesFeatureParityReport.png)

Verwenden Sie diesen Bericht, um neue Funktionen zu markieren, die für die Datenbank in SQL Server-Zielversion verwendet werden kann.

Bei Auswahl eine Funktion in das Trichterdiagramm werden die Daten im unteren Bereich hervorgehoben, welche Objekte von der Funktion betroffen sind. Im folgenden Beispiel die **Stretch-Datenbank für speichereinsparungen** Funktion ausgewählt ist, und eine Tabelle ist aufgeführt, die von dieser Funktion profitieren könnten.

![Feature-Empfehlung für Stretch-Datenbank](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Upgrade bereitschaftsbericht für Azure SQL-Datenbank

![Upgrade bereitschaftsbericht für Azure SQL-Datenbank](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

Dieser Bericht zeigt die Datenbank-Bereitschaft zum Migrieren zu Azure SQL-Datenbank V12. Die Daten aus diesem Bericht stammen aus das "Dbo". In der Datenbank DMAReporting UpgradeSuccessRanking-Sicht.

### <a name="azure-features-parity-report"></a>Azure-Funktionen Parität Bericht

![Azure-Funktionen Parität Bericht](../dma/media/AzureFeaturesParityReport.png)

Verwenden Sie diesen Bericht zum Hervorheben der *Ebene Instanzfunktionen* , werden von Azure SQL-Datenbank V12 nicht unterstützt.

Bei Auswahl eine Funktion in das Trichterdiagramm enthält die Daten im unteren Bereich der Instanzen und Funktionen, die nicht unterstützt werden. Im folgenden Beispiel wird diese Funktion aktiviert: **Always on-verfügbarkeitsgruppenkonfiguration in Azure SQL-Datenbank nicht unterstützt**.  

![AlwaysOn Availability Group-Funktion](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Bericht zur Azure SQL-Datenbank nicht unterstützte Funktionen

![Bericht zur Azure SQL-Datenbank nicht unterstützte Funktionen](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

Dieser Bericht hebt hervor, welche Funktionen nicht unterstützt werden, für einen bestimmten **Datenbank** das Ziel ist bei Azure SQL-Datenbank (V12).

Durch das Filtern von der Datenbank produktmodellname und Funktion den Wert in das Trichterdiagramm, sehen Sie die Details auf die nicht unterstützte Funktion. Details enthalten, welches Objekt betroffen ist und Empfehlungen für das Problem.

Z. B. das Filtern nach der DTC-Datenbank und **schreibgeschützte Datenbanken können nicht aktualisiert werden**, sehen Sie eine Liste von Objekten, die betroffen sind.

![Schreibgeschützte Datenbanken nicht aktualisiert Problem](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>Siehe auch

[Übersicht über Data-Migrations-Assistenten](../dma/dma-overview.md)

[Migration Assistant herunterladen von Daten](https://www.microsoft.com/download/details.aspx?id=53595)

[Power BI-download](https://powerbi.microsoft.com/)
