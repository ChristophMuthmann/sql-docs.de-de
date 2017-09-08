---
title: 'Schritt 1: Herunterladen der Beispieldaten | Microsoft Docs'
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 147860e9af8cce86d1a7ccbd3e53f20d240fcd49
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="step-1-download-the-sample-data"></a>Schritt 1: Herunterladen der Beispieldaten

In diesem Schritt fügen Sie das Beispieldataset und Skripts herunterladen. Die Daten- und die Skriptdateien werden jeweils auf Github freigegeben, doch das PowerShell-Skript lädt die Daten und Skriptdateien in ein lokales Verzeichnis Ihrer Wahl herunter.

## <a name="download-the-data-and-scripts"></a>Herunterladen der Daten und Skripts

1. Öffnen Sie eine Windows PowerShell-Befehlskonsole.

    Verwenden Sie die Option **als Administrator ausführen**, sofern Sie über Administratorrechte erforderlich sind, um das Zielverzeichnis erstellen oder Schreiben von Dateien in das angegebene Ziel.

2. Führen Sie die folgenden PowerShell-Befehle aus, die den Wert des Parameters *DestDir* auf jedem beliebigen lokalen Verzeichnis ändern.  Die Standardeinstellung, wir haben hier verwendete, ist **TempPythonSQL**.

    ```
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/PythonSQL/Download_Scripts_SQL_Walkthrough.ps1'
    $ps1_dest = "$pwd\Download_Scripts_SQL_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir 'C:\tempPythonSQL'
    ```
    
    Wenn der von Ihnen angegebene Ordner in *DestDir* nicht existiert, wird er vom PowerShell-Skript erstellt.
    
    Wenn Sie eine Fehlermeldung erhalten, legen Sie vorübergehend die Richtlinie für die Ausführung von PowerShell-Skripts **uneingeschränkten** nur für diese exemplarische Vorgehensweise, mit der **umgehen** Argument und die Änderungen an der aktuellen Bereichsauswahl Sitzung. Das Ausführen dieses Befehls führt zu keiner Konfigurationsänderung.
    
    `Set\-ExecutionPolicy Bypass \-Scope Process`

3. Abhängig von Ihrer Internetverbindung kann der Download eine Weile dauern. Wenn alle Dateien heruntergeladen wurden, wechselt PowerShell in das mithilfe des Parameters  *DestDir*angegebene Verzeichnis. Führen Sie den folgenden Befehl in der PowerShell-Eingabeaufforderung aus, und überprüfen Sie die Dateien, die heruntergeladen wurden.

    ```
    ls
    ```
**Ergebnisse:**

![Liste der von PowerShell-Skript heruntergeladenen Dateien](media/sqldev-python-filelist.png "Liste der von PowerShell-Skript heruntergeladenen Dateien")

## <a name="next-step"></a>Nächster Schritt

[Schritt 2: Importieren von Daten in SQL Server mithilfe von PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="previous-step"></a>Vorheriger Schritt

[In der Datenbank Python Analytics für den SQL-Entwickler](sqldev-in-database-python-for-sql-developers.md)

## <a name="see-also"></a>Siehe auch

[Machine Learning-Dienste mit Python](../python/sql-server-python-services.md)



