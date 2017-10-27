---
title: "Einstellungen der Übermittlungserweiterungen von Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
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
- XML Web service [Reporting Services], delivery extension settings
- Report Server Web service, delivery extension settings
- delivery [Reporting Services]
- network share delivery [Reporting Services]
- file share delivery [Reporting Services]
- e-mail [Reporting Services]
- mailing reports [Reporting Services]
- sharing reports
- extensions [Reporting Services], delivery
- mail [Reporting Services]
- Web service [Reporting Services], delivery extension settings
ms.assetid: 68c31a85-261c-4ec4-b8df-1f9842b46f8a
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: bc52f95cdc038c0074feb10b05fffe916b3d3da1
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="reporting-services-delivery-extension-settings"></a>Einstellungen der Reporting Services-Übermittlungserweiterungen
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]enthält eine e-Mail-übermittlungserweiterung und eine Dateifreigabe-übermittlungserweiterung. Über die E-Mail-Übermittlung können Sie einen Bericht per E-Mail an einzelne Benutzer oder Gruppen senden. Über die Dateifreigabeübermittlung können Sie automatisch gerenderte Berichte versenden, die auf Ihrem Netzwerk freigegeben werden sollen. Sie können jede dieser unterstützten Übermittlungserweiterungen mit Standardabonnements oder datengesteuerten Abonnements verwenden. Sie leiten die Übermittlungseinstellungen, die spezifisch für den Typ der Übermittlungserweiterung sind, bei jedem Aufruf der Methoden <xref:ReportService2010.ReportingService2010.CreateSubscription%2A>, <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>, <xref:ReportService2010.ReportingService2010.SetSubscriptionProperties%2A> und <xref:ReportService2010.ReportingService2010.SetDataDrivenSubscriptionProperties%2A> weiter. Um programmgesteuert eine Liste der Übermittlungseinstellungen abzurufen, verwenden Sie die <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A>-Methode.  
  
> [!NOTE]  
>  Bei den Einstellungen für die Übermittlungserweiterungen wird die Groß-/Kleinschreibung beachtet.  
  
## <a name="e-mail-delivery-settings"></a>Einstellungen für die E-Mail-Übermittlung  
 In der folgenden Tabelle werden die Einstellungen der E-Mail-Übermittlung für Abonnements aufgeführt, die Berichtsserver-E-Mail verwenden.  
  
|Einstellung|Wert|  
|-------------|-----------|  
|**AN**|Die e-Mail-Adresse, die auf die **auf** Zeile der e-Mail-Nachricht. Mehrere E-Mail-Adressen werden durch Semikolon getrennt. Erforderlich.|  
|**CC**|Die e-Mail-Adresse, die auf die **Cc** Zeile der e-Mail-Nachricht. Mehrere E-Mail-Adressen werden durch Semikolon getrennt. Optional.|  
|**BCC**|Die e-Mail-Adresse, die auf die **Bcc** Zeile der e-Mail-Nachricht. Mehrere E-Mail-Adressen werden durch Semikolon getrennt. Optional.|  
|**ReplyTo-Element**|Die e-Mail-Adresse, die in der **Antwort an** -Header der e-Mail-Nachricht. Dieser Wert darf nur eine E-Mail-Adresse enthalten. Optional.|  
|**Bericht einschließen**|Ein Wert, der angibt, ob der Bericht in der E-Mail-Übermittlung enthalten sein soll. Der Wert **"true"** gibt an, dass der Bericht im Textkörper der e-Mail-Nachricht übermittelt wird.|  
|**Renderformat**|Der Name der Renderingerweiterung, die zum Generieren des gerenderten Berichts verwendet werden soll. Der Name muss einer der sichtbaren Renderingerweiterungen entsprechen, die auf dem Berichtsserver installiert sind. Dieser Wert ist erforderlich, wenn die **Bericht einschließen** eingestellt auf einen Wert von **"true"**.|  
|**Priority**|Die Priorität, mit der die E-Mail gesendet wird. Gültige Werte sind **niedrig**, **NORMAL**, und **hohe**. Der Standardwert ist **NORMAL**.|  
|**Betreff**|Der Text in der Betreffzeile der E-Mail-Nachricht.|  
|**Anmerkung**|Der im Textkörper der E-Mail-Nachricht enthaltene Text.|  
|**IncludeLink**|Ein Wert, der angibt, ob ein Link zum Bericht im Textkörper der E-Mail enthalten sein soll.|  
  
## <a name="file-share-delivery-settings"></a>Einstellungen der Dateifreigabeübermittlung  
 In der folgenden Tabelle werden die Einstellungen der Dateifreigabeübermittlung für Abonnements aufgelistet.  
  
|Einstellung|Wert|  
|-------------|-----------|  
|**DATEINAME**|Der Name der Datei, die auf dem Datenträger gespeichert wird.|  
|**FILEEXTN**|Gibt an, ob eine Dateierweiterung für den gerenderten Bericht enthalten sein soll. Der Wert lautet entweder **"true"** oder **"false"**.|  
|**PFAD**|Der Ordnerpfad oder der UNC-Dateifreigabepfad, in dem der Bericht gespeichert werden soll.|  
|**RENDER_FORMAT**|Das Format des Berichts, der auf dem Datenträger gespeichert wird.|  
|**BENUTZERNAME**|Der Benutzername, der benötigt wird, um auf die Netzwerkressource oder den Datenträger zuzugreifen.|  
|**KENNWORT**|Das Kennwort, das benötigt wird, um auf die Netzwerkressource oder den Datenträger zuzugreifen.|  
|**WRITEMODE**|Der Schreibmodus, der zu verwenden ist, wenn Sie auf den Datenträger zugreifen. Gültige Werte sind **keine**, **überschreiben**, und **AutoIncrement**.|  
  
## <a name="see-also"></a>Siehe auch  
 [Technische Referenz &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)   
 [Erstellen von Anwendungen mit dem Webdienst und .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  

