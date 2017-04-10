---
title: "Korrelieren einer Ablaufverfolgung mit Windows-Leistungsprotokolldaten (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Ablaufverfolgungen [SQL Server], Protokolle"
ms.assetid: e1b3072c-8daf-49a7-9895-c8cccd2adb95
caps.latest.revision: 32
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 32
---
# Korrelieren einer Ablaufverfolgung mit Windows-Leistungsprotokolldaten (SQL Server Profiler)
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] kann Microsoft Windows-Systemmonit- oder-Leistungsindikat- oderen mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Ereignissen in Beziehung setzen. Der Windows-Systemmonitor protokolliert die Systemaktivität für angegebene Leistungsindikatoren in Leistungsprotokollen.  
  
> [!NOTE]  
>  Informationen zur gemeinsamen Nutzung von Protokollen in verschiedenen Windows-Versionen finden Sie am Ende dieses Themas.  
  
### So korrelieren Sie eine Ablaufverfolgung mit Leistungsprotokolldaten  
  
1.  Öffnen Sie eine Ablaufverfolgungsdatei oder -tabelle in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Ablaufverfolgungen, die noch ausgeführt werden und Ereignisdaten sammeln, können nicht korreliert werden. Um die Genauigkeit der Korrelation mit den Systemmonitordaten sicherzustellen, muss die Ablaufverfolgung die beiden Datenspalten **StartTime** und **EndTime** enthalten.  
  
2.  Klicken Sie in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **Datei** auf **Leistungsdaten importieren**.  
  
3.  Wählen Sie im Dialogfeld **Öffnen** eine Datei aus, die ein Leistungsprotokoll enthält. Die Leistungsprotokolldaten und die Ablaufverfolgungsdaten müssen im selben Zeitraum aufgezeichnet werden.  
  
4.  Aktivieren Sie im Dialogfeld zum Beschränken der Leistungsindikatoren **** die Kontrollkästchen, die den Systemmonitorobjekten und den Leistungsindikatoren entsprechen, die Sie neben der Ablaufverfolgung anzeigen möchten. Klicken Sie auf **OK.**  
  
5.  Wählen Sie im Ablaufverfolgungs-Ereignisfenster ein Ereignis aus, oder navigieren Sie in diesem Fenster mithilfe der Pfeiltasten durch mehrere benachbarte Zeilen. Der senkrechte rote Strich im Datenfenster unter **Systemmonitor** weist auf die mit dem ausgewählten Ablaufverfolgungsereignis korrelierten Leistungsprotokolldaten hin.  
  
6.  Klicken Sie im Systemmonitordiagramm auf einen Sie interessierenden Punkt. Die entsprechende Ablaufverfolgungszeile, die zeitlich am nächsten ist, wird ausgewählt. Halten Sie die linke Maustaste gedrückt, und ziehen Sie den Mauszeiger innerhalb des Systemmonitordiagramms, um einen Zeitbereich zu vergrößern.  
  
### So erstellen Sie Leistungsprotokolle, die in verschiedenen Windows-Versionen verwendet werden können  
  
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
  
## Siehe auch  
 [Vorlagen und Berechtigungen in SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [Starten von SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md)  
  
  