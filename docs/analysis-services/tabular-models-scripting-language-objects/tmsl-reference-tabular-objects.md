---
title: Definitionen von Systemobjekten im tabellarischen Modell Scripting Language (TMSL) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 486f0507-cec6-4672-b947-0bb61d1cbc46
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ff54b2a0d18f11b637c448fdf2c76787581e5459
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="tmsl-reference---tabular-objects"></a>TMSL-Verweis - tabellarische Objekte
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Anwendungen, die zu erstellen, verwenden oder Verwalten von tabellendatenbanken oder, die eine Verbindung mit einer SQL Server 2016 Analysis Services-Instanz im tabellarischen Modus herstellen, können die tabellarische Tabular Model Scripting Language (TMSL) für Befehle und Objekt-Darstellungen im JSON-Format verwenden.  
  
 Dieser Artikel beschreibt die wichtigsten Objekte des TMSL-Schemas, die von SQL Server Management Studio, SQL Server Data Tools (SSDT) und AMO PowerShell generierten Skripts verwendet.  
  
 Definitionen von Systemobjekten sind im JSON-Format und verwendet in TMSL-Befehle wie CREATE-, Alter- und löschen. Finden Sie unter [Befehle in Tabular Model Scripting Language &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md) eine Liste der Befehle.  
  
## <a name="main-objects"></a>Hauptobjekte  
 In der folgenden Tabelle wird die Liste der am häufigsten verwendeten Objekte im TMSL-Skript.  
  
|||  
|-|-|  
|[Datenbankobjekt &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)|Definiert eine tabellarische Datenbank mit Kompatibilitätsgrad 1200 oder höher, auf Grundlage eines Modells der gleichen Ebene.|  
|[Modellobjekt &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md)|Definiert ein tabellarisches Modell mit Kompatibilitätsgrad 1200 oder höher.|  
|[DataSources-Objekt &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)|Definiert eine Verbindung mit einer Datenquelle, die während des Imports auf das Modell geladen werden oder für Pass-through-Abfragen verwendet werden, wenn das Modell im DirectQuery-Modus befindet.|  
|[Tables-Objekt &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)|Gibt den Tabellen des Modells an.|  
|[Partitionen Objekt &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)|Definiert die Speicherung der Tabelle Schemarowsets, einschließlich der berechnete Tabellen.|  
|[Beziehungen Objekt &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md)|Definiert die Beziehungen zwischen Tabellen.|  
|[Rollenobjekt &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)|Definiert Berechtigungen, Mitgliedschaft und Sicherheitsfilter, das Steuern des Zugriffs auf Daten und Vorgänge.|  
  
## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
