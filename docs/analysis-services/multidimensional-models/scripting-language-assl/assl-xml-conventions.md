---
title: ASSL XML-Konventionen | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- whitespace [Analysis Services Scripting Language]
- trailing whitespace
- XSD data types [Analysis Services Scripting Language]
- inheritance [Analysis Services Scripting Language]
- cardinality [Analysis Services Scripting Language]
- white space [Analysis Services Scripting Language]
- ASSL, XML conventions
- defaults [Analysis Services Scripting Language]
- leading whitespace
- Analysis Services Scripting Language, XML conventions
- XML [Analysis Services Scripting Language]
- hierarchies [Analysis Services Scripting Language]
- inherited defaults [Analysis Services Scripting Language]
ms.assetid: bce4edad-4420-41ce-9672-8c00c5c0dec6
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a8cd244f64d45ff81ff51cba6b528c81ba743ff1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="assl-xml-conventions"></a>XML-Konventionen in ASSL
  Die Analysis Services Scripting Language (ASSL) stellt die Hierarchie von Objekten als Satz von Elementtypen dar, die jeweils die untergeordneten Elemente definieren, die sie enthalten können.  
  
 Für die Darstellung der Objekthierarchie verwendet ASSL folgende XML-Konventionen:  
  
-   Alle Objekte und Eigenschaften werden als Elemente dargestellt, mit Ausnahme von XML-Standardattributen wie „xml:lang“.  
  
-   Sowohl Elementnamen als auch Enumerationswerte befolgen die Microsoft .NET Framework-Benennungskonvention der Schreibweise von Pascal ohne Unterstriche.  
  
-   Die Groß-/Kleinschreibung aller Werte wird beibehalten. Bei Werten für Enumerationen wird ebenfalls die Groß-/Kleinschreibung unterschieden.  
  
 Zusätzlich zu dieser Konventionsliste werden in Analysis Services bestimmte Konventionen in Bezug auf Kardinalität, Vererbung, Leerzeichen, Datentypen und Standardwerte befolgt.  
  
## <a name="cardinality"></a>Kardinalität  
 Wenn ein Element eine Kardinalität besitzt, die größer als 1 ist, wird dieses Element von einer XML-Elementauflistung gekapselt. Der Name der Auflistung verwendet die Pluralform der in der Auflistung enthaltenen Elemente. Das folgenden XML-Fragment stellt beispielsweise die **Dimensions** -Auflistung innerhalb eines **Database** -Elements dar:  
  
 `<Database>`  
  
 `…`  
  
 `<Dimensions>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `</Dimensions>`  
  
 `</Database>`  
  
 ``  
  
 Die Reihenfolge der Elemente ist bedeutungslos.  
  
## <a name="inheritance"></a>Vererbung  
 Die Vererbung wird bei unterschiedlichen Objekten verwendet, die über überlappende, jedoch deutlich unterschiedliche Sätze von Eigenschaften verfügen. Beispiele für derartige überlappende, jedoch unterschiedliche Objekte sind virtuelle Cubes, verknüpfte Cubes und reguläre Cubes. Für überlappende, jedoch unterschiedliche Objekte wird in Analysis Services das **type** -Standardattribut aus dem XML-Instanzennamespace verwendet, um die Vererbung anzugeben. Das folgende XML-Fragment zeigt, wie das **type** -Attribut ermittelt, ob ein **Cube** -Element von einem regulären Cube oder von einem virtuellen Cube erbt:  
  
 `<Cubes>`  
  
 `<Cube xsi:type=”RegularCube”>`  
  
 `<Name>Sales</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `<Cube xsi:type=”VirtualCube”>`  
  
 `<Name>SalesAndInventory</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `</Cubes>`  
  
 ``  
  
 Die Vererbung wird im Allgemeinen nicht verwendet, wenn mehrere Typen eine Eigenschaft mit dem gleichen Namen besitzen. Die **Name** - und die **ID** -Eigenschaft sind beispielsweise auf zahlreichen Elementen vorhanden, diese Eigenschaften wurden jedoch nicht zu einem abstrakten Typ heraufgestuft.  
  
## <a name="whitespace"></a>Leerzeichen  
 Leerzeichen innerhalb eines Elementwerts werden beibehalten. Führende und nachfolgende Leerzeichen werden jedoch immer entfernt. Die folgenden Elemente besitzen beispielsweise den gleichen Text, jedoch eine unterschiedliche Anzahl von Leerzeichen innerhalb dieses Texts, daher werden sie behandelt, als besäßen sie unterschiedliche Werte:  
  
 `<Description>My text<Description>`  
  
 `<Description>My  text<Description>`  
  
 ``  
  
 Die folgenden Elemente unterscheiden sich jedoch nur durch führende und nachfolgende Leerzeichen, daher werden sie behandelt, als besäßen sie die gleichen Werte.  
  
 `<Description>My text<Description>`  
  
 `<Description>  My text  <Description>`  
  
 ``  
  
## <a name="data-types"></a>Datentypen  
 In Analysis Services werden die folgenden XSD-Standarddatentypen (XML Schema Definition Language) verwendet:  
  
 **Int**  
 Ein ganzzahliger Wert im Bereich von -231 bis 231 – 1.  
  
 **Long**  
 Ein ganzzahliger Wert im Bereich von -263 bis 263 – 1.  
  
 **String**  
 Ein Zeichenfolgenwert, der den folgenden allgemeinen Regeln entspricht:  
  
-   Steuerzeichen werden entfernt.  
  
-   Führende und nachfolgende Leerzeichen werden entfernt.  
  
-   Interne Leerzeichen werden beibehalten.  
  
 Die**Name** - und die **ID** -Eigenschaft besitzen spezielle Beschränkungen für gültige Zeichen in Zeichenfolgenelementen. Weitere Informationen zu **Namen** und **ID** Konventionen, finden Sie unter [ASSL-Objekte und-Objekteigenschaften](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
 **DateTime**  
 Eine **DateTime** -Struktur aus dem .NET Framework. Ein **DateTime** -Wert darf nicht NULL sein. Das früheste von dem **DataTime** -Datentyp unterstützte Datum ist der 1. Januar 1601, das für Programmierer als **DateTime.MinValue**zur Verfügung steht. Das früheste unterstützte Datum gibt an, dass ein **DateTime** -Wert fehlt.  
  
 **Boolean**  
 Eine Enumeration mit nur zwei Werten wie {true, false} oder {0, 1}.  
  
## <a name="default-values"></a>Standardwerte  
 Analysis Services verwendet die in der folgenden Tabelle aufgelisteten Standardwerte:  
  
|XML-Datentyp|Standardwert|  
|-------------------|-------------------|  
|**Boolean**|False|  
|**String**|"" (leere Zeichenfolge)|  
|**Integer** oder **Long**|0 (Null)|  
|**Zeitstempel**|12:00:00 AM, 1/1/0001 (entsprechend den .NET Frameworks- **System.DateTime** mit 0 Takten)|  
  
 Eine Element, das vorhanden, jedoch leer ist, wird interpretiert, als hätte es den Wert einer NULL-Zeichenfolge, nicht den Standardwert.  
  
### <a name="inherited-defaults"></a>Geerbte Standards  
 Einige auf einem Objekt angegebene Eigenschaften stellen Standardwerte für die gleiche Eigenschaft auf untergeordneten oder nachfolgenden Objekten bereit. Beispielsweise stellt **Cube.StorageMode** den Standardwert für **Partition.StorageMode**bereit. Folgende Regeln werden von Analysis Services auf geerbte Standardwerte angewendet:  
  
-   Wenn die Eigenschaft für das untergeordnete Objekt in XML NULL ist, nimmt ihr Wert standardmäßig den geerbten Wert an. Wenn Sie den Wert jedoch vom Server abfragen, gibt der Server den NULL-Wert des XML-Elements zurück.  
  
-   Es ist nicht möglich, programmgesteuert festzustellen, ob die Eigenschaft eines untergeordneten Objekts direkt auf dem untergeordneten Objekt festgelegt oder geerbt wurde.  
  
 Einige Elemente besitzen definierte Standards, die gelten, wenn das Element fehlt. Beispielsweise entsprechen sich die **Dimension** -Elemente in den folgenden XML-Fragmenten, obwohl ein **Dimension** -Element ein **Visible** -Element enthält, das andere **Dimension** -Element jedoch nicht.  
  
 `<Dimension>`  
  
 `<Name>Product</Name>`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `<Name>Product</ Name>`  
  
 `<Visible>true</Visible>`  
  
 `</Dimension>`  
  
 Weitere Informationen zu geerbten Standards finden Sie unter [ASSL-Objekte und-Objekteigenschaften](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
  

