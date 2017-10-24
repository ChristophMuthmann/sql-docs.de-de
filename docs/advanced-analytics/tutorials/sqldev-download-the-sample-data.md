---
title: 'Lektion 1: Herunterladen der Beispieldaten | Microsoft Docs'
ms.custom: 
ms.date: 07/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 32a5d5ad-c58a-4669-a90d-ef296b48fcd8
caps.latest.revision: 10
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1843dc06a0587e34e0ed369ea54fd5b71b217b24
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-1-download-the-sample-data"></a>Lektion 1: Herunterladen der Beispieldaten

Dieser Artikel ist Teil eines Lernprogramms für SQL-Entwicklern zum Verwenden von R in SQL Server.

In diesem Schritt fügen Sie das Beispieldataset herunterladen und die [!INCLUDE[tsql](../../includes/tsql-md.md)] Skriptdateien, die in diesem Lernprogramm verwendet werden. Die Daten und die Skriptdateien auf GitHub freigegeben werden, aber das PowerShell-Skript Daten-und Skripts auf Ihrer Wahl ein lokales Verzeichnis herunter.

## <a name="download-the-data-and-scripts"></a>Laden Sie die Daten und Skripts

1.  Öffnen Sie eine Windows PowerShell-Befehlskonsole.
  
    Verwenden Sie die Option **Als Administrator ausführen**, wenn Administratorrechte erforderlich sind, um das Zielverzeichnis zu erstellen oder Dateien in das angegebene Ziel zu schreiben.
  
2.  Führen Sie die folgenden PowerShell-Befehle aus, die den Wert des Parameters *DestDir* auf jedem beliebigen lokalen Verzeichnis ändern.  Wir haben in diesem Fall **TempRSQL**verwendet.
  
    ```ps
    $source = ‘https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_SQL_Walkthrough.ps1’  
    $ps1_dest = “$pwd\Download_Scripts_SQL_Walkthrough.ps1”
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir ‘C:\tempRSQL’
    ```
  
    Wenn der von Ihnen angegebene Ordner in *DestDir* nicht existiert, wird er vom PowerShell-Skript erstellt.
  
    > [!TIP]
    > Wenn Sie eine Fehlermeldung erhalten, können Sie für diese exemplarische Vorgehensweise die Richtlinie für die Ausführung von PowerShell-Skripts auf **Uneingeschränkt** festlegen, indem Sie das Bypass-Argument verwenden, und die Gültigkeit der Änderungen auf die aktuelle Sitzung beschränken.
    >   
    >````
    > Set\-ExecutionPolicy Bypass \-Scope Process
    >````
    > Das Ausführen dieses Befehls führt zu keiner Konfigurationsänderung.
  
    Abhängig von Ihrer Internetverbindung kann der Download eine Weile dauern.
  
3.  Wenn alle Dateien heruntergeladen wurden, wechselt PowerShell in das mithilfe des Parameters  *DestDir*angegebene Verzeichnis. Führen Sie den folgenden Befehl in der PowerShell-Eingabeaufforderung aus, und überprüfen Sie die Dateien, die heruntergeladen wurden.
  
    ```
    ls
    ```
  
    **Ergebnisse:**
  
    ![Liste der von PowerShell-Skript heruntergeladenen Dateien](media/rsql-devtut-filelist.png "Liste der von PowerShell-Skript heruntergeladenen Dateien")
  
## <a name="next-lesson"></a>Nächste Lektion

[Lektion 2: Importieren von Daten in SQL Server mit PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)

## <a name="previous-lesson"></a>Vorherige Lektion

[In der Datenbank-R-Analyse für SQL-Entwickler](../tutorials/sqldev-in-database-r-for-sql-developers.md)

