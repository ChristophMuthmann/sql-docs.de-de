---
title: Installieren Sie Sample Data and Projects | Microsoft Docs
ms.custom: 
ms.date: 02/02/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: fc475b25-cbb2-408a-901f-9299299538c5
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: af6002ed27aabacf1b9e9a08cf3e659559daf5f5
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="install-sample-data-and-multidimensional-projects"></a>Installieren von Beispieldaten und mehrdimensionale Projekte 
[!INCLUDE[ssas-appliesto-sqlas-all](../includes/ssas-appliesto-sqlas-all.md)]

Verwenden Sie die Anweisungen und Links in diesem Thema, um die Daten- und Projektdateien-Dateien, die in der Analysis Services-Lernprogrammen verwendet installieren.  Wenn Sie das mehrdimensionale Lernprogramm abschließen, müssen Sie nur die Beispielprojekte zu installieren, wenn Sie möchten ein vollständig abgeschlossenes Projekt mit dem verglichen werden soll, die Sie in diesem Lernprogramm erstellen.
  
## <a name="step-1-install-sql-server-software"></a>Schritt 1: Installieren der SQL Server-Software  
In den Lektionen dieses Lernprogramms wird vorausgesetzt, dass Sie folgende Software installiert haben. Sie können alle Funktionen auf einem einzelnen Computer installieren. Um diese Funktionen zu installieren, führen Sie SQL Server-Setup aus, und wählen Sie auf der Seite Funktionsauswahl diese Funktionen aus.  
  
-   Datenbankmodul  
  
-   Analysis Services  
  
    Analysis Services ist nur in der Evaluation, Enterprise, Business Intelligence und Standard Edition verfügbar.  
  
    Standardmäßig wird der Analysis Services 2016 und höher als tabellarische Instanz, die Sie überschreiben können, durch Auswählen von mehrdimensionalen Servermodus auf dem Server Konfigurationsseite des Installations-Assistenten installiert. Falls Sie beide Servermodi ausführen möchten, führen Sie SQL Server-Setup auf demselben Computer erneut aus, um eine zweite Analysis Services-Instanz im anderen Modus zu installieren.  
  
-   [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)  
  
Sie können Excel optional installieren, um mehrdimensionale Daten zu durchsuchen, während Sie das Lernprogramm ausführen. Durch die Installation von Excel wird die Funktion **In Excel analysieren** aktiviert. Diese startet Excel mit einer PivotTable-Feldliste, die mit dem Cube verbunden ist, den Sie erstellen. Es wird empfohlen, zum Durchsuchen von Daten Excel zu verwenden, da Sie schnell einen Pivotbericht erstellen können, der Ihnen das Interagieren mit den Daten ermöglicht.  
  
Alternativ können Sie Daten mithilfe des integrierten MDX-Abfrage-Designers durchsuchen, der in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]integriert ist. Der Abfrage-Designer gibt die gleichen Daten zurück, jedoch werden die Daten als flaches Rowset dargestellt.  
  
## <a name="step-2-download-sql-server-data-tools-for-visual-studio"></a>Schritt 2: Herunterladen von SQL Server Datatools für Visual Studio 
In dieser Version wird SQL Server Data Tools getrennt von anderen SQL Server-Funktionen heruntergeladen und installiert. Der Designer und Projektvorlagen zum Erstellen von BI-Modelle und Berichte sind in enthalten SSDT für Visual Studio 2015 oder als [NuGet-Pakete](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) für Visual Studio-2017.  
  
-   [Laden Sie SQL Server Data Tools (SSDT) herunter](http://go.microsoft.com/fwlink/?LinkID=827542). Die Datei wird im Ordner Downloads gespeichert. Führen Sie Setup aus, um das Tool zu installieren.  
  
## <a name="step-3-install-databases"></a>Schritt 3: Installieren von Datenbanken  
In einem mehrdimensionalen Analysis Services-Modell werden Transaktionsdaten verwendet, die Sie aus einem Managementsystem für relationale Datenbanken importieren. In diesem Lernprogramm verwenden Sie die folgende relationale Datenbank als Datenquelle.  
  
-   **AdventureWorksDW 2012 oder höher** – Dies ist ein relationales Datawarehouse, die auf eine Datenbankmodulinstanz ausgeführt wird. Es enthält die ursprünglichen Daten, die in den Analysis Services-Datenbanken und -Projekten verwendet werden, die Sie im gesamten Lernprogramm erstellen und bereitstellen.  
  
    Sie können diese Beispieldatenbank mit [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] und höher. Im Allgemeinen sollten Sie die Beispiel-Datenbankversion Abgleich Ihrer Datenbank-Engine-Version verwenden.
  
Um die Datenbank zu installieren, führen Sie folgende Schritte aus:  
  
1.  Herunterladen einer [AdventureWorkDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) datenbanksicherung von GitHub.  
  
2.  Kopieren Sie die Sicherungsdatei in das Datenverzeichnis der lokalen SQL Server-Datenbankmodul-Instanz.
  
3.  Starten Sie SQL Server Management Studio, und stellen Sie eine Verbindung mit der Datenbankmodul-Instanz her.  
  
4.  Stellen Sie die Datenbank wieder her.  
  
## <a name="step-4-grant-database-permissions"></a>Schritt 4: Gewähren von Datenbankberechtigungen  
In den Beispielprojekten werden Einstellungen für den Datenquellenidentitätswechsel verwendet, die den Sicherheitskontext angeben, unter dem Daten importiert oder verarbeitet werden. Standardmäßig geben die Identitätswechseleinstellungen das Analysis Services-Dienstkonto für den Zugriff auf die Daten an. Um diese Standardeinstellung zu verwenden, müssen Sie sicherstellen, dass das Dienstkonto, unter dem Analysis Services ausgeführt wird, datenleserberechtigungen verfügt, auf die **AdventureWorksDW2014** Datenbank.  
  
> [!NOTE]  
> Um den Lerneffekt zu verbessern, wird empfohlen, die standardmäßige Identitätswechseloption für das Dienstkonto zu verwenden und dem Dienstkonto in SQL Server Datenleserberechtigungen zu erteilen. Es sind zwar weitere Identitätswechseloptionen verfügbar, jedoch sind nicht alle von ihnen für Verarbeitungsvorgänge geeignet. Insbesondere wird die Option zum Verwenden der Anmeldeinformationen des aktuellen Benutzers nicht für Verarbeitungsvorgänge unterstützt.  
  
1.  Bestimmen Sie das Dienstkonto. Sie können Kontoinformationen mit dem SQL Server-Konfigurations-Manager oder der Konsolenanwendung Dienste anzeigen. Wenn Sie Analysis Services als Standardinstanz installiert haben, wird der Dienst als **NT Service\MSSQLServerOLAPService**ausgeführt.  
  
2.  Stellen Sie in Management Studio eine Verbindung mit der Datenbankmodul-Instanz her.  
  
3.  Erweitern Sie den Knoten Sicherheit, klicken Sie mit der rechten Maustaste auf Anmeldungen, und wählen Sie **Neue Anmeldung**aus.  
  
4.  Geben Sie auf der Seite Allgemein in Anmeldename den Namen **NT Service\MSSQLServerOLAPService** (bzw. den Namen des Kontos, unter dem der Dienst ausgeführt wird) ein.  
  
5.  Klicken Sie auf **Benutzerzuordnung**.  
  
6.  Aktivieren Sie das Kontrollkästchen neben den **AdventureWorksDW2014** Datenbank. Zu den Mitgliedern der Rolle sollten automatisch **db_datareader** und **public**gehören. Klicken Sie auf **OK** , um die Standardeinstellungen zu übernehmen.  
  
## <a name="step-5-install-projects"></a>Schritt 5: Installieren von Projekten  

Die Beispielprojekte sind nur notwendig, für den Vergleich mit, was Sie im Lernprogramm mehrdimensionale Modellierung erstellen. Diese sind nicht erforderlich, um das Lernprogramm abzuschließen.
  
1.  Herunterladen der [Adventure-Works – mehrdimensionale-Modell-project.zip](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks-analysis-services) aus der Adventure Works für Analysis Services-Beispielseite auf GitHub.  
  
    Dieses Projekt funktioniert für SSAS 2014 und höheren Versionen.  
  
2.  Verschieben Sie die ZIP-Datei in einen Ordner direkt unterhalb des Stammlaufwerks (beispielsweise C:\Tutorial). Dieser Schritt bewirkt, dass weniger Fehler der Art "Pfad zu lang" auftreten; diese werden manchmal ausgegeben, wenn Sie versuchen, die Dateien in den Ordner Downloads zu entzippen.  
  
3.  Entzippen der Beispielprojekte: Klicken Sie mit der rechten Maustaste auf die Datei, und wählen Sie **Alle extrahieren**aus. 
  
4.  Entfernen Sie den Schreibschutz dieser Dateien. Mit der rechten Maustaste in des übergeordneten Ordners, wählen Sie **Eigenschaften**, und deaktivieren Sie das Kontrollkästchen **schreibgeschützte**. Klicken Sie auf **OK**. Wenden Sie die Änderungen auf diesen Ordner sowie Unterordner und Dateien an.  

5.  Öffnen Sie die Projektmappendatei (sln) in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
6.  Stellen Sie die Projektmappe bereit, um zu überprüfen, ob die Datenbankberechtigungen und die Informationen zum Serverspeicherort ordnungsgemäß eingerichtet sind.  
  
    Wenn Analysis Services und das Datenbankmodul als Standardinstanz (MSSQLServer) installiert sind und sämtliche Software auf demselben Computer ausgeführt wird, können Sie im Menü Erstellen auf **Projektmappe bereitstellen** klicken, um das Beispielprojekt zu erstellen und auf der lokalen Instanz von Analysis Services bereitzustellen. Während der Bereitstellung, Daten werden verarbeitet (oder nicht importiert) aus der **AdventureWorksDW** Datenbank auf dem lokalen Datenbankmodulinstanz her. Auf der Analysis Services-Instanz, die die vom Datenbankmodul abgerufenen Daten enthält, wird eine neue Analysis Services-Datenbank erstellt.  
  
    Wenn Fehler auftreten, überprüfen Sie die vorherigen Schritte zum Einrichten von Datenbankberechtigungen. Zusätzlich müssen u. U. auch Servernamen geändert werden. Der Standardservername lautet "localhost". Wenn die Server auf Remotecomputern oder als benannte Instanzen installiert werden, müssen Sie den Standardnamen mit einem für Ihre Installation gültigen Servernamen überschreiben. Wenn sich die Server auf Remotecomputern befinden, müssen Sie möglicherweise außerdem die Windows-Firewall so konfigurieren, dass sie den Zugriff auf die Server zulässt.  
  
    Der Servername für Verbindungen mit dem Datenbankmodul wird im Datenquellenobjekt der mehrdimensionalen Projektmappe (Adventure Works-Lernprogramm) angegeben und im Projektmappen-Explorer angezeigt.  
  
    Der Servername für Verbindungen mit Analysis Services wird in den Eigenschaftenseiten des Projekts auf der Registerkarte Bereitstellung angegeben und ebenfalls im Projektmappen-Explorer angezeigt.  
  
7.  Stellen Sie in SQL Server Management Studio eine Verbindung mit Analysis Services her. Überprüfen Sie, ob auf dem Server eine Datenbank mit dem Namen **Analysis Services Tutorial** ausgeführt wird.  
  
## <a name="next-step"></a>Nächster Schritt  
Jetzt können Sie das Lernprogramm verwenden. Weitere Informationen für den Einstieg finden Sie unter [Mehrdimensionale Modellierung &#40;Adventure Works-Tutorial&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md).  
  
## <a name="see-also"></a>Siehe auch  
[Konfigurieren der Windows-Firewall, um den Zugriff auf Analysis Services zuzulassen](../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
[Configure the Windows Firewall to Allow SQL Server Access](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  