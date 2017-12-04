---
title: Verwenden des URL-Zugriffs in einer Webanwendung | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- links [Reporting Services], URL access
- URL access [Reporting Services], Web applications
- POST requests
- direct addressing [Reporting Services]
- Web applications [Reporting Services]
- hyperlinks [Reporting Services]
ms.assetid: 39e7918c-ad2d-4ca6-b099-2dd4dbdb83dc
caps.latest.revision: "33"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 123e0ff6bbc5a33214e515401ad38f7af5604b5f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="integrating-reporting-services-using-url-access---web-application"></a>Integrieren von Reporting Services mithilfe des URL-Zugriffs: Webanwendung
  Der URL-Zugriff in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] wurde speziell konzipiert, um den Zugriff auf einzelne Berichte über ein Netzwerk zu ermöglichen. Dieser Zugriffstyp eignet sich am besten, um die Anzeige und Navigation von Berichten in eine benutzerdefinierte Webanwendung zu integrieren. Um den URL-Zugriff in Webanwendungen zu verwenden, können Sie Folgendes tun:  
  
-   Richten Sie eine URL von einer Website oder einem Portal an einen bestimmten Berichtsserver.  
  
-   Verwenden Sie eine Formular-POST-Methode, und leiten Sie die Parameter für die Abfragezeichenfolge mithilfe von Formularfeldern an eine Berichtsserver-URL.  
  
## <a name="url-access-through-direct-addressing"></a>URL-Zugriff über Direktadressierung  
 Um mit einer URL auf einen Berichtsserver oder ein Berichtsserver-Datenbankelement zuzugreifen, geben Sie einfach die URL-Adresse im Webbrowser oder der Webanwendung an. Sie können auch Parameter für die URL angeben, die das Erscheinungsbild des Berichts oder der Ressource, auf die gerade zugegriffen wird, verändert. Eine URL kann über die Adressleiste eines Webbrowsers an einen Berichtsserver weiterleiten oder die Quelle eines **IFrame** sein, das Bestandteil einer größeren Webanwendung oder eines Portals ist. Sie können Links zu verschiedenen Webseiten Ihres Portals in die Berichte aufnehmen, außerdem können Sie einen speziellen Frame für den Bericht ansteuern oder ein neues Browserfenster im Prozess öffnen.  
  
 Im folgenden Beispiel steuert der Link einen Frame mit dem Namen „main“ an, der sich von dem Frame unterscheiden kann, der den Link enthält. Der Link kann ein Teil eines Webportals sein.  
  
```  
<a href="http://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main" target="main" >  
   Click here for the Territory Sales Drilldown sample report  
</a>  
```  
  
 Im vorherigen Beispiel wird die **LinkTarget**-Einstellung für Geräteinformationen mit dem Wert „main“ in der Abfragezeichenfolge der URL übergeben. Damit wird sichergestellt, dass alle Drillthroughlinks im Bericht auch den Frame „main“ ansteuern.  
  
 Weitere Informationen zu den Einstellungen für Geräteinformationen finden Sie unter [Übergeben von Geräteinformationseinstellungen an Renderingerweiterungen](../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
 Beachten Sie, dass in vielen Servern und Browsern die Anzahl der zulässigen Zeichen in einer URL beschränkt ist. In einigen Fällen sind maximal 256 Zeichen zulässig. Um diese Einschränkung zu umgehen, können Sie POST-Anforderungen mit Formularübergabe verwenden.  
  
> [!NOTE]  
>  Die maximale URL-Länge im Internet Explorer beträgt 2.083 Zeichen. Diese Grenze gilt sowohl für POST- als auch für GET-Anforderungs-URLs. POST-Anforderungen werden jedoch bei der Übergabe von Name-/Wert-Paaren nicht durch die Größe der URL beschränkt, da sie im Header und nicht in der URL übertragen werden.  
  
## <a name="url-access-through-a-form-post-method"></a>URL-Zugriff über die Formular POST-Methode  
 Wenn ein Benutzer mit URL-Zugriff Daten von einem Berichtsserver anfordert, verwendet die HTTP-Anforderung die GET-Methode. Dies entspricht einer Formularübergabe von METHOD = "GET". URL-Anforderungen oder Formularübergaben, die METHOD="GET" verwenden, sind durch die maximale Anzahl von Zeichen beschränkt, die ein Server oder Webbrowser verarbeiten kann.  
  
 Mit POST-Anforderungen (METHOD="POST" und Eingabefelder) werden die Name/Wert-Paare im Header und nicht in der URL übertragen. Daher sind die Name/Wert-Paare der Abfragezeichenfolge nicht Teil der URL und können viel längere und komplexere Parameterlisten enthalten.  
  
 Über den Direktzugriff kann ein Benutzer die URL für den Berichtsserver sehen und kann daher möglicherweise die Abfragezeichenfolge ändern oder sich die jeweiligen Parameter der URL-Anforderung und des Berichtsservers für eine spätere Verwendung notieren.  
  
 Die folgende Beispiel-HTML zeigt die Verwendung eines Formulars, das Sie verwenden können, um einen Berichtsserver mit einer bestimmten URL anzusteuern und die Parameter der Abfragezeichenfolge als Teil der Eingabefelder des Formulars weiterzuleiten.  
  
```  
<FORM id="frmRender" action="http://server/reportserver?/SampleReports/  
   Territory Sales Drilldown" method="post" target="_self">  
   <INPUT type="hidden" name="rs:Command" value="Render">   
   <INPUT type="hidden" name="rc:LinkTarget" value="main">  
   <INPUT type="hidden" name="rs:Format" value="HTML4.0">  
   <INPUT type="submit" value="Button">  
</FORM>  
```  
  
 Im vorhergehenden Beispiel gibt der Berichtsserver, wenn ein Benutzer auf die Schaltfläche im Formular klickt, einen HTML-gerenderten Bericht zurück, der auf den aktuellen Frame gerichtet ist. Eine vergleichbare URL-Zugriffszeichenfolge könnte folgendermaßen aussehen:  
  
```  
http://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main&rs:Format=HTML4.0  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Integration von Reporting Services in Anwendungen](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Integrieren von Reporting Services mit URL-Zugriff](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [Verwenden des URL-Zugriffs in einer Windows-Anwendung](../../reporting-services/application-integration/integrating-reporting-services-using-url-access-windows-application.md)   
 [URL-Zugriff (SSRS)](../../reporting-services/url-access-ssrs.md)  
  
  
