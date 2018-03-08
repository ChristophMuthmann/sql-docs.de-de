---
title: "Programmierung von tabellarischen Modellen für den Kompatibilitätsgrad 1200 | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d343f693-c800-42fe-bb4f-2c38a10919f1
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: c7e1ec3e7ef85cb567d70e96d5c9f3bdd6655f3d
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="tabular-model-programming-for-compatibility-level-1200-and-higher"></a>Tabellarische Programmiermodell für die Kompatibilität auf 1200 und höher
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Beginnen mit dem Kompatibilitätsgrad 1200, tabellarischer Metadaten dient zum Beschreiben der Model-Konstrukten Verlaufsdaten mehrdimensionale Metadaten als Deskriptoren für tabellenmodellobjekte ersetzen. Metadaten für Tabellen, Spalten und Beziehungen werden die Tabelle, Spalte und Beziehung, anstatt die mehrdimensionale Entsprechungen (Dimensionen und Attributtypen).  
  
Sie können Erstellen neuer Modelle mit Kompatibilitätsgrad 1200 oder höher mithilfe der Microsoft.AnalysisServices.Tabular-APIs, die neueste Version von SQL Server Data Tools (SSDT) oder durch Ändern der **CompatibilityLevel** einem vorhandenen tabellarischen Modell zu aktualisieren (auch in SSDT erfolgt). Auf diese Weise bindet das Modell auf neuere Versionen des Servers, Tools und Programmierschnittstellen.   
  
Aktualisieren einer vorhandenen tabellarischen Lösung wird empfohlen, jedoch nicht erforderlich. Vorhandenes Skript und benutzerdefinierte Lösungen, die Zugriff auf oder Verwalten von tabellarischen Modellen oder Datenbanken als verwendet werden-ist. Niedrigeren Kompatibilitätsgraden werden in SQL Server 2016 über die verfügbaren Funktionen auf dieser Ebene vollständig unterstützt. Azure Analysis Services unterstützt nur Kompatibilitätsgrad 1200 oder höher.
  
 Neuer tabellarischer Modelle erfordern verschiedene Code und Skripts, die unten zusammengefasst.  
  
## <a name="object-model-definitions-as-tabular-metadata-constructs"></a>Definitionen von Systemobjekten Modell als tabellarische Metadaten-Konstrukte  
 Die tabellarischen Objektmodell für Modelle von 1200 oder höher verfügbar gemacht wird, im JSON-Format über die [Tabular Model Scripting Language](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) und über die AMO-Datendefinitionssprache durch einen neuen Namespace [ Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)

## <a name="script-for-tabular-models-and-databases"></a>Skript für tabellarische Modelle und Datenbanken  
 TMSL ist eine JSON-Skriptsprache für tabellarische Modelle mit Unterstützung für das Erstellen, lesen, Update, Delete-Vorgänge. Aktualisieren von Daten über TMSL kann und Aufrufen von Datenbankvorgänge für anfügen, trenne, Sicherung, Wiederherstellung und synchronisieren.  
  
 AMO PowerShell akzeptiert TMSL-Skript als Eingabe.  
  
 Finden Sie unter [Tabular Model Scripting Language &#40; TMSL &#41; Verweis](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) und [Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md) für Weitere Informationen.  
  
## <a name="query-languages"></a>Abfragesprachen  
 DAX und MDX, werden für alle tabellarischen Modelle unterstützt.  
  
## <a name="expression-language"></a>Expression-Sprache  
 Filtern und Ausdrücken verwendet, um berechnete Objekte, einschließlich Measures und KPIs erstellen, werden in DAX formuliert. Finden Sie unter [Grundlegendes zu DAX in tabellarischen Modellen](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md) und [Data Analysis Expressions &#40; DAX &#41; in Analysis Services](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5).  
  
## <a name="managed-code-for-tabular-models-and-databases"></a>Verwalteter Code für tabellarische Modelle und Datenbanken  
 AMO umfasst einen neuen Namespace, Microsoft.AnalysisServices.Tabular, für das Arbeiten mit Modellen programmgesteuert an. Finden Sie unter ["Microsoft.AnalysisServices" Namespace](https://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx) für Weitere Informationen.  
  
> [!NOTE]  
>  Analysis Services Management Objects (AMO), ADOMD.NET und tabellarischen Objekts Modell (TOM) Client-Bibliotheken jetzt als Ziel .NET 4.0-Laufzeit verwenden.   
  
## <a name="see-also"></a>Siehe auch  
 [Entwicklerhandbuch (Analysis Services)](../../analysis-services/analysis-services-developer-documentation.md)   
 [Programmierung von tabellarischen Modellen aus Kompatibilitätsgründen Ebenen 1050 bis 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)   
 [Technische Referenz ](../../analysis-services/powershell/technical-reference-ssas.md) [Aktualisieren von Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
 [Kompatibilitätsgrade für tabellarische Modelle und Datenbanken](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)  
  
  
