---
title: Erstellen von SESSION CUBE-Anweisung (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_SESSION_CUBE
- SESSION
- CUBE
- SESSION CUBE
- CREATE SESSION CUBE
- CREATE SESSION
- CREATE
dev_langs:
- kbMDX
helpviewer_keywords:
- CREATE SESSION CUBE
- statements [MDX], CREATE SESSION CUBE
ms.assetid: 06b90f44-d943-4a52-b0d8-4bcbc57ed6ec
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 3f779c5fdc0cdc7d21ae9406a16de9917ad35fee
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---create-session-cube"></a>Datendefinition der MDX - SITZUNGSCUBE erstellen
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Erstellt einen Sitzungscube aus einem vorhandenen Servercube und füllt ihn auf. Der Sitzungscube ist nur innerhalb der aktuellen Sitzung sichtbar. Er kann nicht durchsucht oder aus einer anderen Sitzung abgefragt werden. Der Sitzungscube wird beim Beenden der Sitzung implizit gelöscht.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE SESSION CUBE session_cube_name FROM <cube list> (<param list>)  
  
<cube list>::= source_cube_name [,<cube list>]  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= <reg dim from clause>   
  
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
 session_cube_name  
 Der Name des Sitzungscubes.  
  
 source_cube_name  
 Der Name des Cubes, auf dem der Sitzungscube basiert.  
  
 source_cube_name.measure_name  
 Der vollqualifizierte Name des Quellmeasures, das in den Sitzungscube eingeschlossen wird. Berechnete Elemente der Measures-Dimension sind nicht zulässig.  
  
 measure_name  
 Der Name des Measures im Sitzungscube.  
  
 source_cube_name.dimension_name  
 Der vollqualifizierte Name der Quelldimension, die in den Sitzungscube eingeschlossen wird.  
  
 dimension_name  
 Der Name der Dimension im Sitzungscube.  
  
 AUS \<dim from-Klausel >  
 Nur für die abgeleitete Dimensionsdefinition gültige Angabe.  
  
 NOT_RELATED_TO_FACTS  
 Nur für die abgeleitete Dimensionsdefinition gültige Angabe.  
  
 \<Typ der Ebene >  
 Nur für die abgeleitete Dimensionsdefinition gültige Angabe.  
  
## <a name="remarks"></a>Hinweise  
 Im Gegensatz zu einem Servercube und einem lokalen Cube wird ein Sitzungscube nur für die Sitzung persistent gespeichert, in der der Sitzungscube erstellt wurde. Ein Sitzungscube wird anhand der Measures und Definitionen definiert, durch die er definiert wird. Es gibt zwei Typen von Dimensionen.  
  
-   Quelldimensionen – Hierbei handelt es sich um Dimensionen, die Teil eines oder mehrerer Quellcubes waren.  
  
-   Abgeleitete Dimensionen – Hierbei handelt es sich um Dimensionen, die neue Analysefunktionen bereitstellen. Bei einer abgeleiteten Dimension kann es sich um eine reguläre Dimension handeln, die basierend auf einer Quelldimension definiert wird, die entweder vertikal oder horizontal in Slices aufgeteilt ist oder die eine benutzerdefinierte Gruppierung von Dimensionselementen enthält. Eine abgeleitete Dimension kann auch eine Data Mining-Dimension sein, die auf einem Data Mining-Modell basiert.  
  
> [!NOTE]  
>  Das Dimension-Schlüsselwort kann entweder auf Dimensionen oder Hierarchien verweisen.  
  
 Sitzungscubes werden hauptsächlich für die dynamische Gruppierung der Attributelemente in benutzerdefinierte Elementgruppen durch Clientanwendungen verwendet, beispielsweise Microsoft Excel. In einem Sitzungscube können Sie folgende Aufgaben ausführen:  
  
-   Im Sitzungscube vorhandene Dimensionen entfernen  
  
-   Hinzufügen oder Entfernen von Hierarchien aus einer Dimension.  
  
-   Measuregruppen oder bestimmte Measures entfernen  
  
-   Ein neues Attribut basierend auf Attributbindung hinzufügen, um neue Gruppen für ein vorhandenes Attribut zu erstellen  
  
> [!IMPORTANT]  
>  Die Sicherheit in Sitzungscubeobjekten wird von zugrunde liegenden Quellobjekten geerbt. Andere Objekte, beispielsweise Aktionen und Berechnungsskripts, werden auch vom Sitzungscube geerbt.  
  
 Für die CREATE SESSION CUBE-Anweisung gelten diese Regeln:  
  
-   Sie können keine Gruppierung der Über-/Unterordnungshierarchien ausführen.  
  
-   Sie können keine Gruppierung der ROLAP-Dimensionen ausführen.  
  
-   Sie können keine Gruppierung der verlinkten Dimensionen ausführen.  
  
-   Sie können keine Gruppierung der Ebenen mit benutzerdefinierten Rollups ausführen.  
  
-   Sie können keine Gruppierung der diskretisierten Attributhierarchien ausführen.  
  
-   Sie können keine Gruppierung der unnatürlichen Hierarchien ausführen, bei denen es sich um Hierarchien mit m:n-Beziehungen zwischen Ebenen handelt (beispielsweise Alter und Geschlecht).  
  
-   Explizite Verweise auf einen Cubenamen im MDX-Skript werden durch die Gruppierung unterbrochen, da der Sitzungscube einen anderen Namen aufweist. Verwenden Sie stattdessen das CURRENTCUBE-Schlüsselwort.  
  
-   Sie können keine Gruppierung der Dimensionen mit expliziten Standardelementen ausführen.  
  
-   Beim Ausführen der Gruppierung werden im Bereich einer Sitzung berechnete Elemente des ursprünglichen Servercubes gelöscht.  
  
-   Beim Ausführen der Gruppierung einer Cubedimension in einem Servercube wirkt sich die Gruppierung auf alle Cubedimensionen aus, die auf derselben Dimension basieren.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie eine Version des Adventure Works-Cubes im Sitzungsbereich erstellt wird, die das Reseller Sales Amount-Measure, die Reseller-Dimension, die Product-Dimension, die Geography-Dimension und die Date-Dimension enthält. In diesem Sitzungscube werden zwei Gruppen erstellt. Eine Gruppe enthält Länder in Europa, und eine Gruppe enthält Gruppen in Nordamerika. Dieses Beispiel stellt eine vereinfachte Version der CREATE SESSION CUBE-Anweisung dar, die von Microsoft Excel ausgegeben wird, wenn ein Benutzer eine benutzerdefinierte Gruppierung von Elementen erstellt.  
  
```  
CREATE SESSION CUBE [Adventure Works_XL_GROUPING1]   
   FROM [Adventure Works]   
   ( MEASURE [Adventure Works].[Internet Sales Amount]  
   ,MEASURE [Adventure Works].[Reseller Sales Amount]  
   ,DIMENSION [Adventure Works].[Date].[Calendar]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Year]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Semester]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Quarter]  
   ,DIMENSION [Adventure Works].[Date].[Month Name]  
   ,DIMENSION [Adventure Works].[Date].[Date]  
   ,DIMENSION [Adventure Works].[Geography].[Country]   
      HIDDEN AS _XL_GROUPING81  
   ,DIMENSION [Adventure Works].[Geography].[State-Province]  
   ,DIMENSION [Adventure Works].[Geography].[City]  
   ,DIMENSION [Adventure Works].[Geography].[Postal Code]  
   ,DIMENSION [Adventure Works].[Geography].[Geography]  
   ,DIMENSION [Adventure Works].[Product].[Product Categories]  
   ,DIMENSION [Adventure Works].[Product].[Category]  
   ,DIMENSION [Adventure Works].[Product].[Subcategory]  
   ,DIMENSION [Adventure Works].[Product].[Product]  
   ,DIMENSION [Adventure Works].[Product].[Product Key]  
   ,DIMENSION [Adventure Works].[Reseller].[Reseller]  
   ,DIMENSION [Adventure Works].[Reseller].[Geography Key]  
   ,DIMENSION [Geography].[Country]   
      NOT_RELATED_TO_FACTS FROM _XL_GROUPING81   
          ( LEVEL [(All)]  
         ,LEVEL [Country1] GROUPING  
         ,LEVEL [Country]  
            ,GROUP [Country1].[CountryXl_Grp_1]   
                ( MEMBER [Geography].[Country].&[Canada]  
                  ,MEMBER [Geography].[Country].&[United States] )  
            ,GROUP [Country1].[CountryXl_Grp_2]   
                ( MEMBER [Geography].[Country].&[France]  
                  ,MEMBER [Geography].[Country].&[Germany]  
                  ,MEMBER [Geography].[Country].&[United Kingdom] )   
            )   
   )  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Datendefinitionsanweisungen &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)   
 [CREATE GLOBAL CUBE-Anweisung &#40;MDX&#41;](../mdx/mdx-data-definition-create-global-cube.md)  
  
  
