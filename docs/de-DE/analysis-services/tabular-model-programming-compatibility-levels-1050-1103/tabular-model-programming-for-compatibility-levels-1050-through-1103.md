---
title: Programmierung von tabellarischen Modellen aus Kompatibilitätsgründen Ebenen 1050 bis 1103 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0ceb461e-12c1-44ea-97ac-b99bf308676b
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7008c37fd23f351f1e20a09fe3454a1dc8a7f688
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="tabular-model-programming-for-compatibility-levels-1050-through-1103"></a>Programmierung von tabellarischen Modellen aus Kompatibilitätsgründen Ebenen 1050 bis 1103
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Tabellarische Modelle verwenden relationale Konstrukte, um die von Analyse- und Berichtsanwendungen verwendeten Analysis Services-Daten zu modellieren. Diese Modelle werden auf einer Analysis Service-Instanz ausgeführt, die für den Tabellenmodus konfiguriert ist, und zwar mithilfe eines Moduls für Datenanalyse im Arbeitsspeicher für einen Speicher und schnelle Tabellenscans, mit denen Daten nach Bedarf aggregiert und berechnet werden.  
  
 Wenn die Anforderungen der benutzerdefinierten BI-Lösung am besten von einer tabellarischen Modelldatenbank erfüllt werden, können Sie eine beliebige der Analysis Services-Clientbibliotheken und -Programmierschnittstellen verwenden, um die Anwendung auf einer Analysis Services-Instanz in tabellarische Modelle zu integrieren. Sie können entweder eingebettete MDX oder DAX im Code verwenden, um tabellarische Modelldaten abzufragen und zu berechnen.  
  
 Für tabellarische Modelle, die in früheren Versionen von Analysis Services, in bestimmten Kompatibilitätsgrade 1050 bis 1103-Modelle erstellt die Arbeit mit programmgesteuert in AMO, ADOMD.NET, XMLA oder OLE DB-Objekte sind im Grunde identisch für beide tabellarische und mehrdimensionale Lösungen. Insbesondere wird die Objektmetadaten für mehrdimensionale Modelle definiert auch für tabellarische Modelle Kompatibilitätsgrade 1050-1103 verwendet.  
  
 Ab SQL Server 2016 können tabellarische Modelle erstellt oder aktualisiert auf den 1200 oder höher Kompatibilitätsgrad, der tabellarischen Metadaten zum Definieren des Modells verwendet werden. Auf dieser Ebene sind Metadaten und Programmierbarkeit grundlegend. Finden Sie unter [tabellarische Programmiermodell für die Kompatibilität auf 1200 und höher](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md) und [Aktualisieren von Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) für Weitere Informationen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [CSDL-Anmerkungen für Business Intelligence & #40; CSDLBI & #41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
 [Informationen zum tabellarischen Objektmodell auf Kompatibilität Ebenen 1050 bis 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
 [Technische Referenz für BI-Anmerkungen zu CSDL](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  

[IMDEmbeddedData-Schnittstelle](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/imdembeddeddata-interface.md)


  
  
