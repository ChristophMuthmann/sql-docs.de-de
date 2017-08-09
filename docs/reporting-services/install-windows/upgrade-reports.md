---
title: Aktualisieren von Berichten | Microsoft Docs
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reports [Reporting Services], upgrading
- published reports [Reporting Services], upgrades
- custom report items, upgrading
- Reporting Services, upgrades
- upgrading Reporting Services
- snapshots [Reporting Services], upgrading
- report definition files [Reporting Services]
- .rdl files
ms.assetid: a1a10c67-7462-4562-9b07-a8822188a161
caps.latest.revision: 70
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5c6265fd62ae10a8037b0fbd1f7d26edb5de8bc9
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---

# <a name="upgrade-reports"></a>Aktualisieren von Berichten

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)]

  Berichtsdefinitionsdateien (RDL) werden auf folgende Weise automatisch aktualisiert:  
  
-   Wenn Sie einen Bericht im Berichts-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]öffnen, wird die Berichtsdefinition auf das derzeit unterstützte RDL-Schema aktualisiert. Wenn Sie in den Projekteigenschaften als Berichtsserver [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] angeben, wird die Berichtsdefinition in einem Schema gespeichert, das mit dem Zielserver kompatibel ist.  
  
-   Wenn Sie eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Installation auf eine [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Installation aktualisieren, werden vorhandene Berichte und Momentaufnahmen, die auf einem Berichtsserver veröffentlicht wurden, kompiliert und automatisch auf das neue Schema aktualisiert, wenn sie zum ersten Mal verarbeitet werden. Wenn ein Bericht nicht automatisch aktualisiert werden kann, wird er im Abwärtskompatibilitätsmodus verarbeitet. Die Berichtsdefinition bleibt im ursprünglichen Schema erhalten.  
  
 Berichte werden nicht aktualisiert, wenn Sie eine Berichtsdefinitionsdatei direkt auf den Berichtsserver oder auf eine SharePoint-Website hochladen. Das Upgrade einer Berichtsdefinition in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ist die einzige Möglichkeit, die RDL-Datei zu aktualisieren.  
  
 Nachdem ein Bericht lokal oder auf dem Berichtsserver aktualisiert wurde, werden möglicherweise weitere Fehler, Warnungen und Meldungen angezeigt. Das ist das Ergebnis der Änderungen am internen Berichtsobjektmodell und an Verarbeitungskomponenten, die das Anzeigen von Meldungen bewirken, sobald zugrunde liegende Probleme im Bericht erkannt werden. Weitere Informationen finden Sie unter [Reporting Services Backward Compatibility][](../../reporting-services/reporting-services-backward-compatibility.md "Abwärtskompatibilität | Reporting Services").  
  
 Weitere Informationen zu neuen Funktionen für [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], finden Sie unter [Neuigkeiten in Reporting Services](https://msdn.microsoft.com/library/ms170438.aspx).  

##  <a name="bkmk_versionsupported"></a> Vom Upgrade unterstützte Versionen  
 Berichte, die in einer vorherigen Version von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] erstellt wurden, können aktualisiert werden. Dazu gehören die folgenden Versionen:  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
##  <a name="bkmk_rdlfiles"></a> Berichtsdefinitionsdateien (RDL-Dateien) und Berichts-Designer  
 Eine Berichtsdefinitionsdatei schließt einen Verweis auf den RDL-Namespace ein, der die Version des Berichtsdefinitionsschemas angibt, das zur Überprüfung der RDL-Datei verwendet wird.  
  
 Wenn Sie eine RDL-Datei im Berichts-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]öffnen und der Bericht für einen vorherigen Namespace erstellt wurde, erstellt der Berichts-Designer automatisch eine Sicherungsdatei und aktualisiert den Bericht auf den aktuellen Namespace. Dies ist die einzige Möglichkeit, wie Sie eine Berichtsdefinitionsdatei aktualisieren können.  
  
 Die von Ihnen festgelegten Bereitstellungseigenschaften können das Schema beeinflussen, in dem die Berichtsdefinitionsdatei gespeichert wird. Weitere Informationen finden Sie unter [Bereitstellung und Versionsunterstützung in SQL Server Data Tools &#40;SSRS&#41;](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)enthalten.  
  
 Sie können eine RDL-Datei, die in einer früheren Version erstellten hochladen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] an der neuen Version und es wird bei der ersten Verwendung automatisch aktualisiert. Der Berichtsserver speichert die Berichtsdefinitionsdatei im ursprünglichen Format. Der Bericht wird automatisch aktualisiert, wenn er zum ersten Mal angezeigt wird. Die gespeicherte Berichtsdefinitionsdatei wird jedoch nicht verändert.  
  
 Informationen zum Ermitteln des aktuellen RDL-Schemas für einen Bericht, einen Berichtsserver oder den Berichts-Designer finden Sie unter [Suchen der Berichtsdefinitions-Schemaversion &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  
  
##  <a name="bkmk_publishedreports_and_snapshots"></a> Veröffentlichte Berichte und Berichtsmomentaufnahmen  
 Bei der ersten Verwendung versucht der Berichtsserver, vorhandene veröffentlichte Berichte und Berichtsmomentaufnahmen auf das neue Berichtsdefinitionsschema zu aktualisieren, ohne dass Sie etwas unternehmen müssen. Es wird versucht, das Upgrade auszuführen, wenn der Benutzer einen Bericht oder eine Berichtsmomentaufnahme anzeigt bzw. wenn der Berichtsserver ein Abonnement verarbeitet. Die Berichtsdefinition wird nicht ersetzt, sondern weiterhin auf dem Berichtsserver im ursprünglichen Schema gespeichert. Wenn ein Bericht nicht automatisch aktualisiert werden kann, wird er im Abwärtskompatibilitätsmodus ausgeführt.  
  
##  <a name="bkmk_backcompat"></a> Abwärtskompatibilitätsmodus  
 Berichte, die erfolgreich aktualisiert wurden, werden vom [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Berichtsprozessor verarbeitet. Wenn ein Bericht nicht automatisch aktualisiert werden kann, wird er vom Berichtsprozessor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im Abwärtskompatibilitätsmodus verarbeitet. Ein Bericht kann nicht von beiden Berichtsprozessoren verarbeitet werden. Bei der ersten Verwendung wird ein Bericht entweder erfolgreich aktualisiert oder für den Abwärtskompatibilitätsmodus markiert.  
  
 Nur der [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Berichtsprozessor unterstützt neue Funktionen. Wenn ein Bericht nicht aktualisiert werden kann, können Sie zwar den gerenderten Bericht anzeigen, die neuen Funktionen sind jedoch nicht verfügbar. Um die neuen Funktionen nutzen zu können, muss ein Bericht erfolgreich aktualisiert werden.  
  
##  <a name="bkmk_subreports"></a> Aktualisieren eines Berichts mit Unterberichten  
 Wenn ein Bericht Unterberichte enthält, kann einer von vier möglichen Zustände während des Upgrades auftreten:  
  
-   Der Hauptbericht und alle Unterberichte können erfolgreich aktualisiert werden. Sie werden vom [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Berichtsprozessor verarbeitet.  
  
-   Der Hauptbericht und alle Unterberichte können nicht aktualisiert werden. Sie werden vom Berichtsprozessor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verarbeitet.  
  
-   Der Hauptbericht kann aktualisiert werden, aber ein oder mehrere Unterberichte können nicht aktualisiert werden. Der Hauptbericht wird vom [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Berichtsprozessor verarbeitet. Im gerenderten Bericht wird jedoch an der Stelle, an der der Unterbericht angezeigt würde, der nicht aktualisiert werden konnte, die Meldung angezeigt: "Fehler: Unterbericht konnte nicht verarbeitet werden".  
  
-   Der Hauptbericht kann nicht aktualisiert werden, aber ein oder mehrere Unterberichte können aktualisiert werden. Der Hauptbericht wird vom [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Berichtsprozessor verarbeitet. Im gerenderten Bericht wird jedoch an der Stelle, an der der Unterbericht angezeigt würde, die Meldung angezeigt: "Fehler: Unterbericht konnte nicht verarbeitet werden".  
  
 Wenn die Fehlermeldung "Fehler: Unterbericht konnte nicht verarbeitet werden" angezeigt wird, müssen Sie die Definition des Hauptberichts oder des Unterberichts ändern, sodass alle Berichte von der gleichen Version des Berichtsprozessors verarbeitet werden können.  
  
 Für Drillthroughberichte gilt diese Einschränkung nicht, da sie als unabhängige Berichte verarbeitet werden.  
  
##  <a name="bkmk_CRIs"></a> Aktualisieren eines Berichts mit benutzerdefinierten Berichtselementen  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]-, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]- oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichte können benutzerdefinierte Berichtselemente (Custom Report Item, CRI) enthalten, die von Softwaredrittanbietern bereitgestellt und vom Systemadministrator auf dem Computer zur Berichtserstellung und auf dem Berichtsserver installiert wurden. Berichte, die CRIs enthalten, können auf die folgenden Weisen aktualisiert werden:  
  
-   Ein [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]-, [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]-, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]- oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver wird auf einen [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Berichtsserver aktualisiert. Auf dem Berichtsserver veröffentlichte Berichte werden automatisch bei der ersten Verwendung aktualisiert.  
  
-   Ein [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]-, [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]-, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]- oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht wird auf einen [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Berichtsserver hochgeladen. Der Bericht wird bei seiner ersten Verwendung automatisch aktualisiert.  
  
-   Ein [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]-, [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]-, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]- oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht wird im Berichts-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]geöffnet. Es wird eine Sicherungskopie des ursprünglichen Berichts erstellt. Einer der folgenden zwei Fälle tritt auf:  
  
    1.  Alle CRIs im Bericht verfügen über keine nicht unterstützten Funktionen. Die CRIs werden in Berichtselemente im neuen Berichtsdefinitionsformat konvertiert, sodass der gesamte Bericht aktualisiert wird. Wenn Sie die Datei speichern, wird sie im aktuellen RDL-Namespace gespeichert.  
  
    2.  Ein oder mehrere CRIs im Bericht verfügen über nicht unterstützte Funktionen. Ein Dialogfeld fordert den Benutzer zur Angabe auf, ob die CRIs konvertiert oder unverändert beibehalten werden sollen.  
  
     Weitere Informationen hierzu finden Sie unter [Öffnen eines Berichts mit CRIs im Berichts-Designer](#OpeningaReport) weiter hinten in diesem Thema  
  
 Weitere Informationen zum Identifizieren des aktuellen RDL-Namespace für einen Berichtsserver, zu [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] oder zu einem Bericht finden Sie unter [Suchen der Berichtsdefinitions-Schemaversion &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  
  
### <a name="upgrading-reports-on-a-report-server"></a>Aktualisieren eines Berichts auf einem Berichtsserver  
 Wenn ein [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]-, [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]-, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]- oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht erstmals auf einem Berichtsserver ausgeführt wird, der auf einen [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Berichtsserver aktualisiert wurde, wird der Bericht automatisch auf den aktuellen, vom Berichtsserver unterstützten Berichtsdefinitionsnamespace aktualisiert. Der Bericht kann vor dem Upgrade auf dem Berichtsserver vorhanden gewesen sein, oder der Bericht kann mit dem Berichts-Manager hochgeladen oder vom Berichts-Designer in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]auf dem Berichtsserver veröffentlicht worden sein.  
  
 In der folgenden Tabelle werden die Upgradeaktionen aufgeführt, die vom Berichtsserver für bestimmte Typen von CRIs in einem Bericht ausgeführt werden.  
  
|CRI-Typ|Upgradeaktion des Berichtsservers|  
|--------------|----------------------------------|  
|CRIs von Drittanbietern|Es wird kein Upgrade durchgeführt.<br /><br /> Verarbeitung erfolgt durch den [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]-, [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]-, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]- oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsprozessor.|  
  
###  <a name="OpeningaReport"></a> Öffnen eines Berichts mit CRIs im Berichts-Designer  
 Beim Öffnen einer [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht mit CRIs im Berichts-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], der Bericht auf dem neuen berichtsdefinitionsschema aktualisiert. Abhängig von den im Bericht enthaltenen CRIs wird eine der folgenden Aktionen ausgeführt:  
  
-   Es wurden CRIs von Drittanbietern erkannt. Wenn die auf dem Computer zur Berichtserstellung installierte CRI-Version nicht mit dem neuen RDL-Schema kompatibel ist, wird in der Entwurfsoberfläche ein Textfeld mit einem roten X angezeigt. Sie müssen sich an Ihren Systemadministrator wenden, um neue Versionen der CRIs von Drittanbietern zu installieren, die mit dem neuen RDL-Schema kompatibel sind.  
  
 Ein vorhandener Bericht lässt sich nur dadurch mit dem neuen Berichtsdefinitionsschema aktualisieren, dass er nach dem Upgrade in der Berichterstellungsumgebung gespeichert wird.  
  
###  <a name="bkmk_convertCRIdialog"></a> CRI konvertieren (Dialogfeld)  
 Dieser Bericht enthält benutzerdefinierte Berichtselemente (Custom Report Item, CRI) mit nicht unterstützten Funktionen. CRIs sind Erweiterungen der Berichtsdefinitionssprache (Report Definition Language, RDL) zur Unterstützung benutzerdefinierter Objekte, die Daten in einem Bericht anzeigen. CRIs umfassen Entwurfszeit- und Laufzeitkomponenten, die von Drittanbietern bereitgestellt werden.  
  
> [!NOTE]  
>  Die Entscheidung, benutzerdefinierte Berichtselemente auf einem Berichtsserver zuzulassen, wird vom Systemadministrator getroffen. Zum Anzeigen von CRIs in einem Bericht müssen die CRI-Komponenten auf dem Berichterstellungsserver installiert sein, um einen Bericht als Vorschau anzuzeigen, und auf dem Berichtsserver, um einen veröffentlichten oder hochgeladenen Bericht anzuzeigen. Weitere Informationen finden Sie unter [Benutzerdefinierte Berichtselemente](../../reporting-services/custom-report-items/custom-report-items.md) und in der Dokumentation des Softwaredrittanbieters.  
  
 Einige CRIs können im neuen Berichtsdefinitionsformat in Berichtselemente konvertiert werden. Entscheiden Sie anhand der folgenden Liste, ob die CRIs in diesem Bericht konvertiert werden sollen:  
  
-   **Ja** Wählen Sie **Ja** aus, um nach Möglichkeit alle CRIs im Bericht zu konvertieren. Nicht unterstützte Funktionen in den CRIs können nicht aktualisiert werden und werden aus der Berichtsdefinitionsdatei entfernt. Bei der Anzeige des Berichts werden möglicherweise Unterschiede in der Darstellung der CRIs im Bericht deutlich.  
  
-   **Nein** Wählen Sie **Nein** aus, wenn die CRIs im Bericht nicht konvertiert werden sollen. Diese CRIs können vom Berichtsprozessor nicht in ihrer aktuellen Version angezeigt werden. Wenn der Systemadministrator die Installation einer neuen CRI-Version von einem Softwaredrittanbieter plant, die mit dem neuen Berichtsdefinitionsformat kompatibel ist, sollten Sie **Nein**auswählen. Bis neue Versionen zur Verfügung stehen, werden die CRIs im Bericht als leere Textfelder mit einem roten X dargestellt.  
  
 In beiden Fällen wird der Bericht auf das neue Berichtsdefinitionsformat aktualisiert, und eine Sicherungskopie des ursprünglichen Berichts wird als gespeichert  *\<Berichtsname >* `-` Backup.rdl. Wenn Sie den Bericht im Berichterstellungstool speichern, wird der aktualisierte Bericht im neuen Berichtsdefinitionsformat gespeichert. Beim Veröffentlichen des Berichts wird dieser zuerst auf Ihrem Computer gespeichert und dann auf dem Berichtsserver veröffentlicht. Sie veröffentlichen die aktualisierte Version des Berichts auf dem Berichtsserver.  
  
 Wenn Sie den Bericht nicht speichern, bleibt der ursprüngliche Bericht unverändert. Sie können nicht jedoch bearbeiten dieses Berichts in der SQL Server 2016-Version von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] oder einer berichterstellungsumgebung, die ein neueres berichterstellungsformat verwendet. Sie können weiterhin die ursprüngliche Version des Berichts durch Hochladen zu einem [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] Berichtsserver über das Webportal. Weitere Informationen finden Sie unter [Webportal](../../reporting-services/web-portal-ssrs-native-mode.md).  
  
 Bei Berichten, die Sie hochladen, statt sie auf einem Berichtsserver zu veröffentlichen, bestimmt der Berichtsprozessor, ob der Bericht bei der ersten Verwendung aktualisiert werden kann. Berichte, die nicht aktualisiert werden können, werden im Abwärtskompatibilitätsmodus verarbeitet und weiterhin wie in der früheren Version von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]angezeigt.  

## <a name="next-steps"></a>Nächste Schritte

[Aktualisieren und Migrieren von Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Wichtige Änderungen in SQL Server Reporting Services in SQLServer 2016](../../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md)   
[Verändertes Verhalten von SQL Server Reporting Services in SQLServer 2016](../../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md)   
[Nicht mehr unterstützte Funktionen in SQL Server Reporting Services in SQLServer 2016](../../reporting-services/behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
[Benutzerdefinierte Berichtselemente](../../reporting-services/custom-report-items/custom-report-items.md)   
[Aktualisieren einer Berichtsserver-Datenbank](../../reporting-services/install-windows/upgrade-a-report-server-database.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
