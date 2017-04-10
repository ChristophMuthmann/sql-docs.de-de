---
title: "Verwenden von sqlBindR.exe zum Aktualisieren einer Instanz von R Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server (starting with 2016 CTP3)"
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# Verwenden von sqlBindR.exe zum Aktualisieren einer Instanz von R Services
Microsoft R Server für Windows enthält ein neues Tool namens **SqlBindR.exe**, mit dem die R-Komponenten für eine Instanz aktualisiert werden können. Dieser Vorgang wird als **Bindung** bezeichnet, da durch ihn das Lizenzierungsmodell einer SQL Server 2016-Instanz dahingehend geändert wird, dass sie die neue Microsoft Modern Software Lifecycle Support-Lizenz verwendet.

Dieses Lizenzierungssystem stellt allgemein sicher, dass Ihre Datenanalysten stets die neueste Version von R verwenden. Weitere Informationen über die Bedingungen und Vorteile der Microsoft-Softwarelizenz finden Sie unter [Run Microsoft R Server for Windows (Ausführen von Microsoft R Server für Windows)](https://msdnstage.redmond.corp.microsoft.com/en-us/microsoft-r/rserver-install-windows?branch=r-server-nov16-dev).

Wenn Sie eine Instanz binden, passieren drei Dinge:
+ Die Supportrichtlinie für die Instanz wird von der SQL Server 2016-Support-Richtlinie in den neuen Microsoft Modern Software License-Vertrag geändert.
+ Die zu dieser Instanz gehörenden R-Komponenten werden automatisch mit jeder Version aktualisiert, und zwar im Gleichschritt mit der aktuellen R Server-Version unter den neuen Modern Software License-Bedingungen.
+ Die Instanz kann nicht mehr manuell aktualisiert werden, außer wenn Sie neue Pakete hinzufügen. 

Wenn Sie zu einem späteren Zeitpunkt die Instanz nicht mehr mit jeder neuen Version aktualisieren lassen möchten, müssen Sie die **Bindung** der Instanz aufheben und dann Microsoft R Server-Komponenten so deinstallieren, wie es in folgendem Artikel beschrieben wird: [Run Microsoft R Server for Windows (Ausführen von Microsoft R Server für Windows)](https://msdn.microsoft.com/microsoft-r/rserver-install-windows). Wenn dieser Prozess abgeschlossen ist, wirken sich zukünftige Upgrades von R Server nicht mehr auf die Instanz aus.

> [!NOTE] Der Upgradevorgang wird nur für Instanzen von SQL Server 2016 unterstützt, die mit dem kumulativen Update 3.0 gepatcht wurden.  
> 
> Wenn Sie R Services in SQL Server vNext verwenden, müssen Sie dieses Upgrade nicht anwenden. R-Komponenten werden bei jedem Meilenstein stets automatisch aktualisiert.

## <a name="how-to-upgrade-an-instance"></a>Gewusst wie: Aktualisieren einer Instanz


1. Führen Sie das Installationsprogramm für Microsoft R Server auf dem Computer aus, auf dem sich die zu aktualisierende Instanz befindet.
2. Suchen Sie nach Abschluss der Installation den Ordner mit dem Tool **SqlBindR.exe**. Der Standardspeicherort lautet: `C:\Program Files\Microsoft\R Server\Setup`.
2. Öffnen Sie eine Eingabeaufforderung als Administrator.
3. Geben Sie den folgenden Befehl ein, um eine Liste der verfügbaren Instanzen anzuzeigen: `SqlBindR.exe /list`
4. Führen Sie den Befehl **SqlBindR.exe** mit dem */bind*-Argument aus, um den Namen der zu aktualisierenden Instanz anzugeben. 
   Geben Sie beispielsweise Folgendes ein, um nur die Standardinstanz zu aktualisieren:  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

## <a name="how-to-downgrade-an-instance-of-r-services"></a>Herunterstufen einer Instanz von R Services

Um den Status einer Instanz wiederherzustellen, müssen Sie das SqlBindR-Tool ausführen, um die Lizenzierung zu entfernen, und anschließend die Instanz reparieren bzw. neu installieren.

1. Führen Sie den Befehl **SqlBindR.exe** mit dem */unbind*-Argument aus, und geben Sie die Instanz an. 
   Der folgende Befehl setzt beispielsweise die Standardinstanz wieder auf die SQL Server-Lizenzierung und den SQL Server-Aktualisierungszeitplan zurück:  `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`
2. Stellen Sie den ursprünglichen Zustand der Instanz wieder her, indem Sie eine der folgenden Maßnahmen durchführen:
    + Reparieren Sie die Instanz. Der Reparaturvorgang wendet Aktualisierungen auf alle installierten Funktionen an.
    + Führen Sie eine Deinstallation und eine anschließende Neuinstallation durch, um alle Service-Versionen anzuwenden. Die Instanz muss neu gestartet werden.
3. Nachdem R Server entfernt wurde, werden alle mit der Instanz installierten Pakete ebenfalls entfernt und müssen daher neu installiert werden.

## <a name="requirements"></a>Anforderungen
Die Aktualisierung wird nur für Instanzen von SQL Server 2016 unterstützt, die die folgenden Anforderungen erfüllen:
+ SQL Server 2016 SP1 oder höher
+ Kumulatives Update 3.0 (OD) wurde angewandt

Das aktuelle Upgrade wird derzeit nur mithilfe des Befehlszeilenprogramms unterstützt. Eine interaktive Schnittstelle wird in einer späteren Version bereitgestellt werden.

## <a name="sqlbindrexe-command-syntax"></a>sqlbindr.exe-Befehlssyntax


### <a name="usage"></a>Verwendung

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parameter

|Name|Description|
|------|------|
|*list*| Zeigt eine Liste aller SQL-Datenbankinstanz-IDs auf dem aktuellen Computer an|
|*bind*| Aktualisiert die angegebene SQL-Datenbankinstanz auf die neueste Version von R Server und stellt sicher, dass die Instanz automatisch zukünftige Upgrades von R Server erhält|
|*unbind*|Die neueste Version von R Server wird auf der angegebenen SQL-Datenbankinstanz deinstalliert, und es wird verhindert, dass zukünftige R Server-Upgrades auf die Instanz angewandt werden|

### <a name="errors"></a>Fehler

Die Abfrage gibt die folgenden Fehlermeldungen zurück:

|Fehler|Lösung|
|------|------|
|Fehler beim Binden der Instanz| Die Instanz konnte nicht gebunden werden. Wenden Sie sich an den Support, um Unterstützung zu erhalten.|
|Die Instanz ist bereits gebunden| Sie haben den *bind*-Befehl ausgeführt, die angegebene Instanz ist aber bereits gebunden. Wählen Sie eine andere Instanz.|
|Die Instanz ist nicht gebunden| Sie haben den *unbind*-Befehl ausgeführt, die angegebene Instanz ist aber nicht gebunden. Wählen Sie eine andere Instanz.|
|Keine gültige SQL-Instanz-ID| Möglicherweise haben Sie den Namen der Instanz falsch eingegeben. Führen Sie den Befehl erneut mit dem *list*-Argument aus, um die verfügbaren Instanz-IDs zu sehen.|
|Keine Instanzen gefunden| Auf diesem Computer befindet sich keine Instanz von SQL Server R Services.|
|In der Instanz muss eine kompatible Version von SQL R Services (In-Database) installiert sein.| Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?linkid=835761.|
|Fehler beim Aufheben der Bindung der Instanz| Die Bindung der Instanz konnte nicht aufgehoben werden. Wenden Sie sich an den Support, um Unterstützung zu erhalten.|
|Unerwarteter Fehler aufgetreten| Andere Fehler. Wenden Sie sich an den Support, um Unterstützung zu erhalten.  |
|Keine SQL-Instanzen gefunden| Auf diesem Computer befindet sich keine Instanz von SQL Server. |


## <a name="see-also"></a>Siehe auch

[SQL Server Release Notes (Versionshinweise für SQL Server)](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes)
