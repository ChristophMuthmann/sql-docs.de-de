---
title: 'Schritt 1: Herunterladen der Beispieldaten | Microsoft Docs'
ms.custom: 
ms.date: 10/17/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: b4b9aeed6b56e70c3af0c29f5bc0b6844f0a6f18
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="step-1-download-the-sample-data"></a>Schritt 1: Herunterladen der Beispieldaten

Dieser Artikel ist Teil eines Lernprogramms [In Datenbank-Python-Analyse für SQL-Entwickler](sqldev-in-database-python-for-sql-developers.md). 

Die Daten und die Skripts in diesem Lernprogramm werden auf Github gemeinsam genutzt. In diesem Schritt verwenden Sie ein PowerShell-Skript zum Herunterladen der Daten und Skript-Dateien in ein lokales Verzeichnis Ihrer Wahl.

## <a name="run-the-script"></a>Führen Sie das Skript

1. Öffnen Sie eine Windows PowerShell-Befehlskonsole.

    Verwenden Sie die Option **als Administrator ausführen**, sofern Sie über Administratorrechte erforderlich sind, um das Zielverzeichnis erstellen oder Schreiben von Dateien in das angegebene Ziel.

2. Führen Sie die folgenden PowerShell-Befehle aus, die den Wert des Parameters *DestDir* auf jedem beliebigen lokalen Verzeichnis ändern.  Die Standardeinstellung, wir haben hier verwendete, ist `C:\temp\pysql`.

    ```ps
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/PythonSQL/Download_Scripts_SQL_Walkthrough.ps1'
    $ps1_dest = "$pwd\Download_Scripts_SQL_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir 'C:\temp\pysql'
    ```
    
    Wenn der von Ihnen angegebene Ordner in *DestDir* nicht existiert, wird er vom PowerShell-Skript erstellt.
    
    Wenn Sie eine Fehlermeldung erhalten, legen Sie vorübergehend die Richtlinie für die Ausführung von PowerShell-Skripts **uneingeschränkten** in dieser exemplarischen Vorgehensweise mithilfe der **umgehen** Argument und Bereichsauswahl die Änderungen an der aktuellen Sitzung. Das Ausführen dieses Befehls führt zu keiner Konfigurationsänderung.
    
    ```ps
    Set-ExecutionPolicy Bypass -Scope Process
    ```

3. Der Download kann eine Weile dauern, je nach Ihrer Internet-Verbindung. 

## <a name="view-the-results"></a>Anzeigen der Ergebnisse

Wenn alle Dateien heruntergeladen wurden, wechselt PowerShell in das mithilfe des Parameters  *DestDir*angegebene Verzeichnis. 

+ Führen Sie in der PowerShell-Eingabeaufforderung den folgenden Befehl ein, um die Dateien aufzulisten, die heruntergeladen wurden.

    ```ps
    ls
    ```

![Liste der von PowerShell-Skript heruntergeladenen Dateien](media/sqldev-python-filelist.png "Liste der von PowerShell-Skript heruntergeladenen Dateien")

## <a name="next-step"></a>Nächster Schritt

[Schritt 2: Importieren von Daten nach SQL Server mithilfe von PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="previous-step"></a>Vorheriger Schritt

[In der Datenbank Python Analytics für den SQL-Entwickler](sqldev-in-database-python-for-sql-developers.md)

## <a name="see-also"></a>Siehe auch

[Machine Learning-Dienste mit Python](../python/sql-server-python-services.md)


