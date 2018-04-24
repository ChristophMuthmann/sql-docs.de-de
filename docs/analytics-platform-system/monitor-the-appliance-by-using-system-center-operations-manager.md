---
title: Überwachung mit SCOM - Analyseplattformsystem | Microsoft Docs
description: Verwenden Sie System Center Operations Manager (SCOM), um die Appliance Analytics Platform System (APS) überwachen.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c2b26462ab37cf7d63960ff7db6e20c57e8290bb
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>Überwachung mit System Center Operationsmanager - Analyseplattformsystem
Verwenden Sie System Center Operations Manager (SCOM), um die Appliance Analytics Platform System (APS) überwachen.
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
  
1.  System Center Operationsmanager 2007 R2, 2012 oder 2012 SP1 muss installiert und aktiv sein.  
  
2.  SQL Server 2008 R2 Native Client oder SQL Server 2012 Native Client muss installiert sein.  
  
3.  Die Management Packs zum Überwachen von SQL Server PDW und HDInsight müssen installiert, nicht importiert und konfiguriert werden. Verwenden Sie die folgenden Artikeln für Anweisungen zum Ausführen dieser Aufgaben.  
  
    -   [Installieren Sie die SCOM-Management Packs &#40;Analyseplattformsystem&#41;](install-the-scom-management-packs.md)  
  
    -   [Importieren Sie das SCOM Management Pack für PDW &#40;Analyseplattformsystem&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [Konfigurieren von SCOM zum Überwachen von Analyseplattformsystem &#40;Analyseplattformsystem&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>Zum Überwachen von SQLServer PDW mit SCOM  
Nach dem Konfigurieren der SCOM-Management Packs, klicken Sie auf die Überwachung im Bereich von SCOM, und führen Sie einen Drilldown nach unten bis zum **SQL Server-Appliance** und dann **Microsoft SQL Server Parallel Data Warehouse**. Unter Microsoft SQL Server Parallel Data Warehouse, es gibt vier Möglichkeiten zur Auswahl: Warnungen, Einheiten, Appliance-Diagramm und Knoten.  
  
### <a name="alerts"></a>Warnungen  
Warnungen sind, wo Sie die aktuellen Warnungen verwalten erhalten.  
  
![Warnungen](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>Einheiten  
Einheiten sind, in dem Sie die derzeit ermittelt und überwacht SQL Server PDW-Geräte in Ihrer Umgebung erwarten können. Wenn ein Gerät auf der sich hier nicht angezeigt, und die ODBC-Verbindung für sie erstellt haben, klicken Sie dann möglicherweise etwas mit Ihrem Konto von PDWWatcher. Wenn sie als "nicht überwacht" angezeigt, liegt möglicherweise etwas mit Ihrem Konto PDWMonitor. Etwas Geduld, da SCOM Änderungen in Echtzeit nimmt, doch überprüft regelmäßig, neue Geräte ob überwachen, und sendet in regelmäßigen Abständen Abfragen an die Einheiten für die Überwachung.  
  
![Appliances](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>Anwendungsdiagramm  
Der Diagrammseite Einheiten ist, in dem Sie einen Blick auf die Integrität Ihrer Anwendung mit einer Strukturansicht finden können:  
  
![Anwendungsdiagramm](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>Knoten  
Schließlich können mit die Knoten-Ansicht der Integrität Ihrer Anwendung über jeden Knoten finden Sie unter:  
  
![Nodes](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>Siehe auch  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Grundlegendes zu Verwaltungskonsolenwarnungen &#40;Analyseplattformsystem&#41;](understanding-admin-console-alerts.md)  
  
