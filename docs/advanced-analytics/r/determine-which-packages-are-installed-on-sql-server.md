---
title: Anzeigen von R oder Python-Pakete, die auf SQL Server installiert | Microsoft Docs
ms.custom: ''
ms.date: 02/19/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: e57c22301f69039ad2aa9466a87cce37762691e3
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="viewing-r-or-python-packages-installed-on-sql-server"></a>Anzeigen von R oder Python-Pakete, die auf SQL Server installiert
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Wenn Sie mehrere Python-Umgebungen installiert haben oder mehrere R-Tools verwenden, ist es einfach installiert ein Paket auf der falschen Bibliothek oder der Umgebung und dann nicht möglich, später zu finden. 

Dieser Artikel enthält einige Abfragen, die Sie verwenden können, um Ihrer aktuellen Version zu bestimmen und die Pakete aufzulisten, die in der aktuellen SQL Server-Umgebung installiert sind.

## <a name="verify-the-current-default-library"></a>Überprüfen Sie die aktuelle Standardbibliothek

Für **R** in SQL Server, führen Sie die folgende Anweisung aus, um die Standardbibliothek für die aktuelle Instanz zu überprüfen:

```sql
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Für **Python** in SQL Server, führen Sie die folgende Anweisung aus, um die Standardbibliothek für die aktuelle Instanz zu überprüfen:

```sql
EXEC sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

## <a name="generate-a-package-list-using-a-stored-procedure"></a>Generieren Sie eine Liste der Pakete mit einer gespeicherten Prozedur

Es gibt mehrere Möglichkeiten, die Sie eine vollständige Liste der installierten Pakete abrufen können. Ein Vorteil der ausgeführten Paket List-Befehle aus Sp_execute_external_script ist, dass Sie sichergestellt, dass werden Pakete, die in der Bibliothek für die Instanz installiert.

### <a name="r"></a>R

Im folgenden Beispiel wird die R-Funktion `installed.packages()` in einem [!INCLUDE [tsql](..\..\includes\tsql-md.md)] gespeicherte Prozedur, eine Matrix aus Paketen abzurufen, die in der Bibliothek R_SERVICES für die aktuelle Instanz installiert wurden. Um zu vermeiden, dass die Felder in der DESCRIPTION-Datei analysiert werden, wird nur der Name zurückgegeben.

```SQL
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
NameOnly <- packagematrix[,1];
OutputDataSet <- as.data.frame(NameOnly);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250) ))
```

Weitere Informationen zu den optionalen und Standardfelder für das Beschreibungsfeld der R-Paket finden Sie unter [ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

### <a name="python"></a>Python

Die `pip` Modul wird standardmäßig installiert, und unterstützt viele Vorgänge zum Auflisten installiert Pakete, zusätzlich zu den vom standard Python unterstützt. Sie können ausführen `pip` aus einem Python Eingabeaufforderung natürlich, aber Sie können auch einige Pip-Funktionen aufrufen von `sp_execute_external_script`.

```sql
execute sp_execute_external_script 
@language = N'Python', 
@script = N'
import pip
import pandas as pd
installed_packages = pip.get_installed_distributions()
installed_packages_list = sorted(["%s==%s" % (i.key, i.version)
     for i in installed_packages])
df = pd.DataFrame(installed_packages_list)
OutputDataSet = df
'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

Beim Ausführen `pip` über die Befehlszeile stehen viele weitere Funktionen: `pip list` Ruft alle Pakete, die installiert werden, wohingegen `pip freeze` Listet die Pakete installiert, indem Sie `pip`, und nicht auflisten von Paketen, die selbst pip hängt ab. Sie können auch `pip freeze` um eine Abhängigkeitsdatei zu generieren.

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>Überprüfen Sie, ob ein Paket mit einer Instanz installiert ist

Wenn Sie ein Paket installiert haben und möchten sicherstellen, dass er für eine bestimmte SQL Server-Instanz verfügbar ist, können Sie durch Ausführen der folgenden Aufruf der gespeicherten Prozedur, laden Sie das Paket und nur Nachrichten zurück.

### <a name="r"></a>R

In diesem Beispiel sucht und lädt die Bibliothek "revoscaler" aus, falls verfügbar.

```sql
EXEC sp_execute_external_script  @language =N'R',
@script=N'require("RevoScaleR")'
GO
```

+ Wenn das Paket gefunden wird, wird eine Meldung zurückgegeben: "Befehle wurde erfolgreich abgeschlossen."

+ Wenn das Paket gespeichert oder geladen werden kann, erhalten Sie eine Fehlermeldung, die mit dem Text: "ist kein Paket namens"MissingPackageName""

### <a name="python"></a>Python

Das entsprechende Kontrollkästchen für Python ausgeführt werden kann, aus der Python-shell, mit `conda` oder `pip` Befehle. Führen Sie stattdessen diese Anweisung in einer gespeicherten Prozedur an:

```sql
exec sp_execute_external_script
       @language = N'Python'
       , @script = N'
import pip
import pkg_resources
pckg_name = "revoscalepy"
pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
installed_pckg = pckgs.query(''key == @pckg_name'')
print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")
```

## <a name="view-installed-packages-using-a-utility-or-ide"></a>Anzeigen der installierten Pakete, die über ein Dienstprogramm oder der IDE

Die meisten Entwicklungstools bieten eine Objektkatalog oder eine Liste der Pakete, die installiert sind, oder, im aktuellen Arbeitsbereich oder in der Umgebung geladen werden. Dieser Abschnitt enthält einige kurze Tipps für die Verwendung von beliebten R oder Python-Tools.

### <a name="r-tools"></a>R-tools

Es gibt mehrere Möglichkeiten, eine Liste der installierten oder geladenen Pakete mithilfe von R-Hilfsprogramme zu erhalten. 

+ Aus einem lokalen R-Hilfsprogramm, verwenden Sie eine Basis R-Funktion, wie z. B. `installed.packages()`, im Lieferumfang der `utils` Paket. Um eine Liste zu erhalten, die für eine Instanz genau ist, müssen Sie Bibliothekspfad explizit angeben oder verwenden Sie die R-Tools, die der Instanz-Bibliothek zugeordnet.

### <a name="python-tools"></a>Python-tools

Python-Erweiterungen für Visual Studio stellen die sehr einfach, Pakete, die installiert werden, in der aktuellen Umgebung oder in anderen virtuellen Umgebungen aufgeführt, die in der IDE anzeigen. Mehrere Umgebungen konfigurieren können, wählen Sie eine Umgebung aus einer Liste, und zeigen Sie die Pakete oder neue Pakete zu dieser Umgebung installieren.

+ [Python-Umgebungen](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)

Visual Studio-Code ist eine kostenlose-Editor, der Python, unterstützt auch mehrere Python Linters verfügbar. Obwohl Visual Studio Code wie in Visual Studio einen Paket-Browser nicht bereitstellt, unterstützt konfigurieren und Wechseln zwischen mehreren Umgebungen.

+ [Python in Visual Studio-Code](https://code.visualstudio.com/docs/languages/python)

Möglicherweise einige zusätzliche Konfigurationsschritte erforderlich, um ausführen **Revoscalepy** Befehle von einem Remoteclient aus:

+ [Installieren Sie benutzerdefinierte Python-Pakete und Interpreter lokal auf Windows](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)

Dieses Blog bietet einige nützliche Tipps zum Konfigurieren von anderen Python-Umgebungen, einschließlich PyCharm, zur Bearbeitung **Revoscalepy**.

+ [Erste Schritte mit Python-Webdienste, die mithilfe von Machine Learning-Server](https://blogs.msdn.microsoft.com/mlserver/2017/12/13/getting-started-with-python-web-services-using-machine-learning-server/)

## <a name="use-functions-from-machine-learning-server"></a>Verwenden Sie die Funktionen von Machine Learning-Server

Da die Bibliotheken, die mit SQL Server-Support-Ausführung von Code von einem Remoteclient aus verwendet, Sie diese Funktionen verwenden können, um herauszufinden, welche Pakete werden in einer Remoteumgebung installiert.

### <a name="revoscaler"></a>RevoScaleR

Wenn Sie einen remote-Client arbeiten und keinen Zugriff auf den Server haben, erhalten Sie weiterhin eine Liste der Pakete, die auf SQL Server mithilfe von RevoScaleR-Funktionen installiert werden. Sie geben Sie den SQL Server als computekontext verwenden, die erfordert, dass Sie die Berechtigung zur Verbindung mit des Servers. 

+ [RxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) sucht den Pfad für ein Paket in der remote-computekontext.

+ [RxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) Ruft Informationen zu Paketen, die in einen computekontext installiert.

Führen Sie z. B. die folgenden R-Code zum Abrufen einer Liste von Paketen, die in der angegebenen SQL Server-computekontext verfügbar.

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```

Im folgenden Beispiel wird der Speicherort von "revoscaler" im lokalen rechenkontext und die Paketversion.

```R
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

### <a name="revoscalepy"></a>revoscalepy

Funktionen, die ähnlich wie für "revoscaler" sind zurzeit nicht verfügbar. Suchen Sie in einer späteren Version von **Revoscalepy**.

## <a name="get-library-location-and-version"></a>Speicherort der Bibliothek und Version abrufen

Auch müssen wenn Sie mit mehreren Umgebungen oder Installationen von R oder Python arbeiten, Sie bestätigen, dass der Code, den Sie ausführen, werden die richtige Umgebung für Python oder den Arbeitsbereich "richtige" für r verwenden

Upgrade von Machine learning-Komponenten mithilfe von Bindung kann z. B. der Pfad zum R-Bibliothek in einem anderen Ordner als den Standardwert sein. Wenn Sie R-Client oder eine Instanz des eigenständigen Servers installieren, müssen Sie außerdem möglicherweise mehrere R-Bibliotheken auf Ihrem Computer.

Diese Beispiele zum Abrufen der Pfad und die Version der Bibliothek, die von SQL Server verwendet wird.

### <a name="r"></a>R

Diese gespeicherte Prozedur gibt den Pfad der Instanz-Bibliothek und die Version des Pakets "revoscaler" von SQL Server verwendet:

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> Die [RxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) Funktion kann nur auf dem Zielcomputer ausgeführt werden. Die Funktion kann nicht für Remoteverbindungen Bibliothekspfade zurück.

**Ergebnisse**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```

### <a name="python"></a>Python

In diesem Beispiel gibt die Liste der Ordner für die Python `sys.path` Variable. Die Liste enthält das aktuelle Verzeichnis und den Pfad der Standardbibliothek.

```sql
EXEC sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

**Ergebnisse**

```text
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\python35.zip
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\DLLs
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Sphinx-1.5.4-py3.5.egg
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Pythonwin
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\setuptools-27.2.0-py3.5.egg
```

Weitere Informationen zu den Variablen `sys.path` und wie sie zum Festlegen der Interpreter Suchpfad für Module verwendet wird, finden Sie unter der [Python-Dokumentation](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

