---
title: Datengesteuerte Abonnements | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: ba009f62-0d4f-45e7-a27c-36fd5f0cd3a8
caps.latest.revision: 56
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3e4ffac2b4342d0f8b3c30a9d76cdc7b0ecf098c
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="data-driven-subscriptions"></a>Datengesteuerte Abonnements
  Ein datengesteuertes Abonnement bietet eine Möglichkeit, dynamische Abonnementdaten zu verwenden, die zur Laufzeit aus einer externen Datenquelle abgerufen werden. Mit einem datengesteuerten Abonnement können auch statischer Text und Standardwerte verwendet werden, die Sie beim Definieren des Abonnements angeben. Sie können datengesteuerte Abonnements für die folgenden Aufgaben verwenden:  
  
-   Verteilen eines Berichts an eine ständig wechselnde Liste von Abonnenten. Beispielsweise können Sie mit datengesteuerten Abonnements einen Bericht in einer großen Organisation verteilen, in der die Abonnenten von Monat zu Monat variieren. Sie können aber auch sonstige Kriterien verwenden, um die Gruppenmitgliedschaft aus einer Gruppe vorhandener Benutzer zu bestimmen.  
  
-   Filtern der Berichtsausgabe mithilfe von zur Laufzeit abgerufenen Berichtsparameterwerten.  
  
-   Ändern der Berichtsausgabeformate und Übermittlungsoptionen für jede Berichtsübermittlung.  
  
 Ein datengesteuertes Abonnement besteht aus mehreren Teilen. Die festen Komponenten eines datengesteuerten Abonnements werden beim Erstellen des Abonnements definiert. Dazu zählen u. a. die folgenden:  
  
-   Der Bericht, für den das Abonnement definiert wurde (ein Abonnement ist immer einem einzelnen Bericht zugeordnet).  
  
-   Die Übermittlungserweiterung, die zum Verteilen des Berichts verwendet wurde. Sie können die E-Mail-Übermittlungserweiterung des Berichtsservers, eine Dateifreigabe-Übermittlungserweiterung, den NULL-Übermittlungsanbieter zum Vorabladen des Caches oder eine benutzerdefinierte Übermittlungserweiterung angeben. Innerhalb eines einzelnen Abonnements können Sie nicht mehrere Übermittlungserweiterungen angeben.  
  
-   Die Abonnentendatenquelle. Sie müssen beim Definieren des Abonnements eine Verbindungszeichenfolge für die Datenquelle mit Abonnentendaten angeben. Die Abonnentendatenquelle kann nicht dynamisch zur Laufzeit angegeben werden.  
  
-   Beim Definieren des Abonnements muss die zum Auswählen von Abonnentendaten verwendete Abfrage angegeben werden. Sie können die Abfrage zur Laufzeit nicht ändern.  
  
 Die in einem datengesteuerten Abonnement verwendeten dynamischen Daten werden abgerufen, wenn das Abonnement verarbeitet wird. Beispiele für Daten, die Sie in einem Abonnement verwenden können, sind der Abonnentenname, die E-Mail-Adresse, das bevorzugte Berichtsausgabeformat oder beliebige Werte, die für Berichtsparameter gültig sind. Sie können in einem datengesteuerten Abonnement dynamische Werte verwenden, wenn Sie Sie eine Zuordnung zwischen den bei einer Abfrage zurückgegebenen Feldern und bestimmten Übermittlungsoptionen sowie Berichtsparametern definieren. Bei der Verarbeitung des Abonnements werden jeweils variable Daten aus einer Abonnentendatenquelle abgerufen.  
  
## <a name="requirements-for-using-data-driven-subscriptions"></a>Anforderungen für die Verwendung datengesteuerter Abonnements  
 Die Funktion für datengesteuerte Abonnements ist nicht in allen Editionen verfügbar. Zudem bestehen Einschränkungen hinsichtlich der Arten von Datenquellen, die Sie zur Laufzeit zum Abrufen von Abonnementdaten verwenden können. Die folgende Liste enthält weitere Informationen zu den Anforderungen:  
  
-   Weitere Informationen zu den Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die die Funktion für datengesteuerte Abonnements unterstützen, finden Sie unter [Von den SQL Server 2012-Editionen unterstützte Funktionen](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
-   Wählen Sie für Abonnementdaten eine Datenquelle aus, die Schemainformationen für den Berichtsserver bereitstellen kann. Beispiele für unterstützte Datenquellentypen sind relationale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten, Oracle, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbanken, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketdaten, ODBC-Datenquellen und OLE DB-Datenquellen. Weitere Informationen zu den Anforderungen an Abonnentendatenquellen finden Sie unter [Verwenden einer externen Datenquelle für Abonnentendaten &#40;datengesteuertes Abonnement&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md).  
  
## <a name="working-with-data-driven-subscriptions"></a>Arbeiten mit datengesteuerten Abonnements  
 Die folgenden Themen enthalten weitere Informationen zu datengesteuerten Abonnements.  
  
|Themen|Description|  
|------------|-----------------|  
|[Erstellen, Ändern und Löschen von datengesteuerten Abonnements](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)|Erläutert das Erstellen, Ändern oder Löschen eines datengesteuerten Abonnements.|  
|[Verwenden einer externen Datenquelle für Abonnentendaten &#40;datengesteuertes Abonnement&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)|Enthält Informationen zu den Datenquellen, die Sie für ein datengesteuertes Abonnement verwenden können.|  
|[Erstellen eines datengesteuerten Abonnements &#40;SSRS-Tutorial&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)|Enthält schrittweise Anleitungen zum Erstellen eines datengesteuerten Abonnements.|  
|[Zwischenspeichern von Berichten &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)|Beschreibt die Verwendung des NULL-Übermittlungsanbieters mit einem datengesteuerten Abonnement, um den Cache vorab zu laden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Abonnements und Übermittlung &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Datengesteuertes Abonnement erstellen &#40;Seite, Berichts-Manager&#41;](http://msdn.microsoft.com/library/814b4653-572a-48c7-847f-b310ba0f3046)   
 [Vorabladen des Caches &#40;Berichts-Manager&#41;](../../reporting-services/report-server/preload-the-cache-report-manager.md)  
  
  
