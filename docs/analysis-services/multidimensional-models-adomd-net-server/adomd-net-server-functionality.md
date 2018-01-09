---
title: "ADOMD.NET-Serverfunktionalität | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- functionality [ADOMD.NET]
- ADOMD.NET, functionality
ms.assetid: b74c6957-3f64-4e09-aa09-d06ee93f82fa
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c38c2d4ca012a9b7082ee1a8542b45d053db29fe
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="adomdnet-server-functionality"></a>ADOMD.NET-Serverfunktionalität
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Alle ADOMD.NET-Serverobjekte bieten nur-Lese Zugriff auf die Daten und Metadaten auf dem Server. Verwenden Sie das ADOMD.NET-Serverobjektmodell, um Daten und Metadaten abzurufen, da das Serverobjektmodell keine Schemarowsets unterstützt.  
  
 Mit ADOMD.NET-Serverobjekten können Sie eine benutzerdefinierte Funktion (UDF) oder eine gespeicherte Prozedur zum Erstellen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Diese prozessinternen Methoden werden durch Abfrageanweisungen aufgerufen, die in Sprachen wie Multidimensional Expressions (MDX), Data Mining Extensions (DMX) oder SQL erstellt wurden. Diese prozessinternen Methoden stellen zudem zusätzliche Funktionen bereit, die nicht den Wartezeiten eines Netzwerks unterworfen sind.  
  
> [!NOTE]  
>  Das <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand>-Objekt unterstützt nur DMX.  
  
## <a name="what-is-a-udf"></a>Was ist eine UDF?  
 Ein *UDF* ist eine Methode, die über die folgenden Eigenschaften verfügt:  
  
-   Sie können die UDF im Kontext einer Abfrage aufrufen.  
  
-   Die UDF unterstützt eine beliebige Anzahl von Parametern.  
  
-   Die UDF kann zahlreiche Datentypen zurückgeben.  
  
 Im folgenden Beispiel wird die fiktive UDF `FinalSalesNumber` verwendet:  
  
```  
SELECT SalesPerson.Name ON ROWS,  
       FinalSalesNumber() ON COLUMNS  
FROM SalesModel  
```  
  
## <a name="what-is-a-stored-procedure"></a>Was ist eine gespeichert Prozedur?  
 Ein *gespeicherte Prozedur* ist eine Methode, die über die folgenden Eigenschaften verfügt:  
  
-   Sie rufen Sie eine gespeicherte Prozedur auf eigene mit MDX [Aufrufen](../../mdx/mdx-data-manipulation-call.md) Anweisung.  
  
-   Eine gespeicherte Prozedur unterstützt eine beliebige Anzahl von Parametern.  
  
-   Eine gespeicherte Prozedur kann einen Dataset Zurückgeben einer **IDataReader**, oder ein leeres Ergebnis.  
  
 Im folgenden Beispiel wird die fiktive gespeicherte Prozedur `FinalSalesNumbers` verwendet:  
  
```  
CALL FinalSalesNumbers()  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ADOMD.NET-Serverprogrammierung](../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
