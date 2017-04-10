---
title: "Installieren von Microsoft R Server &#252;ber die Befehlszeile | Microsoft Docs"
ms.custom: ""
ms.date: "01/19/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: 4
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 3
---
# Installieren von Microsoft R Server &#252;ber die Befehlszeile
    
Sie können Microsoft R Server über die Befehlszeile installieren, indem Sie die Skriptfunktionalität verwenden, die mit SQL Server-Setup bereitgestellt wird. 

- **Unbeaufsichtigte** Installation erfordert, dass Sie den Speicherort des Setupprogramms angeben und Argumente verwenden, um anzugeben, welche Funktionen installiert werden sollen. 
- Für eine **stille** Installation geben Sie dieselben Argumente an, und fügen Sie den Schalter **/q** hinzu. Es werden keine Eingabeaufforderungen angezeigt, und es ist keine Interaktion erforderlich. Allerdings schlägt Setup fehl, wenn eines der erforderlichen Argumente nicht angegeben ist.

Weitere Informationen finden Sie unter [Installieren von SQL Server 2016 über die Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).

## <a name="perform-a-command-line-install-of-microsoft-r-server-standalone"></a>Ausführen einer Befehlszeileninstallation von Microsoft R Server (Standalone)

 Im folgenden Beispiel sind die Argumente veranschaulicht, die verwendet werden, wenn mit SQL Server-Setup eine Befehlszeileninstallation von Microsoft R Server ausgeführt wird.


### <a name="example-of-unattended-installation-of-r-server-standalone"></a>Beispiel einer unbeaufsichtigten Installation von R Server (Standalone)

Führen Sie den folgenden Befehl aus einer Eingabeaufforderung mit erhöhten Rechten aus, um nur Microsoft R Server (Standalone) und die entsprechenden Voraussetzungen zu installieren. 

```  
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS 
```  

Sollen der Status und die Eingabeaufforderungen angezeigt werden, entfernen Sie das Argument „/q“.

Beachten Sie, dass alle folgenden Argumente erforderlich sind:
  - **FEATURES = SQL_SHARED_MR** ruft nur die Microsoft R Server-Komponenten ab, einschließlich Microsoft R Open und allen entsprechenden Voraussetzungen.
  - **IACCEPTROPENLICENSETERMS** gibt an, dass Sie den Lizenzbedingungen für die Verwendung der als Open Source vorliegenden R-Komponenten zugestimmt haben.
  - **IACCEPTSQLSERVERLICENSETERMS** ist erforderlich, um den Setup-Assistenten auszuführen.


### <a name="offline-installation"></a>Offlineinstallation

Wenn Sie Microsoft R Server (Standalone) auf einem Computer installieren, der keinen Zugriff auf das Internet hat, müssen Sie die erforderlichen R-Komponenten im Voraus herunterladen und in einen lokalen Ordner kopieren. Informationen zu Downloadspeicherorten finden Sie unter [Installation von R-Komponenten ohne Internetzugang](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).   


## <a name="advanced-installation-tips"></a>Erweiterte Tipps zur Installation

Nachdem Setup abgeschlossen ist, können Sie die Konfigurationsdatei, die von SQL Server-Setup erstellt wurde, sowie eine Zusammenfassung der Setupaktionen anzeigen.

Standardmäßig werden alle Setupprotokolle und -zusammenfassungen für SQL Server und verwandte Funktionen in `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log` erstellt.

Für jede installierte Funktion wird ein eigener Unterordner erstellt. Für Microsoft R Server suchen Sie nach: 
- `RSetup.log`
- `Settings.xml`
- `Summmary<instance_GUID>.txt`

Wenn Sie eine weitere Instanz von Microsoft R Server mit denselben Parametern einrichten möchten, können Sie auch die Konfigurationsdatei wiederverwenden, die während der Installation erstellt wurde. Weitere Informationen hierzu finden Sie unter [Installieren von SQL Server mithilfe einer Konfigurationsdatei](https://msdn.microsoft.com/library/dd239405.aspx).



### <a name="customizing-your-r-environment"></a>Anpassen Ihrer R-Umgebung

Nach der Installation können Sie zusätzliche R-Pakete installieren. Weitere Informationen finden Sie unter [Installieren und Verwalten von R-Paketen](../../advanced-analytics/r-services/installing-and-managing-r-packages.md).

> [!IMPORTANT]
> Wenn Sie Ihren R-Code in SQL Server ausführen möchten, müssen Sie dieselben Pakete sowohl auf dem Clientcomputer, auf dem Microsoft R Server ausgeführt wird, als auch in der SQL Server-Instanz installieren, unter der R Services ausgeführt wird. 



## <a name="see-also"></a>Siehe auch  

[Microsoft R Server](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)
  