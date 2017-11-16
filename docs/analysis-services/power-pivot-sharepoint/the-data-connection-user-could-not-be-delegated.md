---
title: Der Data Connection-Benutzer konnten nicht delegiert werden | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: d2006df1-d244-4786-b272-49d8996cc88c
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 82b5e9a4f63aee2235972f62387367075ff4b8b9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="the-data-connection-user-could-not-be-delegated"></a>Der Data Connection-Benutzer konnten nicht delegiert werden
  Für Excel-Arbeitsmappen, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten enthalten, gibt Excel Services diesen Fehler zurück, wenn keine Verbindung mit einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Serverinstanz in SharePoint hergestellt werden kann.  
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Gilt für|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint|  
|Produktversion|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Ursache|Verbindungsfehler beim Versuch, einen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenanbieter zu verwenden.|  
|Meldungstext|Die Datenverbindung verwendet die Windows-Authentifizierung, und Benutzeranmeldeinformationen konnten nicht delegiert werden. Die folgenden Verbindungen wurden nicht aktualisiert: [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten|  
  
## <a name="explanation"></a>Erklärung  
 Es gibt mehrere Ursachen für diese Fehlermeldung. Alle haben gemeinsam, dass Excel Services keine gültige Windows-Benutzeridentität von einem Claims-Token in SharePoint abrufen können. Bei Excel-Arbeitsmappen, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten enthalten, tritt dieser Fehler auf, wenn eine der folgenden Bedingungen zutrifft:  
  
-   c2WTS (Claims to Windows Token Service) wird nicht ausgeführt. Sie können die Ursache dieses Fehlers überprüfen, indem Sie die SharePoint-Protokolldatei anzeigen. Wenn die SharePoint-Protokolle die Meldung enthalten, dass der Pipeendpunkt "net.pipe://localhost/s4u/022694f3-9fbd-422b-b4b2-312e25dae2a2" auf dem lokalen Computer nicht gefunden wurde, wird c2WTS (Claims to Windows Token Service) nicht ausgeführt. Um ihn zu starten, verwenden Sie die Zentraladministration und überprüfen dann, ob der Dienst in der Konsolenanwendung Dienste ausgeführt wird.  
  
-   Es ist kein Domänencontroller verfügbar, um die Benutzeridentität zu überprüfen. c2WTS (Claims to Windows Token Service) verwendet keine zwischengespeicherten Anmeldeinformationen. Er überprüft die Benutzeridentität für jede Verbindung. Sie können die Ursache dieses Fehlers überprüfen, indem Sie die SharePoint-Protokolldatei anzeigen. Wenn die SharePoint-Protokolle die Meldung "Fehler beim Abrufen von WindowsIdentity aus IClaimsIdentity" enthalten, konnte die Benutzeridentität nicht authentifiziert werden.  
  
-   Die Computer müssen Mitglieder derselben Domäne oder mehrerer Domänen sein, die sich gegenseitig vertrauen.  
  
-   Sie müssen Windows-Domänenbenutzerkonten verwenden. Die Konten müssen über einen Universal Principal Name (UPN) verfügen.  
  
-   Das Excel Services-Dienstkonto muss über Active Directory-Berechtigungen zur Abfrage des Objekts verfügen.  
  
## <a name="user-action"></a>Benutzeraktion  
 Befolgen Sie die nachfolgenden Anweisungen, um den Status von c2WTS (Claims to Windows Token Service) zu überprüfen.  
  
 Wenden Sie sich in allen anderen Fällen an den Netzwerkadministrator.  
  
#### <a name="enable-claims-to-windows-token-service"></a>Aktivieren von c2WTS (Claims to Windows Token Service)  
  
1.  Klicken Sie in der Zentraladministration unter Systemeinstellungen auf **Dienste auf dem Server verwalten**.  
  
2.  Wählen Sie **Claims to Windows Token Service**aus, und klicken Sie dann auf **Starten**.  
  
3.  Überprüfen Sie, ob der Dienst auch in der Konsole Dienste ausgeführt wird.  
  
    1.  Klicken Sie unter Verwaltung auf Dienste.  
  
    2.  Starten Sie c2WTS (Claims to Windows Token Service), falls er nicht ausgeführt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Power Pivot-Dienstkonten](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)  
  
  

