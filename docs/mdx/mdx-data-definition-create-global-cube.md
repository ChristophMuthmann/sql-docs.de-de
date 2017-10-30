---
title: Erstellen Sie GLOBAL CUBE-Anweisung (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GLOBAL CUBE
- CUBE
- GLOBAL
- CREATE
- CREATE GLOBAL
- CREATE GLOBAL CUBE
dev_langs:
- kbMDX
helpviewer_keywords:
- statements [MDX], CREATE GLOBAL CUBE
- CREATE GLOBAL CUBE
ms.assetid: b46f3c98-a4f1-4ebb-915f-a3333f4054dc
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b9a80a053d9666ca2e8c63eb6037dddf3cf4a7a5
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---create-global-cube"></a>MDX-Datendefinition - globalen CUBE erstellen
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt einen lokal persistenten Cube, der auf einem Teilcube aus einem Cube auf dem Server basiert, und füllt ihn auf. Für die Verbindung mit dem lokal persistenten Cube ist keine Verbindung mit dem Server erforderlich. Weitere Informationen zu lokalen Cubes finden Sie unter [lokale Cubes &#40; Analysis Services – mehrdimensionale Daten &#41; ](../analysis-services/multidimensional-models/olap-physical/local-cubes-analysis-services-multidimensional-data.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE GLOBAL CUBE local_cube_name STORAGE 'Cube_Location'   
FROM source_cube_name (<param list>)  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= < dim DM from clause> | <reg dim from clause>   
  
<dim DM from clause>::= dm_model_name> COLUMN column_name   
  
<dim reg from clause>::= dimension_name  
  
<dim content def>::= ( <level list> [,<grouping list>] [,<member slice list>] [,<default member>] )  
  
<level list>::= <level def> [, <level list>]  
  
<level def>::= LEVEL level_name [<level type> ] [AS level_name] [<level content def>]  
  
<level content def>::= ( <property list> ) | NO_PROPERTIES  
  
<level type>::= GROUPING  
  
<property list>::= <property def> [, <property list>]  
  
<property def>::= PROPERTY property_name   
  
<grouping list>::= <grouping entity> [,<grouping list>]  
  
<grouping entity>::= GROUP group_level_name.group_name (<mixed list>)  
  
<grp mixed list>::= <grp mixed element> [,<grp mixed list>]  
  
<grp mixed element>::= <grouping entity> | <member def>  
  
<member slice list>::= <member list>  
  
<member list>::= <member def> [, <member list>]  
  
<member def>::= MEMBER member_name  
  
<default member>::= DEFAULT_MEMBER AS MDX_expression  
  
<visibility qualifier>::= HIDDEN   
```  
  
## <a name="syntax-elements"></a>Syntaxelemente  
 local_cube_name  
 Der Name des lokalen Cubes.  
  
 'Cube_Location'  
 Der Name und der Pfad für den lokal persistenten Cube.  
  
 source_cube_name  
 Der Name des Cubes, auf dem der lokale Cube basiert.  
  
 source_cube_name.measure_name  
 Der vollqualifizierte Name des Quellmeasures, das in den lokalen Cube eingeschlossen wird. Berechnete Elemente der Measures-Dimension sind nicht zulässig.  
  
 measure_name  
 Der Name des Measures im lokalen Cube.  
  
 source_cube_name.dimension_name  
 Der vollqualifizierte Name der Quelldimension, die in den lokalen Cube eingeschlossen wird.  
  
 dimension_name  
 Der Name der Dimension im lokalen Cube.  
  
 AUS \<dim from-Klausel >  
 Nur für die abgeleitete Dimensionsdefinition gültige Angabe.  
  
 NOT_RELATED_TO_FACTS  
 Nur für die abgeleitete Dimensionsdefinition gültige Angabe.  
  
 \<Typ der Ebene >  
 Nur für die abgeleitete Dimensionsdefinition gültige Angabe.  
  
## <a name="remarks"></a>Hinweise  
 Eine lokale Cubedatei ist eigene Begriffe der Measures und Definitionen, die ihn definieren. Es gibt zwei Typen von Dimensionen.  
  
-   Quelldimensionen – sind diese Dimensionen, die Teil eines oder mehrerer Quellcubes waren.  
  
-   Abgeleitete Dimensionen – Hierbei handelt es sich um Dimensionen, die neue Analysefunktionen bereitstellen. Bei einer abgeleiteten Dimension kann es sich um eine reguläre Dimension handeln, die basierend auf einer Quelldimension definiert wird, die entweder vertikal oder horizontal in Slices aufgeteilt ist oder die eine benutzerdefinierte Gruppierung von Dimensionselementen enthält. Eine abgeleitete Dimension kann auch eine Data Mining-Dimension sein, die auf einem Data Mining-Modell basiert.  
  
> [!NOTE]  
>  Das Dimension-Schlüsselwort kann entweder auf Dimensionen oder Hierarchien verweisen.  
  
 In einem lokalen Cube können Sie folgende Aufgaben ausführen:  
  
-   Entfernen von Dimensionen, die im Quellcube vorhanden sind.  
  
-   Hierarchien aus einer Dimension hinzufügen oder entfernen  
  
-   Measuregruppen oder bestimmte Measures entfernen  
  
 Die CREATE GLOBAL CUBE-Anweisung hält die folgenden Regeln ein:  
  
-   Mit der CREATE GLOBAL CUBE-Anweisung werden automatisch alle Befehle, z. B. berechnete Measures oder Aktionen, in den lokalen Cube kopiert. Enthält ein Befehl einen MDX-Ausdruck (Multidimensional Expression), der explizit auf den übergeordneten Cube verweist, kann dieser Befehl nicht vom lokalen Cube ausgeführt werden. Verwenden Sie zur Vermeidung dieses Problems die **CURRENTCUBE** Schlüsselwort der MDX-Ausdrücken für Befehle zu definieren. Die **CURRENTCUBE** -Schlüsselwort verwendet den aktuellen Cubekontext aus, wenn Sie einen Cube innerhalb eines MDX-Ausdrucks zu verweisen.  
  
-   Ein globaler Cube, der aus einem vorhandenen globalen Cube in einer lokalen Cubedatei erstellt wurde, kann nicht in derselben lokalen Cubedatei gespeichert werden. Angenommen, Sie erstellen einen globalen Cube mit dem Namen SalesLocal1 und speichern ihn in der Datei C:\SalesLocal.cub. Sie können dann eine Verbindung zur Datei C:\SalesLocal.cub herstellen und einen zweiten globalen Cube mit dem Namen SalesLocal2 erstellen. Wenn Sie nun versuchen, den globalen Cube SalesLocal2 in der Datei C:\SalesLocal.cub zu speichern, erhalten Sie eine Fehlermeldung. Sie können den globalen Cube SalesLocal2 allerdings in einer anderen lokalen Cubedatei speichern.  
  
-   Globale Cubes unterstützen keine Distinct Count Measures. Da Cubes mit Distinct Count Measures nicht additiv sind, werden von der CREATE GLOBAL CUBE-Anweisung weder das Erstellen noch das Verwenden von Distinct Count Measures unterstützt.  
  
-   Wenn einem lokalen Cube ein Measure hinzugefügt wird, müssen Sie auch mindestens eine Dimension verwenden, die mit dem hinzugefügten Measure in Zusammenhang steht.  
  
-   Wenn einem lokalen Cube eine Über-/Unterordnungshierarchie hinzugefügt wird, werden die Ebenen und Filter einer Über-/Unterordnungshierarchie ignoriert, und die gesamte Über-/Unterordnungshierarchie wird eingeschlossen.  
  
-   Elementeigenschaften werden in lokalen Cubes nicht unterstützt.  
  
-   Das Erstellen eines lokalen Cubes ist mit einer Perspektive nicht möglich.  
  
-   Wenn Sie ein semiadditives Measure in einen lokalen Cube einschließen, gelten die folgenden Regeln:  
  
    -   Sie müssen die Account-Dimension verwenden, wenn die AggregateFunction-Eigenschaft für das hinzugefügte Measure ByAccount lautet.  
  
    -   Sie müssen die gesamte Time-Dimension einschließen, wenn das hinzugefügte Measure der AggregateFunction-Eigenschaft FirstChild, LastChild, FirstNonEmpty, LastNonEmpty oder AverageOfChildren lautet.  
  
-   Data Mining-Dimensionen können einem lokalen Cube nicht hinzugefügt werden.  
  
-   Bezugsdimensionen werden materialisiert und als reguläre Dimensionen hinzugefügt.  
  
-   Wenn Sie eine m:n-Dimension einschließen, gelten die folgenden Regeln:  
  
    -   Sie müssen die gesamte m:n-Dimension hinzufügen.  
  
    -   Sie müssen die Zwischenmeasuregruppe hinzufügen.  
  
    -   Sie müssen die Gesamtheit aller Dimensionen hinzufügen, die für die zwei an der m:n-Beziehung beteiligten Measuregruppen gelten.  
  
 Im folgenden Beispiel wird gezeigt, wie eine lokale persistente Version des Adventure Works-Cubes erstellt wird, die lediglich das Reseller Sales Amount-Measure, die Reseller-Dimension und die Date-Dimension enthält.  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller1.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
   )  
```  
  
 Im folgenden Beispiel wird das Aufteilen in Slices beim Erstellen eines lokalen Cubes veranschaulicht. Der erstellte globale Cube basiert auf dem Adventure Works-Cube, der anhand des 2005-Elements der Fiscal Year-Ebene in vertikale und anhand der Ebenen Fiscal Year und Month in horizontale Slices aufgeteilt wurde.  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller2.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
      (  
LEVEL [Fiscal Year],  
LEVEL [Month],  
MEMBER [Date].[Fiscal].[Fiscal Year].&[2005]  
      )  
   )  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Datendefinitionsanweisungen &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)   
 [Erstellen Sie SESSION CUBE-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-create-session-cube.md)  
  
  

