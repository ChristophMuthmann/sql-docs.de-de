---
title: Installieren Sie neue Python-Pakete unter SQL Server | Microsoft Docs
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 78a76403f3212c7619afbf02577075161699fbd6
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="install-new-python-packages-on-sql-server"></a>Installieren Sie neue Python-Pakete unter SQL Server

Dieser Artikel beschreibt, wie neue Python-Pakete auf einer Instanz von SQL Server-2017 zu installieren.

Es beschreibt auch, wie Pakete aufzulisten, die in der aktuellen Umgebung installiert sind.

## <a name="prerequisites"></a>Voraussetzungen

Der Prozess für die Installation der neuen Pakete ist ähnlich wie in einer standardumgebung Python. Allerdings sind einige zusätzliche Schritte erforderlich, wenn der Server nicht über eine Internetverbindung verfügt.

+ Sie müssen Machine Learning-Services (Datenbankintern) mit der Python-Sprachoption installiert haben. Anweisungen hierzu finden Sie unter [Python Machine Learning-Dienste einrichten](setup-python-machine-learning-services.md).

+ Für jede Instanz des Servers müssen Sie eine separate Kopie des Pakets installieren. Pakete können nicht über Instanzen freigegeben werden.

+ Bestimmen Sie, ob das Paket, das Sie verwenden möchten mit Python 3.5 und in der Windows-Umgebung funktioniert. 

    Im Allgemeinen bestehen einige Einschränkungen auf die Pakete, die Sie importieren und in der SQL Server-Umgebung verwenden können. Mögliche Probleme sind: Pakete, die verwenden Netzwerkfunktionen, der blockiert ist, auf dem Server oder durch die Firewall, oder Pakete mit Abhängigkeiten, die auf einem Windows-Computer nicht installiert werden.

+ Administratorzugriff auf dem Server ist erforderlich, um Pakete zu installieren.

## <a name="add-a-new-python-package"></a>Fügen Sie ein neues Python-Paket hinzu

In diesem Beispiel wird davon ausgegangen, dass Sie ein neues Paket direkt auf dem SQL Server-Computer installieren möchten.

Das Paket installiert, die in diesem Beispiel ist [CNTK](https://docs.microsoft.com/cognitive-toolkit/), ein Framework zum umfassenden lernen von Microsoft, die Anpassung unterstützt Trainings- und Freigabe von verschiedenen Arten von neuronalen Netzwerken.

> [!TIP]
> Benötigen Sie Hilfe beim Konfigurieren der Python-Tools an? Finden Sie in folgenden Blogs:
> 
> [Erste Schritte mit Python-Webdienste, die mithilfe von Machine Learning-Server](https://blogs.msdn.microsoft.com/mlserver/2017/12/13/getting-started-with-python-web-services-using-machine-learning-server/)
> 
> [David Crook: Cognitive Microsoft-Toolkit + VS-Code](http://dacrook.com/cntk-vs-code-awesome/)

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>Schritt 1: Die Windows-Version von Python-Paket herunterladen

+ Bei der Installation von Python-Pakete auf einem Server ohne Internetzugang müssen Sie die WHL-Datei auf einen anderen Computer herunterladen und kopieren es auf den Server.

    Z. B. auf einem separaten Computer, Sie können die WHL Datei herunterladen von diesem Standort [https://cntk.ai/PythonWheel/CPU-Only](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl), und kopieren Sie die Datei `cntk-2.1-cp35-cp35m-win_amd64.whl` in einen lokalen Ordner auf dem SQL Server-Computer.

+ SQL Server-2017 verwendet Python 3.5. Achten Sie darauf, erhalten Sie die Windows-Version des Pakets, und eine Version, die mit Python 3.5 kompatibel ist.

Diese Seite enthält Downloads für mehrere Plattformen und für mehrere Versionen der Python: [CNTK einrichten](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>Schritt 2: Öffnen Sie eine Python-Eingabeaufforderung

Suchen Sie nach der Python-Bibliothek Standardspeicherort von SQL Server verwendet. Wenn Sie mehrere Instanzen installiert haben, achten Sie darauf, dass Sie den PYTHON_SERVICE-Ordner für die Instanz zu suchen, in dem Sie das Paket hinzufügen möchten.

Z. B. wenn Machine Learning-Dienste mithilfe der Standardwerte installiert wurde, und Machine Learning auf der Standardinstanz aktiviert ist, wäre der Pfad folgendermaßen:

    `C:\Program Files\Microsoft SQL  Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

Öffnen Sie die Python-Eingabeaufforderung, die der Instanz zugeordnet.

> [!TIP]
> Es wird empfohlen, dass Sie eine Python-Umgebung spezifisch für Machine Learning-Server oder SQL Server einrichten.

### <a name="step-3-install-the-package-using-pip"></a>Schritt 3: Installieren Sie das Paket, die Verwendung von pip

+ Wenn Sie mit der über die Befehlszeile Python vertraut sind, verwenden Sie zum Installieren der neuen Pakete PIP.exe. Sie finden die **Pip** Installer in die `Scripts` Unterordner. 

    Wenn Sie eine Fehlermeldung erhalten **Pip** wird nicht erkannt als ein interner oder externer Befehl können Sie den Pfad der ausführbaren Datei Python und den Ordner "Python-Skripts" der PATH-Variablen in Windows hinzufügen.

    Den vollständigen Pfad der **Skripts** Ordner in einer Standardinstallation lautet wie folgt:

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Scripts`

+ Wenn Sie Visual Studio 2017 oder Visual Studio 2015 mit den Python-Erweiterungen verwenden, können Sie ausführen `pip install` aus der **Python-Umgebungen** Fenster. Klicken Sie auf **Pakete**, und geben Sie im Textfeld den Namen oder Speicherort des zu installierenden Pakets an. Sie brauchen geben `pip install`; es wird für Sie automatisch ausgefüllt. 

    - Wenn der Computer über Internetzugriff verfügt, geben Sie den Namen des Pakets oder die URL für ein bestimmtes Paket und eine Version aus. Um die Version des CNTK installieren, die für Windows und Python 3.5 unterstützt wird, können Sie z. B. die Download-URL angeben:`https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - Wenn der Computer nicht über Internetzugriff verfügt, sollten Sie die WHL-Datei im Voraus heruntergeladen haben. Geben Sie dann den lokalen Pfad und den Namen ein. Fügen Sie beispielsweise den folgenden Pfad und Dateinamen zum Installieren der WHL-Datei, die von der Website heruntergeladen:`"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

Sie möglicherweise aufgefordert, die zum Erhöhen der Berechtigungen, um die Installation abzuschließen.

Im Verlauf der Installation können Sie statusmeldungen in das Eingabeaufforderungsfenster sehen:

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```



### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>Schritt 4. Laden Sie das Paket oder seine Funktionen als Teil des Skripts

Wenn die Installation abgeschlossen ist, können Sie sofort beginnen, verwenden das Paket aus, wie im nächsten Schritt beschrieben.

Beispiele für umfassenden Lernen mit CNTK, finden Sie diese Lernprogramme: [Python-API für CNTK](https://cntk.ai/pythondocs/tutorials.html)

Um Funktionen aus dem Paket in Ihr Skript zu verwenden, fügen Sie den Standard `import <package_name>` -Anweisung in der ersten Zeile des Skripts:

```python
import numpy as np
import cntk as cntk
cntk._version_
```

##  <a name="how-to-view-installed-packages-using-conda"></a>Zum Anzeigen der installierten Pakete mit conda

Es gibt verschiedene Möglichkeiten, die Sie eine Liste der installierten Pakete abrufen können. Sie können z. B. Anzeigen der installierten Pakete in der **Python-Umgebungen** Visual Studio-Fenster.

Wenn Sie die Python-Befehlszeile verwenden, können Sie mithilfe der **Conda** Paket-Manager, der mit der Python Anaconda-Umgebung hinzugefügt, die von SQL Server-Setup enthalten ist.

Zum Anzeigen von Python-Pakete, die in der aktuellen Umgebung installiert wurden, führen Sie diesen Befehl aus den Eingabeaufforderungsfenstern aus:

```python
conda list
```

Weitere Informationen zu **Conda** und wie Sie es verwenden können zum Erstellen und Verwalten von mehreren Python-Umgebungen finden Sie unter [Verwaltung von Umgebungen mit Conda](https://conda.io/docs/user-guide/tasks/manage-environments.html).
