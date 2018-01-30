---
title: "Bereitstellen eines virtuellen Computers für Machine Learning in Azure | Microsoft Docs"
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
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 781622d51b7112d3a501652b7c320ab27e74ae35
ms.sourcegitcommit: c77a8ac1ab372927c09bf241d486e96881b61ac9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="provision-a-virtual-machine-for-machine-learning-on-azure"></a>Bereitstellen eines virtuellen Computers für Machine Learning in Azure

Virtuelle Computer in Azure sind eine praktische Möglichkeit für einen vollständigen Server-Umgebung für den Machine learning-Lösungen schnell konfigurieren.

Dieser Artikel führt der Abbilder der virtuellen Maschine, die SQL Server mit den Machine learning-als auch einige verknüpfte virtuelle Computer enthalten.

Dieser Artikel bietet auch Antworten auf häufig gestellte Fragen zu ändern oder Aktualisieren einer vorhandenen SQL Server-Instanz auf einem virtuellen Computer.

+ [Liste der aktuellen virtuellen Computer](#bkmk_list)

## <a name="provision-a-virtual-machine-with-sql-server-and-machine-learning"></a>Bereitstellen eines virtuellen Computers mit SQL Server und machine learning

Wenn Sie mit der Azure-VMs nicht vertraut sind, wird empfohlen, dass Sie weitere Informationen zu mithilfe des Portals und Konfigurieren eines virtuellen Computers den folgenden Artikeln finden Sie unter.

+ [Virtuelle Computer – Erste Schritte](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [Erste Schritte mit Windows Virtual Machines](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/)

Achten Sie darauf, dass die neue Version der Azure-Portal oder Azure Marketplace zu verwenden. Einige Images sind nicht verfügbar, wenn Sie dem Azure-Katalog im klassischen Portal durchsuchen.

**Erstellen des virtuellen Computers**

1. Öffnen Sie das Azure Portal: [portal.azure.com](https:portal.azure.com).

2. Klicken Sie auf **VMs**, oder klicken Sie auf **neu**.

3. Klicken Sie auf **Hinzufügen**.

4. Geben Sie im Suchfeld am oberen Rand der Seite "Machine Learning-Server" oder "SQL Server", um eine Liste der zugehörigen virtuellen Maschinen finden Sie unter.

5. Überprüfen Sie die Anforderungen, und klicken Sie auf **erstellen** um zu beginnen.

6. Nachdem die virtuelle Maschine erstellt wurde und ausgeführt wird, klicken Sie auf die **verbinden** Schaltfläche, um eine Verbindung zu öffnen, und melden Sie sich mit dem neuen Computer.

5. Nachdem Sie eine Verbindung herstellen, können Sie zusätzliche R oder Python-Pakete installieren oder Konfigurieren von Ihrem bevorzugten Entwicklungstool.

### <a name="connect-to-the-virtual-machine"></a>Verbinden mit dem virtuellen Computer

Die Möglichkeit, die ein Client mit SQL Server ausgeführt wird, auf einem virtuellen Computer verbindet unterscheidet sich je nach Speicherort des Clients und die Netzwerkkonfiguration.

Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einer SQL Server-Computer in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-connect).

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

Dieser Abschnitt enthält einige häufig gestellte Fragen zu den Machine learning-virtuellen Computern von Microsoft.

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>Kann ich einen virtuellen Computer mit SQL Server-2017 installieren?

Eine Windows-basierte virtuelle Maschine für SQL Server 2017 Enterprise Edition, die Machine Learning Services umfasst steht ab November 2017. 

Ankündigungen zu neuen Data Science virtuellen Maschinen überwachen Sie diese Blog-Websites:

+ [Cortana Intelligence und Machine Learning](https://blogs.technet.microsoft.com/machinelearning/)
+ [Data Platform Insider](https://blogs.technet.microsoft.com/dataplatforminsider/)

### <a name="adding-sql-server-to-an-existing-virtual-machine"></a>Hinzufügen von SQL Server zu einer vorhandenen virtuellen Maschine

Zusätzlich zur Erstellung einer virtuellen Maschine mithilfe eines Images, die bereits enthält SQL Server-Machine learning können Sie SQL Server auf einer vorhandenen virtuellen Maschine installieren und Machine learning-Funktionen aktivieren. Es wird empfohlen, Enterprise oder Developer Edition, um ressourceneinschränkungen zu vermeiden. Installation erfordert auch, dass Sie Ihren eigenen Lizenzschlüssel verwenden.

Wenn Sie Setup ausführen, achten Sie darauf, dass Sie die Machine learning-Funktion und mindestens eine Sprache (R oder Python) auswählen. Einige zusätzliche Schritte sind erforderlich zum Aktivieren der Machine Learning-Dienste für die Kommunikation mit SQL Server und Netzwerk auf dem virtuellen Computer aktiviert.

Weitere Informationen finden Sie unter [Installing SQL Server R Services auf einem virtuellen Azure-Computer](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md).

### <a name="using-machine-learning-in-azure-sql-database"></a>Verwenden von Machine Learning in Azure SQL-Datenbank

Die Vorschau des R-Unterstützung in SQL Azure wird derzeit für laufende Entwicklungen angehalten. Weitere Informationen finden Sie unter [Azure SQL-Datenbank](../r/using-r-in-azure-sql-database.md).

### <a name="can-i-upgrade-the-sql-server-version-on-a-virtual-machine"></a>Kann ich die SQL Server-Version auf einem virtuellen Computer aktualisiere?

Auch die SQL Server 2016-Images R, unterstützt, wenn Sie Python verwenden möchten, können Sie auf SQL Server 2017 aktualisieren, die dadurch auch anderen Machine learning-Komponenten aktualisiert.

Um die Version von SQL Server aktualisieren, die installiert ist, öffnen Sie das SQL Server-Installationscenter auf der virtuellen Maschine, und wählen die **Upgrade** Option. Je nach dem Virtual Machine kann Sie erstellt haben, eine Lizenz erforderlich sein.

Weitere Informationen finden Sie unter [Aktualisieren von SQL Server mithilfe des Installations-Assistenten](https://docs.microsoft.com/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup).

### <a name="can-i-upgrade-just-the-machine-learning-components"></a>Kann ich nur Machine learning Komponenten aktualisiere?

Wenn neue Updates für "revoscaler", MicrosoftML oder Revoscalepy veröffentlicht werden, können Sie Machine learning-Komponenten, die von SQL Server verwendet werden, mithilfe der genannten aktualisieren _Bindung_. Dies ändert nicht Ihre SQL Server-Version, aber es ändert die Supportrichtlinie für die Instanz.

Weitere Informationen finden Sie unter [verwenden SqlBindR Machine Learning-Komponenten auf SQL Server Upgrade](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>Wie greife ich auf Daten im Azure Storage-Konto zu?

Wenn Sie Daten aus Ihrem Azure-Konto verwenden möchten, stehen mehrere Optionen für den Zugriff auf die Daten oder zum Verschieben der Daten zur Verfügung:

+ Kopieren Sie die Daten aus dem Speicherkonto mit einem Hilfsprogramm wie [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)in das lokale Dateisystem. 

+ Fügen Sie die Dateien zu einer Dateifreigabe des Speicherkontos hinzu, und binden Sie anschließend die Dateifreigabe als Netzlaufwerk auf Ihrem virtuellen Computer ein. Weitere Informationen finden Sie unter [Einbinden von Azure-Dateien](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/). 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>Wie verwende ich Daten aus Azure Data Lake Storage (ADLS)?

Sie können die Daten lesen, aus dem ADLS-Speicher mithilfe von "revoscaler", unter Verwendung von WebHDFS auf um das Speicherkonto, das die gleiche Weise wie würden Sie eine HDFS-Dateisystem zu verweisen. Weitere Informationen finden Sie im Artikel: [mithilfe von R für FileSystem-Vorgänge auf Azure Data Lake-Speicher](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/).

### <a name="i-cant-find-the-rre-virtual-machine"></a>Die RRE virtuelle Maschine kann nicht gefunden werden.

Die "RRE für Windows-VM", die gab es zuvor in den Azure Marketplace wurde ersetzt durch das Image "Machine Learning-Server für Windows".

Machine Learning-Server-Images sind auch für CentOS Linux-Version 7.2 Linux RedHat Version 7.2 und Ubuntu, Version 16.04 verfügbar.

Weitere Informationen finden Sie unter [Machine Learning-Server in der Cloud](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-in-the-cloud)

### <a name="configuring-machine-learning-server-or-r-server-to-support-web-services"></a>Konfigurieren von Machine Learning-Server oder R-Server zur Unterstützung von Webdiensten

Wenn Sie einen virtuellen Computer verwenden, der Machine Learning-Server enthält, möglicherweise zusätzliche Konfigurationsschritte erforderlich, Web Service-Bereitstellung, Remoteausführung, oder verwenden den virtuellen Computer als Bereitstellungsserver in Ihrer Organisation sein.

Anweisungen hierzu finden Sie unter [Konfigurieren von Machine Learning-Servers Analytics operationalisieren von](https://docs.microsoft.com/machine-learning-server/operationalize/configure-machine-learning-server-one-box).

Wenn Sie nur Pakete, z. B. "revoscaler" oder MicrosoftML verwenden möchten, ist keine zusätzliche Konfiguration erforderlich.

## <a name="bkmk_list"></a>Liste der virtuellen Computer

Derzeit sind die folgenden virtuellen Maschinen für maschinelles Lernen mit SQL Server verfügbar:

|Name| Kommentare|
|----|----|----|
| **SQL Server 2016**| ***  |
|SQL Server 2016 SP1 Enterprise unter Windows|R-Services integrierten erweiterten Analysen.|
|BYOL SQL Server 2016 SP1 Enterprise unter WindowsServer |R-Services integrierten erweiterten Analysen. |
|Kostenlose Lizenz: SQL Server 2016-SP1-Entwickler auf WindowsServer 2016 |R-Services integrierten erweiterten Analysen. |
| Data Science Virtual Machine - Windows 2012|Enthält die gängigen Tools für Data Science, einschließlich Microsoft R Server Developer Edition, SQL Server 2016 Developer Edition, Python Anaconda-Verteilung, Julia Pro Developer Edition und Jupyter Notebooks für r| 
| Data Science Virtual Machine - Windows-2016|Enthält SQL Server 2016 Developer Edition mit Unterstützung für R-Analysen in der Datenbank an.|
|**SQL Server 2017**| ***   |
|SQL Server 2017 Enterprise Windows Server 2016| Machine Learning-Dienste mit Unterstützung für Python und R-Sprache.|
|BYOL SQL Server 2017 Enterprise, WindowsServer 2016|Machine Learning-Dienste mit Unterstützung für Python und R-Sprache.|
| Freien SQL Server-Lizenz: Entwickler SQL Server 2017 unter WindowsServer|Machine Learning-Dienste mit Unterstützung für Python und R-Sprache.|
| **Andere**| *** |
| Machine Learning-Server nur SQL Server 2017 Enterprise|Ähnlich wie in der SQL Server 2016 Enterprise-Image, aber die eigenständige Version des Machine Learning-Server und enthält den Kern ScaleR und Operationalisierung Funktionalität optimiert für Windows-Umgebungen.|
| Machine Learning-Server unter Windows|Enthält die eigenständige Version des Machine Learning-Servers mit operationalisierung-Funktionen, die für die Windows-Umgebung optimiert.|
|Data Science Virtual Machine |Linux-Editionen sind R-Server. Virtuelle Linux-Computer, die SQL Server-2017 enthalten kann nicht R oder Python-Code in SQL Server ausgeführt werden. Allerdings können Sie die Bewertung auf einem trainierten Modell mit der VORHERSAGE von T-SQL-Funktion ausführen. Weitere Informationen finden Sie unter [in SQl Server Native Bewertung](../sql-native-scoring.md).|
