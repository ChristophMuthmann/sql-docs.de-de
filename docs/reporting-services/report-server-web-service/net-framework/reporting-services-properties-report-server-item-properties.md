---
title: Berichtsservereigenschaften Element | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- report servers [Reporting Services], properties
- item-specific properties [Reporting Services]
- report items [Reporting Services], properties
- items [Reporting Services], properties
ms.assetid: 21edec6d-9897-48fb-8c75-182305b1dbdb
caps.latest.revision: 43
author: sabotta
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 33dfc4da9781e537c222bd9aed593b694d734ba0
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="reporting-services-properties---report-server-item-properties"></a>Eigenschaften für Reporting Services - Eigenschaften der Berichtsserverelemente
  Elementeigenschaften sind Eigenschaften, die für Elemente in der Berichtsserver-Datenbank spezifisch sind. Zu diesen Elementen gehören Berichte, verlinkte Berichte, Ordner, Ressourcen, Modelle und Datenquellen.  
  
 Folgende Namen der Elementeigenschaften sind reserviert. Sie können keine benutzerdefinierten Eigenschaften des gleichen Namens erstellen. Sie können viele dieser Eigenschaften mit den Webdienstmethoden für Berichtsserver lesen oder ändern.  
  
## <a name="item-properties"></a>Elementeigenschaften  
 Folgende Eigenschaften gelten für alle Elemente in der Berichtsserver-Datenbank.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**CreatedBy**|Der Name des Benutzers, der das Element ursprünglich zur Berichtsserver-Datenbank hinzugefügt hat.|  
|**CreationDate**|Der Zeitpunkt (Datum und Uhrzeit), zu dem das Element zur Berichtsserver-Datenbank hinzugefügt wurde.|  
|**Description**|Die Beschreibung des Elements.|  
|**Hidden**|Ein Wert, der angibt, ob das Element für Benutzer sichtbar und verfügbar ist.|  
|**ID**|Die ID eines Elements in der Berichtsserver-Datenbank.|  
|**ModifiedBy**|Der Name des Benutzers, der das Element als Letzter in der Berichtsserver-Datenbank geändert hat.|  
|**ModifiedDate**|Zeitpunkt (Datum und Uhrzeit) der letzten Änderung des Elements durch den Benutzer.|  
|**Name**|Der Name eines Elements in der Berichtsserver-Datenbank.|  
|**Pfad**|Der vollständige Pfadname des Elements. Der Pfad jedes Elements in der Berichtsserver-Datenbank hat eine maximale Zeichenlänge von 260.|  
|**Größe**|Die Größe eines Elements (in Byte) in der Berichtsserver-Datenbank.|  
|**Typ**|Der Typ eines Elements in der Berichtsserver-Datenbank.|  
|**"VirtualPath"**|Der virtuelle Pfad zu einem Element in der Berichtsserver-Datenbank. Der Wert der <xref:ReportService2010.CatalogItem.VirtualPath%2A>-Eigenschaft ist der Pfad, in dem der Benutzer das Element findet. Ein Bericht mit dem Namen report1, der sich im persönlichen Ordner des Benutzers "Meine Berichte" befindet, hat den virtuellen Pfad /My Reports. Der tatsächliche Pfad des Elements ist /Benutzer /Benutzername /Meine Berichte.|  
  
## <a name="folder-properties"></a>Ordnereigenschaften  
 Zusätzlich zu den zuvor aufgeführten Elementeigenschaften gilt folgende Eigenschaft für Ordner in der Berichtsserver-Datenbank.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**Reserviert**|Ein Wert, der von der <xref:ReportService2010.ReportingService2010.GetProperties%2A>-Methode für Ordner zurückgegeben wurde, die vom Berichtsserver reserviert sind. Reservierte Ordner enthalten Benutzer, Meine Berichte und /. Reservierte Ordner können nicht geändert oder entfernt werden.|  
  
## <a name="report-properties"></a>Berichtseigenschaften  
 Zusätzlich zu den zuvor aufgeführten Elementeigenschaften gelten folgende Eigenschaften für Berichte in der Berichtsserver-Datenbank.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**Sprache**|Die in einem Bericht verwendete Sprache. Der Wert ist ein Sprachcode, der in der IETF-Spezifikation (Internet Engineering Task Force) RFC1766 definiert ist. Der erste Teil ist eine Bezeichnung aus zwei Zeichen für die Basissprache. Der zweite Teil ist durch einen Bindestrich getrennt und legt die Variation oder den Dialekt der Sprache fest. Wenn der Wert nicht im **Style**-Element angegeben ist, das zum **Body**-Element in der Berichtsdefinition gehört, ist der Standardwert gleich der Sprache des Berichtsservers.|  
|**ReportProcessingTimeout**|Timeout (in Sekunden) für einen einzelnen Bericht. Wenn dieser Wert festgelegt ist, versucht der Berichtsserver, die Verarbeitung eines Berichts zu beenden, sobald der angegebene Zeitraum überschritten wird. Gültige Werte sind **-1** bis **2**.**147**.**483**.**647**. Wenn der Wert gleich **-1** ist, gibt es für den Berichten während der Verarbeitung kein Timeout. Wenn der Wert gleich **null** ist, wird für das Timeout bei der Berichtsverarbeitung der Wert der Systemeigenschaft **ReportProcessingTimeout** verwendet. Der Standardwert ist **null**. Weitere Informationen finden Sie unter [Berichtsserver-Systemeigenschaften](../../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md).|  
|**ExecutionDate**|Zeitpunkt (Datum und Uhrzeit), zu dem zuletzt eine Berichtsmomentaufnahme für einen Bericht erstellt wurde.|  
|**CanRunUnattended**|Ein Wert, der angibt, ob ein Bericht unbeaufsichtigt nach einem Zeitplan ausgeführt werden kann. Ist diese Eigenschaft auf **true** festgelegt, sind die Standardwerte für die Berichtsparameter definiert, und die Anmeldeinformationen für die Datenquelle werden mit dem Bericht gespeichert, oder die Option zum Abrufen der Anmeldeinformationen ist auf **None** festgelegt. Ist diese Eigenschaft auf **false** festgelegt, sind die Voraussetzungen zum unbeaufsichtigten Ausführen eines Berichts nicht erfüllt. Weitere Informationen finden Sie unter [Konfigurieren des Kontos für die unbeaufsichtigte Ausführung &#40;SSRS-Konfigurations-Manager&#41;](../../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).|  
|**HasParameterDefaultValues**|Ein Wert, der angibt, ob im Bericht gültige Standardwerte für alle Berichtsparameter festgelegt wurden. Der Wert lautet auch **true**, wenn ein Bericht keine Berichtsparameter hat. Wenn diese Eigenschaft auf **false** festgelegt ist, hat mindestens ein Berichtsparameter keinen gültigen Standardwert.|  
|**HasDataSourceCredentials**|Ein Wert, der angibt, dass die Option zum Abrufen der Anmeldeinformationen für alle zum Bericht gehörenden Datenquellen entweder gleich **None** oder gleich **Store** ist. Wenn diese Eigenschaft auf **false** festgelegt ist, ist eine Option zum Abrufen der Anmeldeinformationen für eine der zum Bericht gehörenden Datenquellen gleich **Integrated** oder gleich **Prompt**.|  
|**IsSnapshotExecution**|Ein Wert, der angibt, ob der Bericht eine Momentaufnahme ist.|  
|**HasScheduleReadyDataSources**|Ein Wert, der angibt, ob die Datenquellen eines Berichts so konfiguriert sind, dass die geplante Ausführung unterstützt wird. Wenn diese Eigenschaft auf **false** festgelegt ist, können Benutzer den Bericht nicht abonnieren.|  
  
## <a name="resource-properties"></a>Ressourceneigenschaften  
 Zusätzlich zu den zuvor aufgeführten Elementeigenschaften gilt folgende Eigenschaft für Ressourcen in der Berichtsserver-Datenbank.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**MimeType-Eigenschaft**|Der MIME-Typ einer Ressource in der Berichtsserver-Datenbank.|  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit dem Webdienst und .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Berichtsserver-Webdienst](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Technische Referenz &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
