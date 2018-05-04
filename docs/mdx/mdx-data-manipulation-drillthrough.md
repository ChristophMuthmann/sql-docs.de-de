---
title: DRILLTHROUGH-Anweisung (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DRILLTHROUGH
dev_langs:
- kbMDX
helpviewer_keywords:
- DRILLTHROUGH statement
- retrieving data
- data retrieval [MDX]
ms.assetid: dfa22755-0ed4-4bba-9c31-7ade26d9ebdb
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: ed158039ec7d6a4f969ef155542599821daa5fb7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-manipulation---drillthrough"></a>Datenbearbeitung für MDX - DRILLTHROUGH
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ruft die zugrunde liegenden Tabellenzeilen ab, die zum Erstellen einer bestimmten Zelle in einem Cube verwendet wurden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DRILLTHROUGH[MAXROWSUnsigned_Integer]   
      <MDX SELECT statement>   
      [RETURNSet_of_Attributes_and_Measures   
            [,Set_of_Attributes_and_Measures ...]  
      ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Unsigned_Integer*  
 Ein positiver ganzzahliger Wert  
  
 *MDX-SELECT-Anweisung*  
 Eine gültige SELECT-Anweisung in MDX (Multidimensional Expressions)  
  
 *Set_of_Attributes_and_Measures*  
 Eine Liste mit durch Trennzeichen getrennten Dimensionsattributen und Measures  
  
## <a name="remarks"></a>Hinweise  
 Drillthrough ist ein Vorgang, bei dem ein Endbenutzer eine einzelne Zelle in einem Cube auswählt und ein Resultset aus den Quelldaten dieser Zelle abruft, um detailliertere Informationen zu erhalten. Standardmäßig wird ein Drillthrough-Resultset aus den Tabellenzellen abgeleitet, die zur Berechnung des Werts der ausgewählten Cubezelle ausgewertet wurden. Endbenutzer können einen Drillthrough nur dann durchführen, wenn die Clientanwendung diese Funktion unterstützt. In [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], die Ergebnisse direkt aus dem MOLAP-Speicher abgerufen werden, es sei denn, die ROLAP-Partition oder-Dimension abgefragt werden.  
  
> [!IMPORTANT]  
>  Die Drillthrough-Sicherheit basiert auf den für den Cube definierten allgemeinen Sicherheitsoptionen. Erhält ein Benutzer auf bestimmte Daten keinen Zugriff über MDX, ist sein Zugriff über Drillthrough auf genau die gleiche Weise eingeschränkt.  
  
 Eine MDX-Anweisung gibt die betreffende Zelle an. Der Wert von der **MAXROWS** Argument gibt die maximale Anzahl von Zeilen, die von der sich ergebende Rowset zurückgegeben werden soll.  
  
 Standardmäßig werden maximal 10.000 Zeilen zurückgegeben. Dies bedeutet, dass, wenn Sie lassen **MAXROWS** nicht angegeben wurde, erhalten Sie 10.000 Zeilen oder weniger. Wenn dieser Wert für Ihr Szenario zu niedrig ist, legen Sie **MAXROWS** auf eine höhere Zahl wie z. B. `MAXROWS 20000`. Wenn sie insgesamt zu niedrig ist, können Sie die Standardeinstellung steigern, durch Ändern der **OLAP\Query\DefaultDrillthroughMaxRows** Servereigenschaft. Weitere Informationen zum Ändern dieser Eigenschaft finden Sie unter [Servereigenschaften in Analysis Services](../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 Sofern nicht anders angegeben, enthalten die zurückgegebenen Spalten alle Granularitätsattribute aller Dimensionen, die mit der Measuregruppe des angegebenen Measures verbunden sind und keine m:n-Dimensionen sind. Cubedimensionen ist zur Unterscheidung von Dimensionen und Measuregruppen ein $-Zeichen vorangestellt. Die **zurückgeben** -Klausel wird verwendet, um die von der Drillthroughabfrage zurückgegebenen Spalten anzugeben. Die folgenden Funktionen kann angewendet werden, um ein einzelnes Attribut oder measure der **zurückgeben** Klausel.  
  
 Name(attribute_name)  
 Gibt den Namen des angegebenen Attributelements zurück.  
  
 UniqueName(attribute_name)  
 Gibt den eindeutigen Namen des angegebenen Attributelements zurück.  
  
 Key(attribute_name[, N])  
 Gibt den Schlüssel des angegebenen Attributelements zurück, wobei N die Spalte im zusammengesetzten Schlüssel (sofern vorhanden) angibt. Der Standardwert für N ist 1.  
  
 Caption(attribute_name)  
 Gibt die Beschriftung des angegebenen Attributelements zurück.  
  
 MemberValue(attribute_name)  
 Gibt den Elementwert des angegebenen Attributelements zurück.  
  
 CustomRollup(attribute_name)  
 Gibt den benutzerdefinierte Rollupausdruck für das angegebene Attributelement zurück.  
  
 CustomRollupProperties(attribute_name)  
 Gibt die benutzerdefinierte Rollupeigenschaft für das angegebene Attributelement zurück.  
  
 UnaryOperator(attribute_name)  
 Gibt den unären Operator des angegebenen Attributelements zurück.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Zelle für den Monat Juli 2007 für das Reseller Sales Amount-Measure (das Standardmeasure) für das Land Australien angegeben. Die RETURN-Klausel gibt an, dass die der Zelle zugrunde liegenden Werte Datum jedes Verkaufs, Produktmodellname, Mitarbeitername, Betrag der Verkäufe, Steuerbetrag sowie Produktkosten zurückgegeben werden sollen.  
  
```  
DRILLTHROUGH  
SELECT  
   ([Date].[Calendar].[Month].[July 2007])  
ON 0   
FROM [Adventure Works]  
WHERE [Geography].[Country].[Australia]  
RETURN   
  [$Date].[Date]  
  ,KEY([$Product].[Model Name])  
  ,NAME([$Employee].[Employee])  
  ,[Reseller Sales].[Reseller Sales Amount]  
  ,[Reseller Sales].[Reseller Tax Amount]  
  ,[Reseller Sales].[Reseller Standard Product Cost]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Datenbearbeitungsanweisungen &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
