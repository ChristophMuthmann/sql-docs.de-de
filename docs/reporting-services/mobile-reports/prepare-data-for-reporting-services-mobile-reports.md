---
title: "Vorbereiten von Daten für mobile Berichte von Reporting Services | Microsoft-Dokumentation"
ms.custom: 
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8adce9ad-6a08-4d20-b1cf-d3c45544d8de
caps.latest.revision: "15"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: eb1b7514e8ba88f4dacf3a521f6deb0d934dfa2d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="prepare-data-for-reporting-services-mobile-reports"></a>Vorbereiten von Daten für mobile Berichte von Reporting Services
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] unterstützt eine Reihe von komplexen Datenvorgängen, einschließlich Filterung, Aggregation und Erstellen von Zeitscheiben. Dieser Artikel enthält einige Aspekte, die beim Vorbereiten von Daten berücksichtigt werden sollten. Daten vorab zu aggregieren, kann sowohl die Erstellung als auch die Verwendung mobiler Berichte optimieren. Zudem wird dies von einigen Designs für mobile Berichte benötigt.   
  
## <a name="date-and-time-formats"></a>Datums- und Zeitformate 
Beim Umgang mit Datum/Uhrzeit-Intervallen zur Verwendung in einem mobilen Bericht, vor allem mit dem Zeitnavigator, ist es wichtig, die Datum/Uhrzeit-Spalte ordnungsgemäß zu formatieren, damit der [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] sie als solche identifizieren kann. Nachstehend finden Sie Beispiele für gültige Datum/Uhrzeit-Formate:  
  
    05/01/2009    
    2009-05-01    
    05/01/2009 14:57:32.8    
    2009-05-01 14:57:32.8    
    2009-05-01T14:57:32.8375298-04:00    
    5/01/2008 14:57:32.80 -07:00    
    1 May 2008 2:57:32.8 PM    
    Fri, 15 May 2009 20:10:57 GMT    
  
Datum- und uhrzeitbasierte Datasets können in den meisten Fällen durch ein oder mehrere Datum/Uhrzeit-Intervalle beschrieben werden, z.B. stündlich, täglich, monatlich, vierteljährlich und jährlich. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] kann mehrere Tabellen verschiedener Granularität kombinieren und in einem einzelnen mobilen Bericht anzeigen. Behalten Sie jedoch die relevanten Intervalle aus dem/den ursprünglichen Dataset(s) im Hinterkopf, da diese Ihnen helfen können, wenn Sie entscheiden, welche Datum/Uhrzeit-Filteroptionen Sie dem Benutzer im endgültigen mobilen Bericht präsentieren.  

Datumsfelder in mehrdimensionalen und tabellarischen [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] -Modellen können in freigegebenen Datasets ihre Datumsformatierung verlieren. Suchen Sie unter [Retain date formatting for Analysis Services in mobile reports](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md) (Datumsformatierung für Analysis Services in mobilen Berichten beibehalten) nach einer Lösung, die die Formatierung beibehält.
  
## <a name="preparing-filter-data"></a>Vorbereiten von Filterdaten ##  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] kann Daten sowohl auf Datum/Uhrzeit-Feldern als auch Schlüsselfeldern basierend filtern. Obwohl Schlüsselfelder numerisch sind, handelt sich dabei in den meisten Fällen um eine ID oder einen Zeichenfolgenwert. Zum Vorbereiten eines Filterfelds für die Verwendung mit einem Navigatorelement, wie der Auswahlliste, sollte der Filterschlüssel eine einzelne Spalte in der Datentabelle sein. Auf diese Weise können Sie die Tabellenzeilen entsprechend dem Wert in der Filterspalte gruppieren. Durch mehrere Spalten mit verschiedenen Filterschlüsseln oder Filterkriterien können mobile Berichte mit mehreren Filternavigatoren zusammen hierarchisch oder einzeln verwendet werden.  
  
| Branche  | Country   | Region    |  
| ------------- | ------------- | ------------- |  
| Banken     | AFGHANISTAN   | ASIEN      |  
| Kommerzielle und professionelle Dienstleistungen | AFGHANISTAN | ASIEN |  
| Essen, Getränke und Tabak | AFGHANISTAN | ASIEN |  
| Medien | AFGHANISTAN | ASIEN |  
| Arzneimittel | AFGHANISTAN | ASIEN |  
| Lebensmittel- und Basisartikeleinzelhandel | ALBANIEN | EUROPA |  
  
  
Schlüsselbasierte Filter können für die Verwendung mit einer Auswahlliste auch in einer Baumstruktur hierarchisch strukturiert sein. Zum Vorbereiten von Daten zur Verwendung in dieser Art von Szenario erstellen Sie eine Nachschlagetabelle, die die hierarchische Struktur beschreibt. Verwenden Sie eine Tabellenstruktur, die eine Schlüsselspalte und eine übergeordnete Schlüsselspalte enthält, um anzugeben, wo in der gesamten Hierarchie ein Knoten hingehört.  
  
In dieser Tabelle werden die ParentKey-Elemente zunächst in der ItemKey-Spalte und dann in der ParentItemKey-Spalte neben ihren untergeordneten Elementen aufgelistet.   
  
|ItemKey    | ParentItemKey |  
| ------------- | ------------- |  
| Finanzen    |   |  
| Industrie   |   |  
| Basiskonsumgüter |    |  
| Nicht-Basiskonsumgüter |  |     
| Gesundheitswesen   |   |  
| Informationstechnologie |  |  
| Banken | Finanzen |  
| Immobilien | Finanzen |  
| Diversifizierte Finanzunternehmen |  Finanzen |   
| Versicherung |   Finanzen |  
| Kommerzielle und professionelle Dienstleistungen |  Industrie |  
| Investitionsgüter |   Industrie |  
| Transport |  Industrie |  
| Essen, Getränke und Tabak |    Basiskonsumgüter |  
| Lebensmittel- und Basisartikeleinzelhandel |    Basiskonsumgüter |  
| Haushalts- und persönliche Produkte | Basiskonsumgüter |  
| Medien | Nicht-Basiskonsumgüter |  
| Automobile und Komponenten |  Nicht-Basiskonsumgüter |  
| Gebrauchsgüter und Kleidung |Nicht-Basiskonsumgüter |  
| Verbraucherdienste |   Nicht-Basiskonsumgüter |  
| Einzelhandel | Nicht-Basiskonsumgüter |  
| Arzneimittel   | Gesundheitswesen |  
| Medizinische Geräte und Dienstleistungen |    Gesundheitswesen |  
| Software und Dienstleistungen | Informationstechnologie |  
| Technologie-Hardware und -Geräte   | Informationstechnologie |  
| Telekommunikationsdienste |Informationstechnologie |  
  
### <a name="see-also"></a>Siehe auch  
- [Vorbereiten von Excel-Daten für mobile Berichte von Reporting Services](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md)  
- [Retain date formatting for Analysis Services in mobile reports](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md)
- [Erstellen und Veröffentlichen von mobilen Berichten mit dem Publisher für mobile Berichte von SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
  
  
  

