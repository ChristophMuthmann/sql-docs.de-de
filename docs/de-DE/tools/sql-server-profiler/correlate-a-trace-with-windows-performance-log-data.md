---
title: Korrelieren einer Ablaufverfolgung mit Windows-Leistungsprotokolldaten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- correlating trace with log data
- logs [SQL Server], traces
- Profiler [SQL Server Profiler], correlating trace with log data
- traces [SQL Server], logs
- SQL Server Profiler, correlating trace with log data
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9fc0474e0f3c823b2ca3fa16979e16ff5123f321
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="correlate-a-trace-with-windows-performance-log-data"></a>Korrelieren einer Ablaufverfolgung mit Windows-Leistungsprotokolldaten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] können Sie ein Microsoft Windows-Leistungsprotokoll öffnen, die Leistungsindikatoren auswählen, die Sie mit einer Ablaufverfolgung korrelieren möchten, und die ausgewählten Leistungsindikatoren zusammen mit der Ablaufverfolgung auf der grafischen Benutzeroberfläche von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] anzeigen. Wenn Sie ein Ereignis im Ablaufverfolgungsfenster auswählen, zeigt ein senkrechter roter Strich im Datenfensterbereich des Systemmonitors von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] an, welche Leistungsprotokolldaten mit dem ausgewählten Ablaufverfolgungsereignis korrelieren.  
  
 Um eine Ablaufverfolgung mit Leistungsindikatoren zu korrelieren, öffnen Sie eine Ablaufverfolgungsdatei oder -tabelle, die die Datenspalten **StartTime** und **EndTime** data columns, und then click **Datei** von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **Leistungsdaten importieren** . Anschließend können Sie das Leistungsprotokoll öffnen und die Systemmonitor-Objekte und -Leistungsindikatoren auswählen, die Sie mit der Ablaufverfolgung korrelieren möchten.  
  
### <a name="to-correlate-a-trace-with-performance-log-data"></a>So korrelieren Sie eine Ablaufverfolgung mit Leistungsprotokolldaten  
  
1.  Öffnen Sie eine Ablaufverfolgungsdatei oder -tabelle in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Ablaufverfolgungen, die noch ausgeführt werden und Ereignisdaten sammeln, können nicht korreliert werden. Um die Genauigkeit der Korrelation mit den Systemmonitordaten sicherzustellen, muss die Ablaufverfolgung die beiden Datenspalten **StartTime** und **EndTime** enthalten.  
  
2.  Klicken Sie in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **Datei** auf **Leistungsdaten importieren**.  
  
3.  Wählen Sie im Dialogfeld **Öffnen** eine Datei aus, die ein Leistungsprotokoll enthält. Die Leistungsprotokolldaten und die Ablaufverfolgungsdaten müssen im selben Zeitraum aufgezeichnet werden.  
  
4.  Aktivieren Sie im Dialogfeld zum Beschränken der **Leistungsindikatoren** die Kontrollkästchen, die den Systemmonitorobjekten und den Leistungsindikatoren entsprechen, die Sie neben der Ablaufverfolgung anzeigen möchten. Klicken Sie auf **OK.**  
  
5.  Wählen Sie im Ablaufverfolgungs-Ereignisfenster ein Ereignis aus, oder navigieren Sie in diesem Fenster mithilfe der Pfeiltasten durch mehrere benachbarte Zeilen. Der senkrechte rote Strich im Datenfenster unter **Systemmonitor** weist auf die mit dem ausgewählten Ablaufverfolgungsereignis korrelierten Leistungsprotokolldaten hin.  
  
6.  Klicken Sie im Systemmonitordiagramm auf einen Sie interessierenden Punkt. Die entsprechende Ablaufverfolgungszeile, die zeitlich am nächsten ist, wird ausgewählt. Halten Sie die linke Maustaste gedrückt, und ziehen Sie den Mauszeiger innerhalb des Systemmonitordiagramms, um einen Zeitbereich zu vergrößern.  
  
### <a name="to-create-performance-logs-that-can-be-shared-among-different-versions-of-windows"></a>So erstellen Sie Leistungsprotokolle, die in verschiedenen Windows-Versionen verwendet werden können  
  
1.  Öffnen Sie **Verwaltung**in der Systemsteuerung, und doppelklicken Sie dann auf **Leistung**.  
  
2.  Erweitern Sie im Dialogfeld **Leistung** die Option **Leistungsdatenprotokolle und Warnungen**, klicken Sie mit der rechten Maustaste auf **Leistungsindikatorenprotokolle**, und klicken Sie dann auf **Neue Protokolleinstellungen**.  
  
3.  Geben Sie einen Namen für das Leistungsindikatorenprotokoll ein, und klicken Sie dann auf **OK**.  
  
4.  Klicken Sie auf der Registerkarte **Allgemein** auf **Indikatoren hinzufügen**.  
  
5.  Wählen Sie in der Liste **Leistungsobjekt** das Leistungsobjekt aus, das Sie überwachen möchten. Die Namen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Leistungsobjekte für Standardinstanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beginnen mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , benannte Instanzen beginnen mit MSSQL$*instanceName*.  
  
6.  Fügen Sie Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz die benötigte Anzahl an Leistungsindikatoren und andere wichtige Werte, wie z. B. die Prozessorzeit und die Datenträgerzeit, hinzu.  
  
7.  Wenn Sie alle gewünschten Leistungsindikatoren hinzugefügt haben, klicken Sie auf **Schließen**.  
  
8.  Legen Sie Werte für das Intervall **Daten erfassen alle** fest. Beginnen Sie mit einem mittleren Stichprobenintervall, beispielsweise 5 Minuten, und passen Sie es dann bei Bedarf an.  
  
9. Wählen Sie auf der Registerkarte **Protokolldateien** in der Liste **Protokolldateityp** die Option **Textdatei (durch Trennzeichen getrennt)** aus. Durch Trennzeichen getrennte Textprotokolldateien können in verschiedenen Windows-Versionen freigegeben und später in Berichtstools, wie z. B. Microsoft Excel, angezeigt werden.  
  
10. Geben Sie auf der Registerkarte **Zeitplan** einen Zeitplan für die Überwachung an.  
  
11. Klicken Sie auf **OK** , um das Leistungsprotokoll zu erstellen.  
