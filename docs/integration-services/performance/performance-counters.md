---
title: Leistungsindikatoren | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/27/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [Integration Services], performance counters
- performance counters [Integration Services]
- data flow [Integration Services], performance
- counters [Integration Services]
- data flow engine [Integration Services]
ms.assetid: 11e17f4e-72ed-44d7-a71d-a68937a78e4c
caps.latest.revision: "63"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1906bfa062b4c38c00c708bbbb9d09cbf0612071
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="performance-counters"></a>Performance Counters
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installiert eine Reihe von Leistungsindikatoren, mit denen Sie die Leistung des Datenflussmoduls überwachen können. Sie können beispielsweise den Indikator "Gespoolte Puffer" überwachen, um zu bestimmen, ob Datenpuffer vorübergehend auf den Datenträger geschrieben werden, während ein Paket ausgeführt wird. Diese Auslagerung reduziert die Leistung und weist darauf hin, dass der Computer nicht genügend Arbeitsspeicher hat.  
  
> **HINWEIS:** Wenn Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf einem Computer installieren, auf dem [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]ausgeführt wird, und anschließend ein Upgrade des betreffenden Computers auf [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]ausführen, werden beim Upgradeprozess die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Leistungsindikatoren vom Computer entfernt. Zum Wiederherstellen der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Leistungsindikatoren auf dem Computer führen Sie Setup von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Reparaturmodus aus.  
  
 In der folgenden Tabelle sind diese Leistungsindikatoren beschrieben.  
  
|Leistungsindikator|Description|  
|-------------------------|-----------------|  
|Gelesene BLOB-Bytes|Die Anzahl der Bytes der BLOB-Daten (Binary Large Object), die das Datenflussmodul in allen Datenquellen gelesen hat.|  
|Geschriebene BLOB-Bytes|Die Anzahl der Bytes der BLOB-Daten (Binary Large Object), die das Datenflussmodul in alle Ziele geschrieben hat.|  
|Verwendete BLOB-Dateien|Die Anzahl von BLOB-Dateien, die das Datenflussmodul zurzeit zum Spoolen verwendet.|  
|Pufferspeicher|Die zurzeit verwendete Arbeitsspeichermenge. Hier kann sowohl der physische als auch der virtuelle Speicher enthalten sein. Wenn diese Zahl den physischen Speicher übersteigt, vergrößert sich der Wert für **Gespoolte Puffer** , um anzuzeigen, dass Speicherauslagerungsvorgänge zunehmen. Umfangreiche Speicherauslagerungsvorgänge beeinträchtigen die Leistung des Datenflussmoduls.|  
|Verwendete Puffer|Die Anzahl von Pufferobjekten aller Typen, die alle Datenflusskomponenten und das Datenflussmodul zurzeit verwenden.|  
|Gespoolte Puffer|Der Anzahl von zurzeit auf den Datenträger geschriebenen Puffern. Wenn dem Datenflussmodul nur wenig physischer Speicher zur Verfügung steht, werden die Puffer, die zurzeit nicht verwendet werden, auf den Datenträger geschrieben und anschließend, falls erforderlich, neu geladen.|  
|Flatpufferspeicher|Die Gesamtanzahl der Bytes des Speichers, der von allen Flatpuffern verwendet wird. Als Flatpuffer werden Speicherblöcke bezeichnet, die von einer Komponente zum Speichern von Daten verwendet werden. Ein Flatpuffer ist ein großer Byteblock, auf den byteweise zugegriffen wird (also ein Byte nach dem anderen).|  
|Verwendete Flatpuffer|Die Anzahl der vom Datenflussmodul verwendeten Flatpuffer. Alle Flatpuffer sind private Puffer.|  
|Privater Pufferspeicher|Der Gesamtspeicher, der von allen privaten Puffern verwendet wird. Ein Puffer ist nicht privat, wenn das Datenflussmodul ihn zur Unterstützung des Datenflusses erstellt. Ein Puffer wird als privat bezeichnet, wenn er von einer Transformation für temporäre Arbeitsvorgänge verwendet wird. Private Puffer werden beispielsweise von der Aggregationstransformation verwendet.|  
|Private verwendete Puffer|Die Anzahl der von Transformationen verwendeten Puffer.|  
|Gelesene Zeilen|Die Anzahl der Zeilen, die von einer Quelle erstellt werden. In dieser Anzahl sind die von der Transformation für Suche aus Verweistabellen gelesenen Zeilen nicht enthalten.|  
|Geschriebene Zeilen|Die Anzahl der Zeilen, die für ein Ziel verfügbar gemacht werden. In dieser Anzahl sind die in den Zieldatenspeicher geschriebenen Zeilen nicht enthalten.|  
  
 Verwenden Sie das Leistungs-Snap-In von Microsoft Management Console (MMC), um ein Protokoll zu erstellen, in dem die Leistungsindikatoren aufgezeichnet werden.  
  
 Weitere Informationen zur Verbesserung der Leistung finden Sie unter [Funktionen für die Datenflussleistung](../../integration-services/data-flow/data-flow-performance-features.md).  
  
## <a name="obtain-performance-counter-statistics"></a>Abrufen von Leistungsindikatorstatistiken  
 Für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekte, die auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Server bereitgestellt werden, können Sie Leistungsindikatorstatistiken mithilfe der Funktion [dm_execution_performance_counters &#40;SSISDB-Datenbank&#41;](../../integration-services/functions-dm-execution-performance-counters.md) abrufen.  
  
 Im folgenden Beispiel gibt die Funktion Statistiken für eine aktive Ausführung mit einer ID von 34 zurück.  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (34)  
```  
  
 Im folgenden Beispiel gibt die Funktion Statistiken für alle Ausführungen zurück, die auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server ausgeführt werden.  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (NULL)  
  
```  
  
> **WICHTIG!** Wenn Sie ein Mitglied der **ssis_admin** -Datenbankrolle sind, werden Leistungsstatistiken für alle aktiven Ausführungen zurückgegeben.  Wenn Sie kein Mitglied der **ssis_admin** -Datenbankrolle sind, werden Leistungsstatistiken zu den aktiven Ausführungen zurückgegeben, für die Sie Leseberechtigungen haben.  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   Tool, [SSIS Performance Visualization für Business Intelligence Development Studio (CodePlex-Projekt)](http://go.microsoft.com/fwlink/?LinkId=146626)auf codeplex.com.  
  
-   Video [Messen und Verstehen der Leistung der SSIS-Pakete in Enterprise (SQL Server-Video)](http://go.microsoft.com/fwlink/?LinkId=150497)auf msdn.microsoft.com.  
  
-   Supportartikel [Der SSIS-Leistungsindikator ist im Systemmonitor nicht mehr verfügbar, wenn Sie ein Upgrade auf Windows Server 2008 ausführen](http://go.microsoft.com/fwlink/?LinkId=235319)auf support.microsoft.com.  

## <a name="add-a-log-for-data-flow-performance-counters"></a>Hinzufügen eines Protokolls für Datenfluss-Leistungsindikatoren
  In diesem Verfahren wird beschrieben, wie ein Protokoll für die vom Datenflussmodul bereitgestellten Leistungsindikatoren hinzugefügt wird.  
  
> [!NOTE]  
>  Wenn Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf einem Computer installieren, auf dem [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]ausgeführt wird, und anschließend ein Upgrade des betreffenden Computers auf [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]ausführen, werden beim Upgradeprozess die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Leistungsindikatoren vom Computer entfernt. Zum Wiederherstellen der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Leistungsindikatoren auf dem Computer führen Sie Setup von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Reparaturmodus aus.  
  
### <a name="to-add-logging-of-performance-counters"></a>So fügen Sie die Protokollierung von Leistungsindikatoren hinzu  
  
1.  Wenn Sie die klassische Ansicht verwenden, klicken Sie in der **Systemsteuerung**auf **Verwaltung**. Wenn Sie die Kategorieansicht verwenden, klicken Sie auf **Leistung und Wartung** und dann auf **Verwaltung**.  
  
2.  Klicken Sie auf **Leistung**.  
  
3.  Erweitern Sie im Dialogfeld **Leistung** die Option **Leistungsdatenprotokolle und Warnungen**, klicken Sie mit der rechten Maustaste auf **Leistungsindikatorenprotokolle**, und klicken Sie dann auf **Neue Protokolleinstellungen**. Geben Sie den Namen des Protokolls ein. Geben Sie z. B. **MeinProtokoll**ein.  
  
4.  Klicken Sie auf **OK**.  
  
5.  Klicken Sie im Dialogfeld **MeinProtokoll** auf **Indikatoren hinzufügen**.  
  
6.  Klicken Sie auf **Lokale Leistungsindikatoren verwenden** , um die Leistungsindikatoren auf dem lokalen Computer zu protokollieren. Oder klicken Sie auf **Leistungsindikatoren auswählen von:** , und wählen Sie dann einen Computer aus der Liste aus, um die Leistungsindikatoren auf dem angegebenen Computer zu protokollieren.  
  
7.  Wählen Sie im Dialogfeld **Indikatoren hinzufügen** die Option **SQLServer:SSIS-Pipeline** aus der Liste **Leistungsobjekt** aus.  
  
8.  Gehen Sie zur Auswahl von Leistungsindikatoren wie folgt vor:  
  
    -   Wählen Sie **Alle Indikatoren** , um alle Leistungsindikatoren zu protokollieren.  
  
    -   Wählen Sie **Indikatoren aus Liste auswählen** , und wählen Sie die zu verwendenden Leistungsindikatoren aus.  
  
9. Klicken Sie auf **Hinzufügen**.  
  
10. Klicken Sie auf **Schließen**.  
  
11. Prüfen Sie im Dialogfeld **MeinProtokoll** die Liste **Indikatoren** mit den protokollierten Leistungsindikatoren.  
  
12. Um weitere Indikatoren hinzuzufügen, wiederholen Sie die Schritte 5 bis 10.  
  
13. Klicken Sie auf **OK**.  
  
    > [!NOTE]  
    >  Sie müssen den Dienst Leistungsprotokolle und Warnungen mithilfe eines lokalen Kontos oder eines Domänenkontos starten, das Mitglied der Administratorengruppe ist.  

## <a name="see-also"></a>Siehe auch  
 [Ausführung von Projekten und Paketen](../packages/run-integration-services-ssis-packages.md) [Durch ein Integration Services-Paket protokollierte Ereignisse](../../integration-services/performance/events-logged-by-an-integration-services-package.md)  
