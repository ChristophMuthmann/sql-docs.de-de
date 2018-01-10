---
title: ODBC-Verbindungstyp (SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 24163866-f37a-4c38-982e-c3d79bf64d4c
caps.latest.revision: "8"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 102ad01b7e4246ce01c635ffe6e54a0bfdd0f78c
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="odbc-connection-type-ssrs"></a>OBDC-Verbindungstyp (SSRS)
  Wenn Sie Daten von einem ODBC-Datenanbieter einschließen möchten, benötigen Sie ein Dataset, das auf einer Berichtsdatenquelle vom Typ "ODBC" basiert. Dieser integrierte Datenquellentyp basiert auf der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -ODBC-Datenverarbeitungserweiterung.  
  
 Verwenden Sie die Informationen in diesem Thema, um eine Datenquelle zu erstellen. Eine Schritt-für-Schritt-Anleitung finden Sie unter [Hinzufügen und Prüfen einer Datenverbindung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Verbindungszeichenfolge  
 Die Verbindungszeichenfolge für die ODBC-Datenverarbeitungserweiterung hängt vom gewünschten ODBC-Treiber ab. Eine typische Verbindungszeichenfolge enthält Name-Wert-Paare, die vom Treiber unterstützt werden. Die folgende Verbindungszeichenfolge gibt z. B. den ODBC-Treiber für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client und die AdventureWorks-Datenbank an:  
  
```  
Driver={SQL Server Native Client 10.0};Server=server;Database=AdventureWorks;Trusted_Connection=yes;  
```  
  
  
##  <a name="Credentials"></a> Anmeldeinformationen  
 Anmeldeinformationen sind erforderlich, um Abfragen auszuführen und den Bericht lokal oder vom Berichtsserver aus in der Vorschau anzuzeigen.  
  
 Nachdem Sie den Bericht veröffentlicht haben, müssen Sie eventuell die Anmeldeinformationen für die Datenquelle ändern, sodass die Berechtigungen zum Abrufen der Daten beim Ausführen des Berichts auf dem Berichtsserver gültig sind.  
  
 Wenn Sie die ODBC-Datenquelle so konfigurieren, dass ein Kennwort angegeben werden muss oder das Kennwort in der Verbindungszeichenfolge enthalten ist, und Benutzer das Kennwort mit Sonderzeichen (z. B. Satzzeichen) eingeben, können einige zugrunde liegende Datenquellentreiber die Sonderzeichen nicht überprüfen. Beim Verarbeiten des Berichts kann die Meldung "Kein zulässiges Kennwort" auf dieses Problem hinweisen. Wenn das Kennwort nicht geändert werden kann, können Sie mit Ihrem Datenbankadministrator Maßnahmen ergreifen, damit die entsprechenden Anmeldeinformationen auf dem Berichtsserver als Teil eines ODBC-Datenquellennamens des Systems (Data Source Name oder DSN) gespeichert werden. Weitere Informationen finden Sie unter "OdbcConnection.ConnectionString" in der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK-Dokumentation.  
  
> [!NOTE]  
>  Es wird empfohlen, der Verbindungszeichenfolge keine Anmeldeinformationen (z. B. Kennwörter) hinzuzufügen. Der Berichts-Generator enthält eine separate Registerkarte im Dialogfeld **Datenquelle** , auf der Sie Anmeldeinformationen eingeben können.  
  
 Weitere Informationen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) und [Angeben von Anmeldeinformationen im Berichts-Generator](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
  
##  <a name="Remarks"></a> Hinweise  
 ODBC ist eine frühe Datenzugriffstechnologie, die OLEDB vorausgegangen ist. ODBC unterstützt nur relationale Datenquellen. ODBC-Datenanbieter werden als *Treiber*bezeichnet. ODBC-Treiber werden von Microsoft und Drittanbietern bereitgestellt. Microsoft Office installiert z. B. ODBC-Treiber, die eine Verbindung mit Office-Dateiformaten herstellen.  
  
 Bevor Sie eine ODBC-Verbindungszeichenfolge erstellen können, müssen Sie ODBC-Treiber installieren und einen Computer- oder System-DSN erstellen. Zum erfolgreichen Abrufen der gewünschten Daten muss eine vom Treiber unterstützte Abfragesyntax angegeben werden. Die Parameterunterstützung variiert abhängig vom Treiber. Weitere Informationen finden Sie in den spezifischen Themen für den ausgewählten Treiber, z.B. [SQL Server Native Client (ODBC)](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md).  
  
###### <a name="platform-and-version-information"></a>Plattform- und Versionsinformationen  
 Weitere Informationen zur bestimmten ODBC-Datenanbietern finden Sie unter [Von Reporting Services unterstützte Datenquellen &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) in der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Dokumentation der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-[Onlinedokumentation](http://go.microsoft.com/fwlink/?linkid=121312).  
  
  
##  <a name="HowTo"></a> Themen zur Vorgehensweise  
 Dieser Abschnitt enthält schrittweise Anweisungen zum Arbeiten mit Datenverbindungen, Datenquellen und Datasets.  
  
 [Hinzufügen und Prüfen einer Datenverbindung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Erstellen eines freigegebenen Datasets oder eingebetteten Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Hinzufügen eines Filters zu einem Dataset &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> Verwandte Abschnitte  
 Diese Abschnitte der Dokumentation enthalten umfassende grundlegende Informationen zu Berichtsdaten sowie Informationen zum Definieren, Anpassen und Verwenden der mit Daten zusammenhängenden Teile eines Berichts.  
  
 [Berichtsdatasets &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Bietet eine Übersicht über den Zugriff auf Daten für den Bericht.  
  
 [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen in Berichts-Generator](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 Enthält Informationen zu Datenverbindungen und Datenquellen.  
  
 [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Enthält Informationen zu eingebetteten und freigegebenen Datasets.  
  
 [Datasetfelder-Sammlung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Enthält Informationen zur von der Abfrage generierten Datasetfeldauflistung.  
  
 [Von Reporting Services unterstützte Datenquellen (SSRS)](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) in der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Dokumentation der [Onlinedokumentation](http://go.microsoft.com/fwlink/?linkid=121312) zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Enthält ausführliche Informationen zur Plattform- und Versionsunterstützung für die einzelnen Datenerweiterungen.  
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
