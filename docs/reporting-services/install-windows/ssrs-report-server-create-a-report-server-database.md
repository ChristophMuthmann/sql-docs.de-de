---
title: Erstellen eine Berichtsserver-Datenbank (SSRS-Konfigurations-Manager) | Microsoft Docs
ms.custom: 
ms.date: 05/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], databases
- report server database
- databases [Reporting Services], creating
ms.assetid: 8a3a6ffe-4001-46be-8548-94532550f6a5
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 526abc46fe3b7fc3f923c29f4b4857b06f55a37c
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---

# <a name="create-a-report-server-database"></a>Erstellen einer Berichtsserver-Datenbank

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**Im einheitlichen Modus** verwendet zwei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relationale Datenbanken zum Speichern von Berichtsserver-Metadaten und Objekte. Eine Datenbank, die als primärer Speicher dient, und eine zweite Datenbank zum Speichern temporärer Daten. Die Datenbanken werden zusammen erstellt und sind namentlich aneinander gebunden. Bei einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Standardinstanz werden die Datenbanken als **reportserver** und **reportservertempdb**benannt. Zusammen werden die beiden Datenbanken als "Berichtsserver-Datenbank" oder "Berichtsserver-Katalog" bezeichnet.

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**SharePoint-Modus** schließt eine dritte Datenbank, die für datenwarnungsmetadaten verwendet wird. Die drei Datenbanken werden für jede [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung erstellt, und die Datenbanknamen enthalten standardmäßig einen GUID, der die Dienstanwendung darstellt. Im Folgenden finden Sie Beispielnamen der drei Datenbanken im SharePoint-Modus:

-   ReportingService_90a9f37075544f22953c4a62e4a9f370  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370TempDB  
  
-   ReportingService_90a9f37075544f22953c4a62e4a9f370_Alerting  
  
> [!IMPORTANT]  
>  Schreiben Sie keine Anwendungen, um Abfragen auf der Berichtsserver-Datenbank auszuführen. Die Berichtsserver-Datenbank ist kein öffentliches Schema. Die Tabellenstruktur kann sich von einer Version zur nächsten ändern. Verwenden Sie für den Zugriff auf die Berichtsserver-Datenbank stets [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -APIs, wenn Sie eine Anwendung schreiben, die auf die Berichtsserver-Datenbank zugreifen muss.  
>   
>  Dies gilt nicht für die Ausführungsprotokollsichten. Weitere Informationen finden Sie unter [Berichtsserverausführungsprotokoll und die ExecutionLog3-Ansicht](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
## <a name="ways-to-create-the-report-server-database"></a>Möglichkeiten zum Erstellen der Berichtsserver-Datenbank  
 **Einheitlicher Modus** : Sie können die Berichtsserver-Datenbank im einheitlichen Modus wie folgt erstellen:  
  
-   Automatisch: Verwenden Sie den Setup-Assistenten für SQL Server, wenn Sie die Installationsoption für die Standardkonfiguration auswählen. Im SQL Server-Installations-Assistenten ist dies die Option **Installieren und konfigurieren** auf der Seite Berichtsserver-Installationsoptionen. Wenn Sie die Option **Nur installieren** auswählen, müssen Sie die Datenbank mithilfe des Reporting Services-Konfigurations-Managers erstellen.  
  
-   Manuell: Verwenden Sie den Konfigurations-Manager für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Sie müssen die Berichtsserver-Datenbank manuell erstellen, wenn Sie zum Hosten der Datenbank Remote-[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] verwenden. Weitere Informationen finden Sie unter [Erstellen einer Berichtsserver-Datenbank im einheitlichen Modus &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
 **SharePoint-Modus** : Die Seite Berichtsserver-Installationsoptionen besitzt nur eine Option für den SharePoint-Modus von **Nur installieren**. Diese Option installiert alle [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dateien und den gemeinsamen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst. Der nächste Schritt besteht darin mindestens eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung in einer der folgenden Methoden zu erstellen:  
  
-   Verwenden Sie die SharePoint-Zentraladministration, um eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung zu erstellen. Weitere Informationen finden Sie im Abschnitt "Dienstanwendung" in [Step 3: Create a Reporting Services Service Application](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_create_serrviceapplication).  
  
-   Verwenden Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -PowerShell-Cmdlets zum Erstellen einer Dienstanwendung und der Berichtsserver-Datenbanken. Weitere Informationen finden Sie im Beispiel für die Erstellung von Dienstanwendungen im Thema [PowerShell-Cmdlets für SharePoint-Modus von Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
## <a name="database-server-version-requirements"></a>Anforderungen für die Datenbankserver-Version  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird zum Hosten der Berichtsserver-Datenbanken verwendet. Die Instanz [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] kann eine lokale oder eine Remoteinstanz sein. Im Folgenden finden Sie die unterstützten Version von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , die zum Hosten der Berichtsserver-Datenbanken verwendet werden können.  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 Wenn Sie die Berichtsserver-Datenbank auf einem Remotecomputer erstellen, müssen Sie die Verbindung so konfigurieren, dass ein Domänenbenutzerkonto oder ein Dienstkonto mit Netzwerkzugriff verwendet wird. Wenn Sie eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Remoteinstanz verwenden, sollten Sie sorgfältig überlegen, welche Anmeldeinformationen der Berichtsserver für die Verbindung zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz verwenden soll. Weitere Informationen finden Sie unter [Konfigurieren einer Berichtsserver-Datenbankverbindung &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
> [!IMPORTANT]  
>  Der Berichtsserver und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz, die die Berichtsserver-Datenbank hostet, können sich in verschiedenen Domänen befinden. Bei einer Internetbereitstellung ist es üblich, einen Server zu verwenden, der sich hinter einer Firewall befindet. Wenn Sie einen Berichtsserver für den Internetzugriff konfigurieren, sollten Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldeinformationen verwenden, um die Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz hinter der Firewall herzustellen, und IPSec zum Schützen dieser Verbindung.  
  
## <a name="database-server-edition-requirements"></a>Anforderungen für die Datenbankserver-Edition  
 Wenn Sie eine Berichtsserver-Datenbank erstellen, sollten Sie beachten, dass nicht alle Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Hosten der Datenbank verwendet werden können. Weitere Informationen finden Sie im Abschnitt „Anforderungen für die Berichtsserver-Datenbankserver-Edition“ in [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  

## <a name="next-steps"></a>Nächste Schritte

[Konfigurations-Manager für Reporting Services](http://msdn.microsoft.com/en-us/63519ef4-e68a-42fb-9cf7-31228ea4e434)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
