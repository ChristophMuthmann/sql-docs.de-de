---
title: Konnte nicht aktualisiert werden Daten für eine Datenverbindung in der Arbeitsmappe | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c1961c883a5e38c56acf65def83272aa1e5adb8d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="unable-to-refresh-data-for-a-data-connection-in-the-workbook"></a>Daten können nicht für eine Datenverbindung in der Arbeitsmappe aktualisiert werden.
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Excel Services gibt diesen Fehler für Excel-Arbeitsmappen zurück, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten enthalten, wenn es eine Verbindungsanforderung an einen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Server sendet und die Anforderung fehlschlägt.  
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Betrifft:|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Installation|  
|Produktversion|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Ursache|Weitere Informationen finden Sie weiter unten.|  
|Meldungstext|Daten können nicht für eine Datenverbindung in der Arbeitsmappe aktualisiert werden. Versuchen Sie es erneut, oder wenden Sie sich an den Systemadministrator. Die folgenden Verbindungen wurden nicht aktualisiert: [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten|  
  
## <a name="explanation-and-resolution"></a>Erklärung und Behebung  
 Mit Excel Services kann keine Verbindung mit den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten hergestellt werden, bzw. diese Daten können nicht geladen werden. Bedingungen, die zum Auftreten dieses Fehlers führen:  
  
 **Szenario 1: Dienst ist nicht gestartet**  
  
 Die SQL Server Analysis Services-Instanz ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) wurde nicht gestartet. Ein abgelaufenes Kennwort führt zum Anhalten der Ausführung des Diensts. Weitere Informationen zum Ändern des Kennworts finden Sie unter [Konfigurieren von Power Pivot-Dienstkonten](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md) und [Starten oder Beenden eines Power Pivot für SharePoint-Servers](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md).  
  
 **Szenario 2a: Öffnen einer früheren Version der Arbeitsmappe auf dem Server**  
  
 Die Arbeitsmappe, die Sie zu öffnen versuchen, könnte in der SQL Server 2008 R2-Version von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für Excel erstellt worden sein. Höchstwahrscheinlich ist der in der Datenverbindungszeichenfolge angegebene Analysis Service-Datenanbieter nicht auf dem Computer vorhanden, auf dem die Abfrage verarbeitet wird.  
  
 Wenn dies der Fall ist, finden Sie diese Meldung im ULS-Protokoll: "Fehler bei der Aktualisierung für"[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]t Daten "in der Arbeitsmappe '\<URL zur Arbeitsmappe >'", gefolgt von "Kann keine Verbindung hergestellt".  
  
 Um die Version der Arbeitsmappe zu bestimmen, öffnen Sie sie in Excel, und überprüfen Sie, welcher Datenanbieter in der Verbindungszeichenfolge angegeben ist. Eine SQL Server 2008 R2-Arbeitsmappe verwendet MSOLAP.4 als Datenanbieter.  
  
 Um dieses Problem zu umgehen, können Sie die Arbeitsmappe aktualisieren. Alternativ können Sie Clientbibliotheken von der SQL Server 2008 R2-Version von Analysis Services auf den physischen Computern installieren, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint oder Excel Services ausführen. Weitere Informationen finden Sie unter [Installieren des OLE DB-Anbieters für Analysis Services auf SharePoint-Servern](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
 **Szenario 2b: Excel Services werden auf einem Anwendungsserver ausgeführt, der die falsche Version der Clientbibliotheken aufweist**  
  
 Standardmäßig wird von SharePoint Server 2010 die SQL Server 2008-Version vom OLE DB-Anbieter für Analysis Services auf Anwendungsservern installiert, auf denen Excel Services ausgeführt wird. In einer Farm, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenzugriff unterstützt, müssen alle physischen Server, die Anwendungen ausführen, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten anfordern, z.B. Excel Services und [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint, eine höhere Version des Datenanbieters verwenden.  
  
 Server, auf denen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint ausgeführt wird, erhalten automatisch den aktualisierten OLE DB-Datenanbieter. Andere Server, beispielsweise solche, auf denen eine eigenständige Excel Services-Instanz ohne [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint auf dem gleichen Computer ausgeführt wird, müssen für die Verwendung neuerer Clientbibliotheken gepatcht werden. Weitere Informationen finden Sie unter [Installieren des OLE DB-Anbieters für Analysis Services auf SharePoint-Servern](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
 **Szenario 3: Domänencontroller ist nicht verfügbar**  
  
 Eine mögliche Ursache ist, dass kein Domänencontroller verfügbar ist, um die Benutzeridentität zu überprüfen. Ein Domänencontroller ist für den Claims to Windows Token Service erforderlich, um den SharePoint-Benutzer für jede Verbindung zu authentifizieren. c2WTS (Claims to Windows Token Service) verwendet keine zwischengespeicherten Anmeldeinformationen. Er überprüft die Benutzeridentität für jede Verbindung.  
  
 Sie können die Ursache dieses Fehlers überprüfen, indem Sie die SharePoint-Protokolldatei anzeigen. Wenn die SharePoint-Protokolle die Meldung "Fehler beim Abrufen von WindowsIdentity aus IClaimsIdentity" enthalten, konnte die Benutzeridentität nicht authentifiziert werden.  
  
 Fügen Sie den Computer der gleichen Domäne wie der des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Servers hinzu, oder installieren Sie auf dem lokalen Computer einen Domänencontroller, um dieses Problem zu umgehen. Für die zweite Lösung, die Installation des Domänencontrollers, müssen Sie lokale Domänenkonten für alle Dienste und Benutzer erstellen. Sie müssen Dienstkonten und SharePoint-Berechtigungen für die Konten konfigurieren, die Sie definieren.  
  
 Die Installation eines Domänencontrollers auf Ihrem Computer ist nützlich, wenn die Zielsetzung darin besteht, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint in einem Offlinestatus zu verwenden. Ausführliche Anweisungen zur Verwendung von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] offline, finden Sie im Blogeintrag "dauert die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Server aus dem Netzwerk" auf [ http://www.powerpivotgeek.com ](http://go.microsoft.com/fwlink/?LinkId=184241).  
  
 **Szenario 4: Instabiler Server**  
  
 Ein oder mehrere Dienste könnten sich in einem inkonsistenten Status befinden. In einigen Fällen kann das Problem durch Ausführen von IISRESET behoben werden.  
  
  
