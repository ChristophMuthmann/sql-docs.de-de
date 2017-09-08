---
title: Definitionen von Systemobjekten im tabellarischen Modell Scripting Language (TMSL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 486f0507-cec6-4672-b947-0bb61d1cbc46
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3f69f6b59054b7fb1880757271b290874448373d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="tmsl-reference---tabular-objects"></a>TMSL-Verweis - tabellarische Objekte

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Anwendungen, die zu erstellen, verwenden oder Verwalten von tabellendatenbanken oder, die eine Verbindung mit einer SQL Server 2016 Analysis Services-Instanz im tabellarischen Modus herstellen, können die tabellarische Tabular Model Scripting Language (TMSL) für Befehle und Objekt-Darstellungen im JSON-Format verwenden.  
  
 Dieser Artikel beschreibt die wichtigsten Objekte des TMSL-Schemas, die von SQL Server Management Studio, SQL Server Data Tools (SSDT) und AMO PowerShell generierten Skripts verwendet.  
  
 Definitionen von Systemobjekten sind im JSON-Format und verwendet in TMSL-Befehle wie CREATE-, Alter- und löschen. Finden Sie unter [Befehle im tabellarischen Modell Scripting Language &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md) eine Liste der Befehle.  
  
## <a name="main-objects"></a>Hauptobjekte  
 In der folgenden Tabelle wird die Liste der am häufigsten verwendeten Objekte im TMSL-Skript.  
  
|||  
|-|-|  
|[Datenbankobjekt &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)|Definiert eine tabellarische Datenbank mit Kompatibilitätsgrad 1200 oder höher, auf Grundlage eines Modells der gleichen Ebene.|  
|[Modellobjekt &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md)|Definiert ein tabellarisches Modell mit Kompatibilitätsgrad 1200 oder höher.|  
|[DataSources Object &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)|Definiert eine Verbindung mit einer Datenquelle, die während des Imports auf das Modell geladen werden oder für Pass-through-Abfragen verwendet werden, wenn das Modell im DirectQuery-Modus befindet.|  
|[Tables-Objekt &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)|Gibt den Tabellen des Modells an.|  
|[Partitionen Object &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)|Definiert die Speicherung der Tabelle Schemarowsets, einschließlich der berechnete Tabellen.|  
|[Beziehungen Object &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md)|Definiert die Beziehungen zwischen Tabellen.|  
|[Rollen Object &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)|Definiert Berechtigungen, Mitgliedschaft und Sicherheitsfilter, das Steuern des Zugriffs auf Daten und Vorgänge.|  
  
## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
