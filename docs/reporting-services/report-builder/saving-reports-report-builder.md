---
title: Speichern von Berichten (Berichts-Generator) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c5d4f5efbe000946f543fd9b22b5a45f48e06050
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="saving-reports-report-builder"></a>Speichern von Berichten (Berichts-Generator)
  Im Berichts-Generator können Sie einen Bericht mit Seitenzahlen auf einem [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Berichtsserver, in einer SharePoint-Bibliothek, in einer Dateifreigabe, für die Sie Schreibrechte haben, oder auf dem Computer speichern. 
  
Wenn Sie einen Bericht speichern, speichern Sie in Wirklichkeit die Berichtsdefinition, in der das Berichtslayout beschrieben wird. Die Daten werden nicht gespeichert. Bei jeder Ausführung des Berichts werden die Berichtsdaten aktualisiert. Sie sind dann wahrscheinlich anders als bei der letzten Ausführung des Berichts.  
  
 Wenn Sie den Bericht zu einem anderen Format speichern oder die Berichtsdefinition mit den Daten speichern möchten, verwenden Sie eine der folgenden [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionen:  
  
-   Exportieren Sie einen gerenderten Bericht in ein anderes Dateiformat, z. B. in durch Trennzeichen getrennte Dateien (CSV) oder Excel-Arbeitsmappen, und speichern Sie den Bericht in diesem Format. Sie können auch Datenfeeds von Berichten generieren und die Berichtsdaten speichern.  
  
-   Erstellen Sie Berichtsabonnements, um Berichte an eine Dateifreigabe zu übermitteln und dort zu speichern.  
  
-   Speichern Sie Versionen von gerenderten Berichten mithilfe des Berichtsverlaufs als Verlaufskopie.  
  
 Weitere Informationen zum Anzeigen und Verwalten von Berichten direkt auf dem Berichtsserver finden Sie unter [Suchen, Anzeigen und Verwalten von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md) und [Reporting Services-Berichtsserver &#40;einheitlicher Modus&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md).  
  
##  <a name="SavingReportDefinitions"></a> Speichern von Berichten auf einem Berichtsserver  
  Das Speichern eines Berichts auf einem Berichtsserver wird auch als Veröffentlichen eines Berichts bezeichnet. Auch wenn Sie Berichte auf dem Computer speichern können, hat das Speichern der Berichte auf einem Berichtsserver viele Vorteile:  
  
-   Berichte sind für andere Personen verfügbar, wenn diese über die Zugriffsberechtigung auf den Ordner verfügen, in dem Sie den Bericht gespeichert haben.  
  
-   Berichte können im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwaltet und angezeigt werden.  
  
-   Berichtsressourcen wie Datenquellen, Bilder und Unterberichte werden für einen einfacheren Zugriff an einem Speicherort gespeichert.  
  
-   Berichte können über Abonnements an andere Personen übermittelt werden.  
  
-   Berichte werden in der Berichtsserverdatenbank sicher gespeichert.  
  
-   Die Ausführung von Berichten kann protokolliert werden. Damit stehen Leistungs- und Überwachungsinformationen zur Verfügung.  
  
##  <a name="ExportingAndSavingReports"></a> Exportieren und Speichern von Berichten  
 Falls Sie nur wenige Berichte archivieren müssen, sollten Sie einen Bericht exportieren und als Datei speichern. Nachdem Sie einen Bericht in eine Anwendung exportiert haben (z. B. PDF oder Excel), können Sie ihn als Datei speichern und in einem geschützten freigegebenen Verzeichnis im Netzwerk platzieren. Oder Sie laden eine gespeicherte PDF- oder Excel-Datei als Ressourcenelement hoch, falls Sie alle Kopien eines Berichts unabhängig vom Format in der Berichtsserver-Datenbank speichern möchten. Weitere Informationen zum Exportieren eines Berichts finden Sie unter [Exportieren von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) und [Hochladen einer Datei oder eines Berichts](../../reporting-services/reports/upload-a-file-or-report-report-manager.md).  
  
##  <a name="UsingFileShareDelivery"></a> Verwenden der Dateifreigabeübermittlung  
 Falls Sie viele Berichte archivieren müssen, erstellen Sie ein Abonnement, das den Bericht direkt an das Dateisystem übermittelt. Bei dieser Vorgehensweise müssen Sie für jeden Bericht ein Abonnement erstellen, einen freigegebenen Ordner zum Speichern der Berichte auswählen und einen Zeitplan definieren, der bestimmt, wann die Datei erstellt wird. Sobald Sie ein Abonnement definiert haben, kann der Berichtsserver mithilfe des bereitgestellten Zeitplanes den Bericht unbeaufsichtigt ausführen und Berichtsdateien zum Archiv hinzufügen. Darüber hinaus können Sie Zeitpläne für die einmalige Verwendung erstellen, falls Sie Berichte gelegentlich archivieren möchten. Weitere Informationen zu Abonnements und zur Dateifreigabeübermittlung finden Sie unter [Dateifreigabeübermittlung in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md).  
  
##  <a name="UsingReportHistory"></a> Verwenden des Berichtsverlaufs  
 Mit der Funktion zum Berichtsverlauf können ebenfalls Verlaufskopien erstellt werden. Anschließend können Sie die Berichtsserver-Datenbank sichern und die Sicherungskopie für die spätere Verwendung an einem sicheren Ort aufbewahren. Alle Berichtsverläufe (zusammen mit Berichten, freigegebenen Datenquellenelementen, Ordnern, Abonnements und freigegebenen Zeitplänen) werden in der Berichtsserver-Datenbank gespeichert. Sie können eine Sicherungskopie erstellen, um eine permanente Kopie des Berichtsverlaufs und der Metadaten zu verwalten, wie z. B. Abonnementinformationen, die die Empfänger eines Berichts bezeichnen. Weitere Informationen finden Sie unter [Erstellen, Ändern und Löschen von Momentaufnahmen im Berichtsverlauf](../../reporting-services/report-server/create-modify-and-delete-snapshots-in-report-history.md).  
 
##  <a name="HowTo"></a> Themen zur Vorgehensweise  
  
-   [Speichern von Berichten auf einem Berichtsserver &#40;Berichts-Generator&#41;](../../reporting-services/report-builder/save-reports-to-a-report-server-report-builder.md)  
  
-   [Speichern eines Berichts in einer SharePoint-Bibliothek &#40;Berichts-Generator&#41;](../../reporting-services/report-builder/save-a-report-to-a-sharepoint-library-report-builder.md)  
   
## <a name="see-also"></a>Siehe auch  
 [Berichte, Berichtsteile und Berichtsdefinitionen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Installieren und Deinstallieren von Berichts-Generator](http://msdn.microsoft.com/library/2c9a5814-17bf-4947-8fb3-6269e7caa416)   
 [Suchen, anzeigen und Verwalten von Berichten &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportieren von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Drucken von Berichten &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)  
  
  

