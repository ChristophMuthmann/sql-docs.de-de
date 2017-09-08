---
title: "R Server (eigenständig) | Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/22/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: ca9e48f1-67b8-4905-9b78-56752d7a4e81
caps.latest.revision: 22
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1812dc6b60e5f5ee4547810a591b37643be17096
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="r-server-standalone"></a>R-Server (eigenständig)

Microsoft SQL Server 2016 bereitgestellt **R Server (eigenständig)**, im Rahmen der Plattform für die Unterstützung von Enterprise-Klasse Analytics.  Microsoft R Server bietet Skalierbarkeit und Sicherheit für die Sprache "R" und behebt die in-Memory-Einschränkungen von open Source-R. Wie SQL Server R Services bietet Microsoft R Server (eigenständig) parallel und aufgeteilte Verarbeitung von Daten, damit R-Benutzer Daten sehr viel größer als die in den Arbeitsspeicher passen können zu verwenden.

In SQL Server 2017 wurde Unterstützung für die Sprache Python hinzugefügt bietet umfassende Unterstützung in der Computer-Community learning und enthält häufig Bibliotheken für Textanalyse und umfassenden lernen.  Entsprechend diesem größeren Satz der Sprachen, wir haben auch umbenannt **Microsoft Machine Learning-Server (eigenständig)**.

## <a name="benefits-of-microsoft-r-server"></a>Vorteile von Microsoft R Server

Sie können Microsoft R Server für verteilte Datenverarbeitung auf mehreren Plattformen verwenden. Bei der Installation von SQL Server-Setup erhalten Sie den Windows-basierten Server und die erforderlichen Tools für die publishing und Bereitstellen von Modellen. Weitere Informationen zu anderen Plattformen finden Sie in folgenden Ressourcen in der MSDN Library:

+ [Einführung von Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)
+ [R Server für Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)

Sie können auch installieren Microsoft R Server, als Client Entwicklung, zum Abrufen der "revoscaler"-Bibliotheken und Tools, die erforderlich sind, um R-Lösungen zu erstellen, die auf SQL Server bereitgestellt werden können.

## <a name="whats-new-in-microsoft-machine-learning-server"></a>Neuigkeiten in Microsoft Machine Learning-Server

Bei der Installation von Machine Learning Services (eigenständig) mithilfe des SQL Server-2017-Setups müssen Sie jetzt die Möglichkeit, die Sprache Python hinzuzufügen. Natürlich ist die Sprache "R" ist noch eine unterstützte Option, und Sie können auch beide Sprachen installieren, falls gewünscht.
 
In SQL Server 2017 CTP 2.0 umfasst die Serverinstallation auch das Paket Mrsdeploy und anderen Dienstprogrammen für operationalisieren Modelle verwendet. Weitere Informationen finden Sie unter [Operationalisierung mit Mrsdeploy](../../advanced-analytics/operationalization-with-mrsdeploy.md).

Enterprise-Benutzer von SQL Server-Machine Learning können die herunterladbare Installationsprogramme für Microsoft R Server so aktualisieren Sie ihre R-Komponenten in einem Prozess, der als Bindung bezeichnet wird. Weitere Informationen finden Sie unter [SqlBindR verwenden, für die Aktualisierung und SQL Server-Instanz](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

## <a name="get-microsoft-r-server-or-machine-learning-server-standalone"></a>Abrufen von Microsoft R Server "oder" Machine Learning-Server (eigenständig)

 Es gibt mehrere Optionen für die Installation von Microsoft R Server:

+ Verwenden Sie den SQL Server-Setup-Assistenten

  [Erstellen eines eigenständigen R-Servers](../r/create-a-standalone-r-server.md)

  Führen Sie SQL Server 2016-Setup zur Installation **Microsoft R Server (eigenständig)**. Standardmäßig wird die Sprache "R" hinzugefügt.
  Oder führen Sie 2017 von SQL Server-Setup zum Installieren von **Machine Learning-Server (eigenständig)** , und wählen Sie entweder R Python oder sogar beides.

  > [!IMPORTANT]
  > Die Option zur Installation des Servers befindet sich in der **gemeinsam genutzte Funktionen** Setup im Abschnitt. Installieren Sie keine anderen Komponenten.
  >
  > Installieren Sie den Server, nicht auf einem Computer, auf dem SQL Server R Services oder SQL Server-Machine Learning-Services installiert wurde.

+ Verwenden Sie Befehlszeilenoptionen für SQL Server-setup

  [Installieren von Microsoft R Server über die Befehlszeile](../r/install-microsoft-r-server-from-the-command-line.md)

  SQL Server-Setup unterstützt unbeaufsichtigte Installationen über einen umfangreichen Satz von Befehlszeilenargumenten.

+ Verwenden Sie das eigenständige Installationsprogramm

  [Ausführen von Microsoft R Server für Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows).

  Sie können jetzt eine neue Windows Installer verwenden, So richten Sie eine neue Instanz von Microsoft R Server oder Microsoft Machine Learning-Servers ein.  Microsoft R Server (und Microsoft Machine Learning-Server) erfordert eine SQL Server-Enterprise Agreement. Allerdings nach dem Ausführen der eigenständiges Installationsprogramm wird die Supportrichtlinie für eine vorhandene Installation aktualisiert und die neue moderne Lifecycle-Richtlinie verwenden. Diese Support-Option wird sichergestellt, dass Updates für Machine Learning-Komponenten häufiger angewendet werden als dies der Fall wäre, bei Verwendung von SQL Server-Dienst-Versionen.

  
+ Aktualisieren einer SQL Server-Instanz

  [Verwenden zum Aktualisieren einer Instanz von R Services SqlBindR](./use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).
  
  Das eigenständige Installationsprogramm können zum Aktualisieren einer Instanz von SQL Server 2016-R-Services verwenden die neueste Version von r Wenn Sie das Installationsprogramm ausführen, die Supportrichtlinie für moderne Lebenszyklus wird an den Server angewendet werden, und die R-Komponenten erhalten häufiger aktualisiert.
  
  > [! Hinweis} ist dieser Update-Methode derzeit nur für vorhandene Installationen von SQL Server 2016 verfügbar. Upgrades werden jedoch in Zukunft für SQL Server-2017 unterstützt werden.

## <a name="related-machine-learning-products"></a>Verwandte Machine learning-Produkte

+ Virtuelle Computer in Azure mit R-Server

  [Bereitstellen eines virtuellen Computers des R-Server](../../advanced-analytics/r-services/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
  
  Azure Marketplace enthält mehrere Images für virtuelle Computer, die R-Server enthalten. Erstellen eines neuen virtuellen Computers für R-Server in Microsoft Azure ist die schnellste Möglichkeit zum Einrichten eines Servers für die Entwicklung und Bereitstellung von Vorhersagemodellen verwenden. Bilder verfügen über Funktionen für die Skalierung und Freigabe bereits konfiguriert, wodurch R Analytics in Anwendungen eingebettet und Integration von R mit Back-End-Systemen vereinfacht.

+ Data Science Virtual Machine

  [Data Science Virtual Machine - Windows 2016 Preview](http://aka.ms/dsvm/win2016)

  Die neueste Version der Data Science Virtual Machine enthält R-Server, SQL Server, und ein Array der beliebtesten Tools für Machine Learning alle vorinstalliert und getestet. Jupyter Notizbüchern erstellen, Entwickeln von Projektmappen in Julia und GPU-aktivierte umfassenden lernen Bibliotheken wie MXNet, CNTK und TensorFlow verwenden.

## <a name="resources"></a>Ressourcen

Beispiele, Lernprogramme und Weitere Informationen zu Microsoft R Server, finden Sie unter [Microsoft R-Produkte](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started).

## <a name="see-also"></a>Siehe auch

 [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)


