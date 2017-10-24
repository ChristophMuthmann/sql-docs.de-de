---
title: "Installieren von Microsoft R Server über die Befehlszeile | Microsoft-Dokumentation"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: b9f6ceba4d3609a7e7ff816d31446a77c4fea64c
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="install-microsoft-r-server-from-the-command-line"></a>Installieren von Microsoft R Server über die Befehlszeile
    
Dieses Thema beschreibt, wie SQL Server-Befehlszeilenargumente, installieren Sie Microsoft R Server in SQL Server 2016 oder Machine Learning-Server (eigenständig) in SQL Server-2017. 

> [!NOTE]
Sie können auch Microsoft R Server mit einem separaten Windows Installer installieren. Weitere Informationen finden Sie unter [installieren R Server 9.0.1 für Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows). 

## <a name="prerequisites"></a>Erforderliche Komponenten

Diese Methode der Installation erfordert, dass Sie wissen, wie Sie eine Installation von SQL Server über die Befehlszeile ausführen und mit den Argumenten scripting vertraut sind.

- **Unbeaufsichtigte** Installation erfordert, dass Sie den Speicherort des Setupprogramms angeben und Argumente verwenden, um anzugeben, welche Funktionen installiert werden sollen. 
- Für eine **stille** Installation geben Sie dieselben Argumente an, und fügen Sie den Schalter **/q** hinzu. Es werden keine Eingabeaufforderungen angezeigt, und es ist keine Interaktion erforderlich. Allerdings schlägt Setup fehl, wenn eines der erforderlichen Argumente nicht angegeben ist.

Weitere Informationen finden Sie unter [Installieren von SQL Server 2016 über die Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).

## <a name="sql-server-2017-microsoft-machine-learning-server-standalone"></a>SQLServer 2017: Microsoft Machine Learning-Server (eigenständig)

Führen Sie den folgenden Befehl, eine Eingabeaufforderung mit erhöhten Rechten, um nur Microsoft Machine Learning-Server (eigenständig) und die erforderlichen Komponenten zu installieren.  Im Beispiel wird gezeigt, die Argumente verwendet, um r zu installieren.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MR  /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS 
```

Um den Status und die Befehlsaufforderungen anzuzeigen, entfernen Sie das Argument _/q_.

- **Funktionen = SQL_SHARED_MR** ruft nur die Machine Learning-Server-Komponenten ab. Dies schließt alle erforderlichen Komponenten, die standardmäßig im Hintergrund installiert werden.
- **SQL_INST_MR** ist erforderlich, um Installl-Unterstützung für die Sprache "R".
- **SQL_INST_MPY** Unterstützung für Python-Installation erforderlich sind.
- **IACCEPTROPENLICENSETERMS** gibt an, dass Sie den Lizenzbedingungen für die Verwendung der als Open Source vorliegenden R-Komponenten zugestimmt haben.
- **IACCEPTPYTHONLICENSETERMS** gibt an, Sie haben die Lizenzbedingungen für die Verwendung der Python-Komponenten akzeptiert.
- **IACCEPTSQLSERVERLICENSETERMS** ist erforderlich, um den Setup-Assistenten auszuführen.

**Hinweise**

1. Die Funktionen Argument ist erforderlich, wie der SQL Server-Lizenzbedingungen ist.
2. Geben Sie mindestens eine Sprache, zusammen mit der Lizenzierung Vereinbarung-Flag.
3. Sie können eine Sprache oder sowohl R und Python installieren, aber ist eine separate Lizenz erforderlich, für die einzelnen.

## <a name="sql-server-2016-microsoft-r-server-standalone"></a>SQLServer 2016: Microsoft R Server (eigenständig)

Führen Sie den folgenden Befehl aus einer Eingabeaufforderung mit erhöhten Rechten aus, um nur Microsoft R Server (Standalone) und die entsprechenden Voraussetzungen zu installieren.  Das Beispiel zeigt die Argumente, die mit SQL Server 2016-Setup verwendet.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

## <a name="offline-installation"></a>Offlineinstallation

Wenn Sie Machine Learning-Server oder Microsoft R Server (eigenständig) auf einem Computer, die keinen Zugang zum Internet hat installieren, müssen Sie die erforderlichen R-Komponenten im Voraus herunterladen und in einen lokalen Ordner zu kopieren. Informationen zu Downloadspeicherorten finden Sie unter [Installation von R-Komponenten ohne Internetzugang](../r/installing-ml-components-without-internet-access.md).

## <a name="what-is-installed"></a>Was ist installiert

Nachdem Setup abgeschlossen ist, können Sie die Konfigurationsdatei, die von SQL Server-Setup erstellt wurde, sowie eine Zusammenfassung der Setupaktionen anzeigen.

Standardmäßig alle Protokolle und Zusammenfassungen für SQL Server einrichten und verwandte Funktionen werden erstellt, in den folgenden Ordnern:

- SQLServer 2016:`C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log`
- SQLServer 2017:`C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`

Für jede installierte Funktion wird ein eigener Unterordner erstellt.

Informationen zum Einrichten einer anderen Instanz von Microsoft R Server mit denselben Parametern können Sie die Konfigurationsdatei erneut verwenden, die während der Installation erstellt wird. Weitere Informationen finden Sie unter [Installieren von SQL Server mithilfe einer Konfigurationsdatei](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)


## <a name="customize-your-r-environment"></a>Anpassen der R-Umgebung

Nach der Installation können Sie zusätzliche R-Pakete installieren. Weitere Informationen finden Sie unter [Installieren und Verwalten von R-Paketen](../r/install-additional-r-packages-on-sql-server.md).

> [!IMPORTANT]
> Wenn Sie beabsichtigen, Ihre R-Code auf SQL Server ausführen, stellen Sie sicher, dass Sie die gleichen Pakete auf dem Computer installieren, die für die Entwicklung der Lösung und SQL Server-Instanz, in dem Sie ausführen oder Bereitstellen der Lösung, verwendet werden.

Nach der Installation von Machine Learning-Dienste für R (In-Database) können Sie separaten Windows Installer verwenden, um die Version von R zu aktualisieren, die eine angegebene SQL Server-Instanz zugeordnet ist. Weitere Informationen finden Sie unter [verwenden SqlBindR Upgrade r](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).



