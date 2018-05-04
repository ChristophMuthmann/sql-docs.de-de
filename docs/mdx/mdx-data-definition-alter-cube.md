---
title: ALTER CUBE-Anweisung (MDX) | Microsoft Docs
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
- Cube
- ALTER_CUBE
- ALTER CUBE
- ALTER
dev_langs:
- kbMDX
helpviewer_keywords:
- ALTER CUBE statement
- cubes [Analysis Services], modifying
- modifying cubes
ms.assetid: 2f0af61b-f509-4e1a-990f-20a215d22994
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 6a91092f5a62f1c21312ca585834795d678216ae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---alter-cube"></a>MDX - Datendefinition: ALTER CUBE
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ändert die Struktur eines angegebenen Cubes, der normalerweise verwendet wird, um das Rückschreiben von Dimensionen zu unterstützen. Weitere Informationen zur Verwendung des Rückschreibens in einer Anwendung finden Sie in diesem Blogbeitrag: [Erstellen einer Rückschreibeanwendung mit Analysis Services (Blog)](http://go.microsoft.com/fwlink/?LinkId=394977)  
  
 Gleichzeitige Rückschreibevorgänge für Dimensionen können zu einem Deadlock führen. Dabei wird die erste Rückschreibung aufgrund der durch die zweite Rückschreibung aufrechterhaltene gemeinsame Sperre für ein Commit blockiert. In diesem Fall wird zwar kein Fehler generiert, allerdings kann keiner der Vorgänge fortgesetzt werden. Schließlich tritt für beide Rückschreibevorgänge ein Timeout auf, und es wird ein Rollback der Änderungen ausgeführt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER CUBE  
      Cube_Name | CURRENTCUBE  
      <alter clause>   
            [ < alter clause> ...n]  
  
< alter clause> ::=   
   <create dimension member clause>   
  | <remove dimension member clause>  
  | <move dimension member clause>   
    | <update clause>   
    | <create cell calculation clause>  
  
<create dimension member clause> ::=  
CREATE DIMENSION MEMBER [ParentName.]MemberName  
    , [[KEY = Key_Value]   
    | [Property_Name = Property_Value[, ...n]]  
  
<dropping clause>::=  
DROP   
      DIMENSION MEMBER Member_Name   
            Member_Name ...n ]   
      [WITH DESCENDANTS]  
      | [ SESSION ] [ CALCULATED ] MEMBER Member_Name   
                  [ ,Member_Name,...n ]   
    | SET Set_Name  
                  [ ,Set_Name,...n ]   
    | [ SESSION ] CELL CALCULATION CellCalc_Name  
                  [ ,CellCalc_Name,...n ]   
    | ACTION Action_Name  
  
<move dimension member clause> ::=  
MOVE DIMENSION MEMBER MemberName  
        [, SKIPPED_LEVELS = Unsigned_Integer]   
      [WITH DESCENDANTS]  
    UNDER ParentName      
  
<update clause> ::=  
UPDATE   
    CUSTOM ROLLUP FOR MEMBER MemberName  
      [,MemberName, ...n] AS MDX_Expression  
   | DIMENSION Dimension_Name | Hierarchy_Name  
      , DEFAULT_MEMBER = MDX_Expression  
   | DIMENSION MEMBER MemberName AS  
   [MDX_Expression]  
   [Property_Name = Property_Value[, ...n]]  
  
<create cell calculation clause>::=  
CELL CALCULATION Calculation_Name   
   FOR Set_Expression AS MDX_Expression   
            [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="creating-a-dimension-member"></a>Erstellen eines Dimensionselements  
 Der zugrunde liegenden Dimensionstabelle wird eine neue Zeile hinzugefügt.  
  
### <a name="arguments"></a>Argumente  
 *ParentName*  
 Ein gültiger Zeichenfolgenausdruck, der, sofern das neue Dimensionselement nicht auf der Stammebene erstellt wird, den Namen des ihm übergeordneten Elements bereitstellt.  
  
 *MemberName*  
 Ein gültiger Zeichenfolgenausdruck, der einen Elementnamen bereitstellt.  
  
 *Key_Value*  
 Ein gültiger Skalarausdruck, der den Schlüsselwert des neuen Dimensionselements definiert.  
  
 *Eigenschaftsname*  
 Ein gültiger MDX-Bezeichner (Multidimensional Expressions), der eine Elementeigenschaft darstellt.  
  
 *Property_Value*  
 Ein gültiger MDX-Skalarausdruck (Multidimensional Expressions), der den Wert der Eigenschaft eines berechneten Elements definiert.  
  
## <a name="dropping-a-dimension-member"></a>Löschen eines Dimensionselements  
 Beim Löschen eines Dimensionselements aus einer Dimension mit aktiviertem Schreibzugriff wird das Element sowie die dazugehörige Zeile in der zugrunde liegenden Dimensionstabelle gelöscht.  
  
### <a name="arguments"></a>Argumente  
 *Cube_Name*  
 Ein gültiger Zeichenfolgenausdruck, der einen Cubenamen bereitstellt.  
  
 *Member_Name*  
 Ein gültiger Zeichenfolgenausdruck, der einen Elementnamen oder Elementschlüssel bereitstellt.  
  
### <a name="remarks"></a>Hinweise  
 Wenn die WITH DESCENDANTS-Klausel nicht verwendet wird, werden aus den untergeordneten Elementen eines gelöschten Elements untergeordnete Elemente des diesem übergeordneten Elements. Wenn die WITH DESCENDANTS-Klausel verwendet wird, werden alle nachfolgenden Werte einschließlich ihrer Zeilen in der Dimensionstabelle ebenfalls gelöscht.  
  
> [!NOTE]  
>  Informationen zum Löschen von berechneten Elementen, benannten Mengen, Aktionen und zellenberechnungen finden Sie unter [DROP MEMBER-Anweisung &#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md), [SET-Anweisung DROP &#40;MDX&#41;](../mdx/mdx-data-definition-drop-set.md), [DROP ACTION-Anweisung &#40;MDX&#41;](../mdx/mdx-data-definition-drop-action.md), und [DROP CELL CALCULATION-Anweisung &#40;MDX&#41;](../mdx/mdx-data-definition-drop-cell-calculation.md).  
  
## <a name="updating-the-default-dimension-member"></a>Aktualisieren des Standardelements einer Dimension  
 Diese Klausel aktualisiert das Standardelement eines Cubes und wird im MDX-Berechnungsskript zum Definieren eines Standardelements verwendet. Das Standardelement kann für die Datenbankdimension, eine Cubedimension oder einen Anmeldenamen angegeben werden. Das Standardelement kann auch während einer Sitzung geändert werden.  
  
### <a name="arguments"></a>Argumente  
 *Dimension_Name*  
 Eine gültige Zeichenfolge, die den Namen einer Dimension bereitstellt.  
  
 *MDX_Expression*  
 Ein gültiger MDX-Ausdruck, der ein einzelnes Element zurückgibt.  
  
### <a name="remarks"></a>Hinweise  
 Der angegebene MDX-Ausdruck kann statisch oder dynamisch sein.  
  
## <a name="moving-a-dimension-member"></a>Verschieben eines Dimensionselements  
 In der zugrunde liegenden Dimensionstabelle wird eine Zeile geändert.  
  
### <a name="arguments"></a>Argumente  
 *ParentName*  
 Ein gültiger Zeichenfolgenausdruck, der den Namen des neuen übergeordneten Elements des zu verschiebenden Dimensionselements bereitstellt.  
  
 *MemberName*  
 Ein gültiger Zeichenfolgenausdruck, der einen Elementnamen bereitstellt.  
  
 Unsigned_*ganze Zahl*  
 Eine gültige Zahl, die die Anzahl der auszulassenden Ebenen angibt.  
  
 Wenn die WITH DESCENDANTS-Klausel angegeben ist, wird die gesamte Struktur verschoben. Wenn die WITH DESCENDANTS-Klausel nicht angegeben ist, werden aus den untergeordneten Elementen des verschobenen übergeordneten Elements untergeordnete Elemente des dem verschobenen Element übergeordneten Elements. Die Verschiebung wirkt sich einfach dahin gehend aus, dass die Werte der übergeordneten Schlüsselspalte in der zugrunde liegenden Dimensionstabelle aktualisiert werden.  
  
## <a name="updating-a-dimension-member"></a>Aktualisieren eines Dimensionselements  
 Mit der UPDATE DIMENSION MEMBER-Klausel können Sie Eigenschaften eines Elements sowie die einem Element zugeordnete benutzerdefinierte Elementformel ändern.  
  
### <a name="arguments"></a>Argumente  
 *MemberName*  
 Ein gültiger Zeichenfolgenausdruck, der einen Elementnamen bereitstellt.  
  
 *MDX_Expression*  
 Ein gültiger MDX-Ausdruck, der ein einzelnes Element zurückgibt.  
  
 *Property_Value*  
 Ein gültiger MDX-Skalarausdruck, der den Wert der Eigenschaft eines berechneten Elements definiert.  
  
## <a name="creating-a-cell-calculation"></a>Erstellen einer Zellenberechnung  
 Weitere Informationen zum Erstellen einer Zellenberechnung mithilfe der ALTER CUBE-Anweisung finden Sie unter [DROP CELL CALCULATION-Anweisung &#40;MDX&#41;](../mdx/mdx-data-definition-drop-cell-calculation.md).  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Datendefinitionsanweisungen &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
