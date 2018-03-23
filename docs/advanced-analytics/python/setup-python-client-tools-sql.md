---
title: Einrichten von Python-Clienttools für die Verwendung mit SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: ''
ms.component: python
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: d81c3db5c1d1f4658ff9490316fe2311ba96c66f
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="set-up-python-client-tools-for-use-with-sql-server"></a>Einrichten von Python-Clienttools für die Verwendung mit SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In diesem Artikel wird beschrieben, wie eine Python-Umgebung auf einem Windows-Computer zur Unterstützung von ausgeführten Python-Code in SQL Server konfiguriert wird. Dazu gehören die folgenden Szenarien:

+ Sie testen und Entwickeln von Lösungen auf einer Remotearbeitsstation Python und Senden von Code mit SQL Server für die Ausführung in einer SQL Server-computekontext. 

    Im Allgemeinen eine voll ausgestattete Python-Entwicklungsumgebung installieren möchten. 
    
    Ihrer lokalen Python-Umgebung sollte mit der Python-Umgebung auf die SQL Server-Instanz kompatibel sein, und Sie müssen Bibliotheken, die remote rechenkontexte unterstützen installieren.

+ Sie entwickeln und Testen Sie den Code mithilfe von dedizierten Python-Tools und migrieren Sie den Code zu SQL Server in einer gespeicherten Prozedur ausgeführt werden.

    Sie verwenden eine voll ausgestattete Python-IDE für die Entwicklung, vom Server an. Bevor Sie Code bereitstellen, testen Sie es jedoch in einer Umgebung, die SQL Server-Umgebung emuliert.

+ Sie wird in erster Linie Python-Code in einer gespeicherten Prozedur in SQL Server ausführen, und Sie Python-Code nicht entwickeln. Sie erwarten, dass der Code wurde getestet und debuggt werden, bevor Sie es in einer gespeicherten Prozedur umschließen. Allerdings müssen Sie gelegentlich Ausführen des Codes außerhalb von SQL Server, um die Ursache eines Problems zu ermitteln.

    Sie beliebige Python-Tools auf dem Server installieren möchten, und verwenden nur die Standardtools, die mit der Verteilung installiert. Sie können ggf. eine Python-Umgebung zu konfigurieren, die die Instanz-Bibliothek verwendet, um sicherzustellen, dass Code außerhalb einer gespeicherten Prozedur.

## <a name="requirements"></a>Anforderungen

Unabhängig davon, welche Tools Sie verwenden, um Ihrem Python-Code zu entwickeln, gelten die folgenden Anforderungen auf, wenn Sie Python-Code in SQL Server ausführen, oder verwenden SQL Server-Daten:

+ Um Python zu verwenden, ist SQLServer 2017 oder höher erforderlich. Sie müssen auch installieren die Funktion, die Machine Learning-Services (Datenbankintern) unterstützt und die Funktion explizit aktivieren. Weitere Informationen finden Sie unter [Einrichten von SQL Server-2017](../r/set-up-sql-server-r-services-in-database.md).

    Wenn Sie eine frühe Version von SQL Server-2017 installiert haben, erhalten Sie möglicherweise Fehler, wenn Sie versuchen, die Ausführung von Python-Befehlen an dieses Befehlszeilen-Hilfsprogramm. Es wird empfohlen, die Sie [ein Upgrade auf die neueste Version](#bkmk_update) Wenn möglich. 

+ Sie müssen sicherstellen, dass das Konto, das Sie verwenden, um das Ausführen des Codes über die Berechtigung für die Verbindung mit der Datenbank sowie zum Ausführen von Python-Code verfügt. Die spezielle Berechtigung `EXECUTE ANY EXTERNAL SCRIPT` ist erforderlich für alle Konten, die R oder Python-Skript verwenden. 

+ Sie müssen sicherstellen, dass das Konto keine Datenbankberechtigungen, die möglicherweise erforderlich, um die Daten lesen oder neue Objekte erstellen. 

+ Wenn Ihr Code Pakete, die nicht standardmäßig mit SQL Server installiert sind erfordert, ordnen Sie den Datenbankadministrator, um die Pakete installiert, die in der Python-Umgebung, die von der Instanz verwendet wird. SQL Server ist eine sichere Umgebung, und es gibt Einschränkungen auf, in dem Pakete installiert werden kann. 

    Ad-hoc-Installation von Paketen als Teil des Codes wird nicht empfohlen, auch wenn Sie Administratorrechte verfügen. Darüber hinaus immer sorgfältig prüfen Auswirkungen auf die Sicherheit vor der Installation der neuen Pakete in der Serverbibliothek.

> [!NOTE]
> Wenn Sie beabsichtigen, verwenden von Python mit Machine Learning-Server, die zusätzliche rechenkontexte, z. B. Linux oder Spark-Cluster unterstützt, finden in diesen Artikeln:
> 
> + [Wie Sie benutzerdefinierte Python-Pakete und Interpreter lokal auf Windows installieren](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)
> + [Verknüpfen Sie Python-Tools und IDEs, mit der Python-Interpreter mit Machine Learning-Server installiert](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)

## <a name="default-tools-included-with-standard-install"></a>Standardtools, die mit der Standardinstallation enthalten

Eine Standardinstallation von SQL Server-2017 mit Machine Learning-Services (datenbankintern) und Python fügt die folgenden standardmäßigen Python-Tools und Ressourcen:

+ Python-Beispieldaten
+ 4.2-Anaconda-Verteilung 
+ Python executables python.exe and pythonw.exe

Standardmäßig ist Installation in diesen Ordner: `~\Program Files\Microsoft SQL Server\<instance_name>\PYTHON_SERVICES`. 

## <a name="open-python-from-the-command-line"></a>Öffnen Sie in der Befehlszeile Python 

Um die Python-Laufzeit zu verwenden, die mit der Instanz installiert ist, können Sie die ausführbare Python im Installationspfad aus starten. Grundlegende Anweisungen befinden sich die [Python für Windows – häufig gestellte Fragen](https://docs.python.org/3/faq/windows.html).

> [!IMPORTANT]
> Im Allgemeinen um Ressourcenkonflikte zu vermeiden, sollten Sie **nicht** Python aus der Bibliothek für die Instanz auf dem Server ausgeführt, wenn Sie vermuten, dass es ist möglich, SQL Server-Instanz ausgeführt wird Python-Code. Allerdings mit den Tools in der Bibliothek Instanz möglicherweise nützlich, wenn Sie versuchen, Debuggen ein Problem, das erfolgt nur, wenn in SQL Server ausgeführt und weitere ausführliche Fehlermeldungen anzuzeigen, oder stellen Sie sicher, dass alle erforderlichen Pakete installiert werden soll.

1. Navigieren Sie zu dem Ordner, in dem die Instanz-Bibliothek installiert ist. In einer Standardinstallation ist der Ordner beispielsweise `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`.

2. Suchen Sie nach Python.exe. 

3. Mit der rechten Maustaste, und wählen Sie **als Administrator ausführen** ein interaktives Befehlszeilentools-Fenster zu öffnen.

## <a name="bkmk_update"></a> Aktualisieren von Python-Komponenten

Sie können die Python-Komponenten aktualisieren, indem Sie herunterladen und installieren eine neuere Version mit den hier beschriebenen Skripts: [installieren Sie Python-Client unter Windows](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter#install-on-windows)
> 
> Das Installationsprogramm heruntergeladen haben, indem Sie das Skript [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054&clcid=1033). Wenn Sie eine andere Version benötigen, finden Sie unter [Machine Learning-Komponenten ohne Internetzugang installieren](http://bing.com)

## <a name="set-up-a-python-development-environment"></a>Einrichten einer Umgebung der Python-Entwicklung

Wenn Sie Skripts über die Befehlszeile einfach Debuggen, können Sie abrufen, indem in der standardmäßigen Python-Tools mit Machine Learning-Diensten installiert oder mithilfe eines Text-Editors. Wenn Sie neue Lösungen entwickeln, oder von einem Remoteclient aus arbeiten, empfehlen wir jedoch verwenden, der eine voll ausgestattete Python-IDE. Beliebte Optionen sind verfügbar:

+ [Community-Edition von Visual Studio 2017](https://www.visualstudio.com/vs/features/python/) mit Python
+ [AI-Tools für Visual Studio](https://docs.microsoft.com/visualstudio/ai/installation)
+ [Python in Visual Studio-Code](https://code.visualstudio.com/docs/languages/python)
+ Beliebte Drittanbietertools wie PyCharm, Spyder und Eclipse

Visual Studio wird empfohlen, da es sich um Datenbankprojekte als auch für Machine Learning-Projekte unterstützt. Hilfestellung bei der Konfiguration einer Python-Umgebung finden Sie unter [Verwalten von Python-Umgebungen in Visual Studio](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)

## <a name="install-revoscalepy"></a>Installieren von revoscalepy

Auch wenn Sie Machine Learning-Dienste erfolgreich installiert haben, möglicherweise eine Fehlermeldung erhalten, wenn versucht wird, laden **Revoscalepy** Funktionen über die Befehlszeile Python. Diese Schritte beschrieben, wie Sie ein Update aus, um die Verwendung von installieren können **Revoscalepy**.

1. Herunterladen der Shell-Skript für die Installation von https://aka.ms/mls93-py (oder verwenden Sie https://aka.ms/mls-py für die 9.2. Release). Das Skript wird Anaconda 4.2.0 müssen, darunter Python 3.5.2, sowie alle Pakete, die zuvor genannten installiert.

2. Öffnen Sie ein neues PowerShell-Fenster mit erhöhten Berechtigungen (als Administrator).

3. Öffnen Sie den Ordner, in dem Sie das Installationsprogramm heruntergeladen haben, und führen Sie das Skript aus:

```ps1
cd {{download-directory}}
.\Install-PyForMLS.ps1
```

Sie können auch Ausführen der `-InstallFolder` Befehlszeilenargument und den neuen Pfad als Teil des Befehls angeben. Beispiel: 

```ps1
.\Install-PyForMLS.ps1 -InstallFolder "<installation_path>")
```

Wenn Sie eine Fehlermeldung erhalten, müssen Sie möglicherweise die Ausführungsrichtlinien für eine bestimmte Datei, die Dauer der Sitzung, anhalten, die wie folgt: 

```ps1
powershell -ExecutionPolicy Bypass -File "C:\<installation_path>\Install-PyForMLS.ps1"
```

Sie können auch Ausführungsrichtlinien für die Dauer der Sitzung anzuhalten. Mit dieser Anweisung wird Festlegen der Ausführungsrichtlinie zu `Unrestricted` für die Dauer der Sitzung, und nicht die Konfiguration ändern oder die Änderung auf dem Datenträger festgeschrieben.

```ps1
Set-ExecutionPolicy Bypass -Scope Process
```

## <a name="verify-that-python-and-revoscalepy-are-working"></a>Stellen Sie sicher, dass Python und Revoscalepy arbeiten

Nach der Installation von allen Tools und Bibliotheken, sollten Sie eine Verbindung mit dem Server herstellen und stellen Sie sicher, dass Sie einen computekontext erstellen können, oder dass Python mit SQL Server kommunizieren kann.

### <a name="verify-that-revoscalepy-works-from-the-python-command-line"></a>Überprüfen Sie, ob diese Revoscalepy über die Befehlszeile Python funktioniert

Zum Überprüfen, ob die **Revoscalepy** Modul kann geladen werden, den folgende Beispielcode über eine Eingabeaufforderung der Python interactive ausführen. Der Code generiert eine Zusammenfassung der mithilfe der Python-Beispieldaten und [Rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary). 

```Python
import os
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions
sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)
ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay+DayOfWeek", ds)
print(summary)
```

Der Pfad zum Beispiel wird gedruckt, damit Sie bestimmen können, welche Instanz des Python aufgerufen wird.

### <a name="verify-that-python-can-be-called-from-sql-server"></a>Stellen Sie sicher, dass Python von SQL Server aufgerufen werden kann

Um sicherzustellen, dass Python mit SQL Server kommuniziert wird, öffnen Sie SQL Server Management Studio. (Sie können z. B. ein vergleichbares Tool verwenden [SQL Operations Studio](https://docs.microsoft.com/sql/sql-operations-studio/what-is).) Öffnen Sie ein neues **Abfrage** Fenster, und führen Sie eine einfache Python-im Rahmen einer gespeicherten Prozedur-Befehl:

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'print(3+4)'
```

Es kann dauern, bis die Python-Laufzeit zum ersten Mal starten, aber keine Fehler vorliegen, Sie wissen, dass der SQL Server Launchpad funktioniert und Python von SQL Server gestartet werden kann.

Zum Überprüfen, ob **Revoscalepy** finden Sie in der SQL Server-Instanz-Bibliothek, führen Sie das Skript basierend auf [Rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary), mit einigen geringfügigen Änderungen zum Generieren von Ergebnissen, die mit SQL Server kompatibel. 

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'
import os
from pandas import DataFrame
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions

sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay + DayOfWeek", ds)
print(summary)
dfsummary = summary.summary_data_frame
OutputDataSet = dfsummary
'
WITH RESULT SETS  ((ColName nvarchar(25) , ColMean float, ColStdDev  float, ColMin  float,   ColMax  float, Col_ValidObs  float, Col_MissingObs int))
```

Da Rx_summary ein Objekt des Typs zurückgibt `class revoscalepy.functions.RxSummary.RxSummaryResults`, die mehrere Elemente enthält, um die Ergebnisse in SQL Server zu behandeln, können Sie nur die Datenrahmen in einem tabellarischen Format extrahieren.

### <a name="verify-python-execution-in-sql-server-as-remote-compute-context"></a>Überprüfen Sie die Python-Ausführung in SQL Server als remote-computekontext.

Wenn Sie installiert haben **Revoscalepy** in Ihrer lokalen Umgebung der Python-Entwicklung, sollten Sie möglicherweise mit einer Instanz von SQL Server-2017 herstellen, auf dem Python aktiviert wurde, und führen Sie eine ähnliche Codebeispiel mithilfe des Servers als die Compute Kontext. 


```Python
import os
from revoscalepy import rx_summary, RxOptions, RxXdfData, RxSqlServerData, RxInSqlServer

# define connection string and compute context
sql_conn_string="Driver=SQL Server;Server=;Database=TestDB;Trusted_Connection=True"
sqlcc = RxInSqlServer(
    connection_string = sql_conn_string,
    num_tasks = 1,
    auto_cleanup = False,
    console_output = True,
    execution_timeout_seconds = 0,
    wait = True
    )
rx_set_compute_context(sqlcc)

# get sample data and path
sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

# generate summary
ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay+DayOfWeek", ds)
print(summary)
```

In diesem Beispiel wird Zusammenfassung Objekt an die Konsole, anstatt zurückgebenden wohlgeformt tabellarischen Daten in SQL Server zurückgegeben. 

Darüber hinaus da [Rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) wurde aufgerufen, werden die Beispieldaten aus dem Ordner "Samples" auf dem SQL Server-Computer, und nicht aus Ihrem lokalen Beispielordner geladen.
