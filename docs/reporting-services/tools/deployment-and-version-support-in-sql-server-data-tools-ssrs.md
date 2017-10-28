---
title: "Bereitstellung und Versionsunterstützung in SQL Server Data Tools (SSDT) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 36f5686d-7e40-4f31-be81-bd197ca33a02
caps.latest.revision: 19
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: 173d2a355d1084b22bdc90643484dbab2568e0b0
ms.contentlocale: de-de
ms.lasthandoff: 09/06/2017

---
# <a name="deployment-and-version-support-in-sql-server-data-tools-ssdt"></a>Bereitstellung und Versionsunterstützung in SQL Server Data Tools (SSDT)
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] unterstützt die folgenden Szenarien:  
  
-   Öffnen von Berichtsdefinitionen (*.rdl) und Berichtsserverprojekten (\*.rptproj)  
  
-   Erstellen von Berichtsdefinitionen  
  
-   Anzeigen einer Berichtsvorschau im Berichts-Designer  
  
-   Bereitstellen von Berichten auf Berichtsservern  
  
##  <a name="bkmk_ConfigurationandDeploymentProperties"></a> Konfigurations- und Bereitstellungseigenschaften  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] unterstützt Projektkonfigurationen. Eine Projektkonfiguration besteht aus einer Gruppe von Eigenschaften, die Speicherorte und Verhaltensweisen angeben, wenn ein Projekt im Rahmen der Vorschau oder Bereitstellung von Berichten erstellt wird. Weitere Informationen zu Projektkonfigurationen finden Sie in der Visual Studio-Dokumentation.  
  
 Das Upgrade von Berichtsdefinitionen auf Schemaversionen, die mit den Zielberichtsservern kompatibel sind, steuern Sie mithilfe von Projektkonfigurationen. Zu den mittels Projektkonfigurationen gesteuerten Eigenschaften zählen der Zielberichtsserver, der Ordner, in dem der Buildprozess vorübergehend Berichtsdefinitionen für die Vorschau und Bereitstellung speichert, und die Fehlerebenen.  
  
 Berichte werden erstellt, bevor sie als Vorschauberichte im Berichts-Designer gerendert oder auf dem Berichtsserver bereitgestellt werden.  
  
 Sie legen die Konfigurationseigenschaften im Dialogfeld [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] **von** fest.  
  
 Die Erstellungs- und Bereitstellungseigenschaften umfassen:  
  
-   OutputPath ist eine Erstellungseigenschaft, die den Pfad von Ordnern angibt, unter denen die für die Erstellungsüberprüfung, Bereitstellung und Berichtsvorschau verwendete Berichtsdefinition gespeichert wird.  
  
-   ErrorLevel ist eine Erstellungseigenschaft, die den Schweregrad der Erstellungsprobleme identifiziert, die als Fehler gemeldet werden. Probleme mit einem Schweregrad kleiner oder gleich dem Wert von ErrorLevel werden als Fehler gemeldet. Andernfalls werden die Probleme als Warnungen gemeldet. Weitere Informationen finden Sie im Abschnitt "Berichts Berichtsüberprüfung und Fehlerebenen" [Entwerfen von Berichten mit Berichts-Designer &#40; SSRS &#41; ](../../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
-   TargetServerVersion ist eine Bereitstellungseigenschaft, die die erwartete Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] identifiziert, die auf dem in der Eigenschaft „TargetServerURL“ angegebenen Zielberichtsserver installiert ist.  
  
 Wenn Sie die frühere Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im Dialogfeld **Projekteigenschaften** angeben, werden die Berichte nicht automatisch in der früheren Version wiederhergestellt. Das bedeutet, dass ein Berichtsserverprojekt Berichte aus zwei verschiedenen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]enthalten kann. Wenn das Berichtsserverprojekt bereitgestellt wird, werden alle im Projekt enthaltenen Berichte in die Version konvertiert, die in TargetServerVersion angegeben ist.  
  
 Sie können einem Projekt mehr als eine Projektkonfiguration hinzufügen; jede einzelne wird für ein anderes Szenario verwendet, z. B. das Bereitstellen auf verschiedenen Berichtsserverversionen. Weitere Informationen finden Sie unter [Festlegen von Bereitstellungseigenschaften &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md) und unter [Eigenschaftsseiten für Projekt &#40;Dialogfeld&#41;](../../reporting-services/tools/project-property-pages-dialog-box.md).  
  
##  <a name="bkmk_SupportedVersions"></a> Unterstützte Versionen  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], die 32-Bit-Entwicklungsumgebung für berichtsserverprojekte, dient nicht zur Ausführung auf [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]-basierten Computern nicht installiert und wird auf [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]-basierten Servern. Für x64-basierte Computer ist jedoch Support für [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] verfügbar.  
  
 In der nachfolgenden Tabelle werden die unterstützten Versionen zum Verfassen und Veröffentlichen von Berichten in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]erläutert.  
  
> [!NOTE]  
>  Das Schema ist seit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]unverändert.  
  
|Projekt- oder Dateityp|Version|Berichte verfassen|Veröffentlichen von Berichten|Hinweise|  
|--------------------------|-------------|--------------------|---------------------|-----------|  
|Berichtsserverprojekt<br /><br /> oder<br /><br /> Berichtsserver-Assistenten-Projekt|[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]|2016-RDL-Schema|[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]||  
|Berichtsserverprojekt<br /><br /> oder<br /><br /> Berichtsserver-Assistenten-Projekt|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|2014-RDL-Schema|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Berichtsserverprojekt<br /><br /> oder<br /><br /> Berichtsserver-Assistenten-Projekt|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|2012-RDL-Schema|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Berichtsserverprojekt<br /><br /> oder<br /><br /> Berichtsserver-Assistenten-Projekt|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|2008 R2-RDL-Schema|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Berichtsserverprojekt<br /><br /> oder<br /><br /> Berichtsserver-Assistenten-Projekt|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|2008-RDL-Schema|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver|Aktualisiert 2003 RDL und 2005 RDL lokal auf das 2008 RDL-Schema.|  
  
 Weitere Informationen über das Öffnen von Berichten in einer vorherigen Version des Berichtsdefinitionsschemas finden Sie unter [Aktualisieren von Berichten](../../reporting-services/install-windows/upgrade-reports.md). Weitere Informationen zu spezifischen Berichtsdefinitionsschemata finden Sie im [Thema zum Angeben der Berichtsdefinitionssprache](http://go.microsoft.com/fwlink/?linkid=116865).  
  
## <a name="see-also"></a>Siehe auch  
 [Veröffentlichen von Datenquellen und Berichten](../../reporting-services/reports/publishing-data-sources-and-reports.md)  
  
  

