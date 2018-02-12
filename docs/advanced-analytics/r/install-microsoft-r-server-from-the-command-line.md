---
title: "Installieren von Machine Learning-Server (eigenständig) oder Microsoft R Server (eigenständig) über die Befehlszeile | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 95f8e0c688a2f141ce066e3831e461509d72c1a9
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="install-machine-learning-server-standalone-or-microsoft-r-server-standalone-from-the-command-line"></a>Installieren von Machine Learning-Server (eigenständig) oder Microsoft R Server (eigenständig) über die Befehlszeile
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel beschreibt die Befehlszeilenargumente für SQL Server verwenden, um die folgenden SQL Server-Funktionen zu installieren, über die Befehlszeile:

+ [In SQLServer 2017 Machine Learning-Server (eigenständig)](#bkmk_mls2017) 
+ [Microsoft R Server (eigenständig), in SQLServer 2016](#bkmk_mrs2016)

Ein **unbeaufsichtigte** Installation erfordert, geben Sie den Speicherort des Setup-Hilfsprogramms und Argumente verwenden, um anzugeben, die zu installierenden Funktionen.

Für eine **stille** Installation geben Sie dieselben Argumente an, und fügen Sie den Schalter **/q** hinzu. Es werden keine aufforderungen mehr bereitgestellt, und keine Benutzerinteraktion erforderlich ist. -Setup Sie jedoch einen Fehler auf, wenn alle erforderlichen Argumente ausgelassen werden.

## <a name="prerequisites"></a>Erforderliche Komponenten

Sie sollten wissen, wie eine Installation von SQL Server über die Befehlszeile ausführen und mit den Argumenten scripting vertraut sein.

Weitere Informationen finden Sie unter [Installieren von SQL Server von der Befehlszeile aus](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).

Wenn Sie Machine Learning-Server oder Microsoft R Server (eigenständig) auf einem Computer, die keinen Zugang zum Internet hat installieren, müssen Sie die erforderlichen Komponenten von R (oder Python) im Voraus herunterladen und in einen lokalen Ordner zu kopieren. Speicherorte für den Download, finden Sie unter [Machine Learning-Komponenten ohne Internetzugang installieren](installing-ml-components-without-internet-access.md).


## <a name="bkmk_mls2017"></a>Installieren Sie Microsoft-Machine Learning-Server (eigenständig)

**Gilt für: SQLServer 2017**

Führen Sie den folgenden Befehl, eine Eingabeaufforderung mit erhöhten Rechten nur Machine Learning-Server (eigenständig) und die erforderlichen Komponenten zu installieren.

+ Die Funktionen Argument ist erforderlich, wie der SQL Server-Lizenzbedingungen ist.
+ Sie können eine Sprache oder sowohl R und Python installieren, aber ist eine separate Lizenz erforderlich, für die einzelnen.

In diesem Beispiel wird gezeigt, die Argumente verwendet, um r zu installieren

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MR  /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

In diesem Beispiel werden die Argumente, die zum Installieren von Python aufgeführt.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MPY  /IACCEPTPYTHONOPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

+ Um den Status und die Befehlsaufforderungen anzuzeigen, entfernen Sie das Argument _/q_.
+ Wenn Sie das Argument verwenden **Funktionen = SQL_SHARED_MR**, nur die Machine Learning-Server-Komponenten installiert sind, mit R weder Python. Diese Installation umfasst alle erforderlichen Komponenten, die standardmäßig im Hintergrund installiert werden. Allerdings wird empfohlen, dass Sie mindestens eine Sprache hinzufügen, wenn Sie zum ersten Mal installieren.
+ Hinzufügen **SQL_INST_MR** zum Installieren von Unterstützung für R.
+ Hinzufügen **SQL_INST_MPY** zum Installieren von Unterstützung für Python.
+ **IACCEPTROPENLICENSETERMS** gibt an, dass Sie den Lizenzbedingungen für die Verwendung der als Open Source vorliegenden R-Komponenten zugestimmt haben.
+ **IACCEPTPYTHONLICENSETERMS** gibt an, Sie haben die Lizenzbedingungen für die Verwendung der Python-Komponenten akzeptiert.
+ **IACCEPTSQLSERVERLICENSETERMS** ist erforderlich, um den Setup-Assistenten auszuführen.


## <a name="bkmk_mrs2016"></a> Installieren von Microsoft R-Server (eigenständig)

**Gilt für: SQLServer 2016**

Führen den folgenden Befehl von einer Eingabeaufforderung mit erhöhten Rechten installiert **nur** Microsoft R Server (eigenständig) und die erforderlichen Komponenten. 

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

> [!TIP]
> Es wird empfohlen, dass Sie nicht diese auf demselben Computer installieren, auf denen eine Instanz von SQL Server R Services gehostet wird.

## <a name="post-installation-tasks"></a>Installationsnachbereitung

Informationen zum Einrichten einer anderen Instanz von Microsoft R Server mit denselben Parametern können Sie die Konfigurationsdatei erneut verwenden, die während der Installation erstellt wird. Weitere Informationen finden Sie unter [Installieren von SQL Server mithilfe einer Konfigurationsdatei](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md).

### <a name="review-installed-components"></a>Überprüfen Sie installiert Komponenten

Nachdem Setup abgeschlossen ist, können Sie die Konfigurationsdatei, die von SQL Server-Setup erstellt wurde, sowie eine Zusammenfassung der Setupaktionen anzeigen.

Standardmäßig alle Protokolle und Zusammenfassungen für SQL Server einrichten und verwandte Funktionen werden erstellt, in den folgenden Ordnern:

+ SQL Server 2017: `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`
+ SQL Server 2016:  `C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log`

Für jede Funktion, die Sie installiert, wird ein separater Unterordner erstellt.

### <a name="customize-the-r-or-python-environment"></a>Anpassen der Umgebung R oder Python

Nach der Installation können Sie zusätzliche R oder Python-Pakete installieren. Der Vorgang unterscheidet sich geringfügig, je nachdem, ob Sie SQL Server 2016 oder SQL Server-2017 verwenden.

In SQl Server-2017 können Sie installieren und Verwalten von R-Pakete mithilfe von T-SQL. Weitere Informationen finden Sie unter [installieren und Verwalten von R-Paketen](../r/install-additional-r-packages-on-sql-server.md).

Für Python und in SQL Server 2016 muss ein Administrator zusätzlichen Bibliotheken installieren, die erforderlich sind.

> [!IMPORTANT]
> Wenn Sie beabsichtigen, Ihre R-Code auf SQL Server ausführen, stellen Sie sicher, dass Sie die gleichen Pakete auf dem Computer installieren, die für die Entwicklung der Lösung und SQL Server-Instanz, in dem Sie ausführen oder Bereitstellen der Lösung, verwendet werden.

### <a name="upgrading-r-server-or-sql-server-machine-learning"></a>Aktualisieren von R-Server oder SQL Server-Machine learning

Wenn Sie nicht beabsichtigen, SQL Server verwenden, können Sie eine separate Windows Installer mit Microsoft R Server "oder" Machine Learning-Server installieren. Downloadpfaden und Anleitungen finden Sie unter folgenden Links:

+ [Installieren Sie Machine Learning-Server für Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Installieren von R Server 9.0.1 für Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) 

Separate Windows Installer für Machine Learning-Server kann auch zum Aktualisieren des Machine learning-Komponenten, mit der Instanz verwendet werden.  Weitere Informationen finden Sie in den folgenden Links:

+ [Verwenden Sie SqlBindR, um R zu aktualisieren.](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)
