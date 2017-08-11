---
title: "Implementieren einer Connection-Klasse für eine Datenverarbeitungserweiterung | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- connections [Reporting Services], data processing extensions
- Connection class
- data processing extensions [Reporting Services], connections
ms.assetid: 7047d29e-a2c9-4e6f-ad02-635851a38ed7
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 19f059c0041cc9effc48e0db9c4b5ef1a504d020
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="implementing-a-connection-class-for-a-data-processing-extension"></a>Implementieren einer Connection-Klasse für Datenverarbeitungserweiterungen
  Die **Verbindung** Objekt stellt eine datenbankverbindung oder ähnliche Ressource dar und ist der Ausgangspunkt für Benutzer von einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] -datenverarbeitungserweiterung. Es stellt Verbindungen zum Datenbankserver, dar, obwohl jede Entität mit ähnlichem Verhalten als verfügbar gemacht werden kann ein **Verbindung**.  
  
 Implementiert eine **Verbindung** Objekt, erstellen Sie eine Klasse, die implementiert <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> und implementiert optional <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>.  
  
 Sie müssen in Ihrer Implementierung sicherstellen, dass eine Verbindung erstellt und geöffnet wird, bevor die Befehle ausgeführt werden können. Stellen Sie in Ihrer Implementierung sicher, dass Clients die Verbindungen ausdrücklich (und nicht implizit) öffnen und schließen. Führen Sie die Sicherheitsprüfungen aus, wenn die Verbindung hergestellt wird. Dadurch, dass eine Verbindung für die anderen Klassen in der [!INCLUDE[ssRS](../../../includes/ssrs-md.md)]-Datenverarbeitungserweiterung vorhanden sein muss, wird sichergestellt, dass bei der Arbeit mit Ihrer Datenquelle stets Sicherheitsprüfungen durchgeführt werden.  
  
 Die Eigenschaften der gewünschten Verbindung werden als Verbindungszeichenfolge dargestellt. Die [!INCLUDE[ssRS](../../../includes/ssrs-md.md)]-Datenverarbeitungserweiterungen sollten unbedingt die Eigenschaft <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection.ConnectionString%2A> unterstützen und das bekannte Name/Wert-Paar verwenden, das von der OLE DB definiert ist.  
  
> [!NOTE]  
>  **Verbindung** Objekte sind häufig ressourcenintensiver abgerufen werden, daher Sie berücksichtigen sollten, pooling der Verbindungen oder andere Techniken, mit denen dieses Problem zu minimieren.  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> erbt von <xref:Microsoft.ReportingServices.Interfaces.IExtension>. Sie müssen die <xref:Microsoft.ReportingServices.Interfaces.IExtension>-Schnittstelle als Teil der Implementierung der Verbindungsklassen implementieren. Durch die <xref:Microsoft.ReportingServices.Interfaces.IExtension>-Schnittstelle kann eine Klasse einen lokalisierten Erweiterungsnamen implementieren und erweiterungsspezifische Konfigurationsdaten verarbeiten, die in der [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Konfigurationsdatei gespeichert sind.  
  
 Ihre **Verbindung** Objekt enthält die <xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A> -Eigenschaft durch seine Implementierung von <xref:Microsoft.ReportingServices.Interfaces.IExtension>. Die [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Datenverarbeitungserweiterungen sollten unbedingt die Eigenschaft <xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A> unterstützen, sodass die Benutzer einen bekannten und lokalisierten Namen auf der Benutzeroberfläche, z. B. dem Berichts-Manager, vorfinden.  
  
 <xref:Microsoft.ReportingServices.Interfaces.IExtension>ermöglicht auch die **Verbindung** Objekt abrufen und Verarbeiten von benutzerdefinierten Konfigurationsdaten, die in der Datei "rsreportserver.config" gespeichert. Weitere Informationen zur Verarbeitung benutzerdefinierter Konfigurationsdaten finden Sie in der Methode <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>.  
  
 Die Klasse, mit der <xref:Microsoft.ReportingServices.Interfaces.IExtension> implementiert wird, wird nicht aus dem Arbeitsspeicher entladen, wenn der Rest der Datenverarbeitungserweiterungsklassen entladen wird. Aus diesem Grund können Sie Ihre **Erweiterung** -Klasse verbindungsübergreifende Statusdaten oder Daten, die zwischengespeichert werden, können im Arbeitsspeicher gespeichert. Ihre **Erweiterung** -Klasse verbleibt im Arbeitsspeicher, wie der Berichtsserver ausgeführt wird.  
  
 Sie erweitern, können Ihre **Verbindung** Klasse, um Unterstützung für die Anmeldeinformationen in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] durch die Implementierung <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>. Beim Implementieren der <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.IntegratedSecurity%2A>, <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.UserName%2A>, und <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.Password%2A> Eigenschaften von der <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> -Schnittstelle, Sie können die **integrierte Sicherheit von** das Kontrollkästchen und **Benutzername** und **Kennwort** Textfelder von der **Datenquelle** Dialogfeld im Berichts-Designer. Hierdurch kann der Berichts-Designer die Anmeldeinformationen für Datenquellen speichern und abrufen, die die Authentifizierung unterstützen. Die Anmeldeinformationen werden sicher gespeichert und verwendet, wenn Berichte im Vorschaumodus gerendert werden.  
  
> [!NOTE]  
>  Die Implementierung von <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> erfordert es implizit, dass Sie die Elemente der <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>-Schnittstelle und der <xref:Microsoft.ReportingServices.Interfaces.IExtension>-Schnittstelle implementieren.  
>   
>  Ein Beispiel **Verbindung** -klassenimplementierung, finden Sie unter [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Erweiterungen](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementing a Data Processing Extension](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
