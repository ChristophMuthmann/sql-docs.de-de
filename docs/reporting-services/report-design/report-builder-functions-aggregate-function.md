---
title: Aggregatfunktion (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 16ce643f-bbb3-40a5-ba78-7aed73156f3e
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 834118e295a58af22a0e0cdd3817af2f33cb023c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="report-builder-functions---aggregate-function"></a>Funktionen des Berichts-Generators: Aggregatfunktion
  Gibt ein benutzerdefiniertes Aggregat des angegebenen Ausdrucks gemäß der Definition durch den Datenanbieter zurück.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Aggregate(expression, scope)  
```  
  
#### <a name="parameters"></a>Parameter  
 *expression*  
 Der Ausdruck, für den die Aggregation auszuführen ist. Der Ausdruck muss aus einem einfachen Feldverweis bestehen.  
  
 *Bereich*  
 (**Zeichenfolge**) Der Name eines Datasets, einer Gruppe oder eines Datenbereichs mit den Berichtselementen, auf die die Aggregatfunktion anzuwenden ist. *Bereich* muss eine Zeichenfolgenkonstante sein und darf kein Ausdruck sein. Wenn *scope* nicht angegeben ist, wird der aktuelle Bereich verwendet.  
  
## <a name="return-type"></a>Rückgabetyp  
 Wird durch den Datenanbieter bestimmt. Die Funktion gibt **Nothing** zurück, wenn der Datenanbieter diese Funktion nicht unterstützt oder Daten nicht verfügbar sind.  
  
## <a name="remarks"></a>Hinweise  
 Die **Aggregate** -Funktion bietet die Möglichkeit, Aggregate zu verwenden, die auf der externen Datenquelle berechnet werden. Die Unterstützung dieser Funktion hängt von der Datenerweiterung ab. Beispielsweise ruft die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenverarbeitungserweiterung vereinfachte Rowsets von einer MDX-Abfrage ab. Einige Zeilen im Resultset können auf dem Datenquellenserver berechnete Aggregatwerte enthalten. Diese Werte werden als *Serveraggregate*bezeichnet. Zum Anzeigen von Serveraggregaten im grafischen Abfrage-Designer für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]klicken Sie in der Symbolleiste auf die Schaltfläche **Aggregat anzeigen** . Weitere Informationen finden Sie unter [Benutzeroberfläche des MDX-Abfrage-Designers für Analysis Services (Berichts-Generator)](http://msdn.microsoft.com/library/7e288eee-2d37-485e-a6a0-dbba5e041e26).  
  
 Beim Anzeigen der Kombination aus Aggregat- und Detaildatasetwerten in Detailzeilen eines Tablix-Datenbereichs werden Serveraggregate in der Regel nicht einbezogen, da es sich nicht um Detaildaten handelt. Sie können jedoch alle für das Dataset abgerufenen Werte anzeigen und die Art der Berechnung und Anzeige für die Aggregatdaten anpassen.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] erkennt die Verwendung der **Aggregat** -Funktion in Ausdrücken Ihres Berichts, um zu bestimmen, ob Serveraggregate in Detailzeilen angezeigt werden sollen. Wenn Sie **Aggregate** in einen Ausdruck eines Datenbereichs einbeziehen, können Serveraggregate nur in Ergebniszeilen für Gruppen oder Gesamtergebniszeilen, jedoch nicht in Detailzeilen erscheinen. Wenn Sie Serveraggregate in Detailzeilen anzeigen möchten, verwenden Sie die **Aggregate** -Funktion nicht.  
  
 Sie können dieses Standardverhalten ändern, indem Sie den Wert der Option **Teilergebnisse als Detailzeilen interpretieren** des Dialogfelds **Dataseteigenschaften** ändern. Wenn diese Option auf **True**festgelegt wird, werden alle Daten, einschließlich der Serveraggregate, als Detaildaten angezeigt. Ist die Option auf **False**festgelegt, werden Serveraggregate als Gesamtbeträge angezeigt. Die Einstellung für diese Eigenschaft beeinflusst alle Datenbereiche, die mit diesem Dataset verknüpft sind.  
  
> [!NOTE]  
>  Die Gruppenausdrücke aller Gruppen, die das Berichtselement enthalten, das auf **Aggregat** verweist, müssen aus einfachen Feldverweisen bestehen, z.B. `[FieldName]`. Sie können **Aggregate** in einem Datenbereich, der komplexe Gruppenausdrücke verwendet, nicht einsetzen. Für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenverarbeitungserweiterung muss Ihre Abfrage MDX-Felder des Typs **LevelProperty** (nicht **MemberProperty**) enthalten, um die Aggregation mit der **Aggregat**-Funktion zu unterstützen.  
  
 Das*Expression* -Objekt kann Aufrufe von geschachtelten Aggregatfunktionen enthalten. Dabei gelten folgende Ausnahmen und Bedingungen:  
  
-   Das*Scope* -Objekt für geschachtelte Aggregate muss dem Bereich des äußeren Aggregats entsprechen oder darin enthalten sein. In allen eindeutigen Bereichen des Ausdrucks muss ein Bereich eine untergeordnete Beziehung zu allen anderen Bereichen haben.  
  
-   Das*Scope* -Objekt für geschachtelte Aggregate darf nicht der Name eines Datasets sein.  
  
-   Das*Expression* -Objekt darf die Funktionen **First**, **Last**, **Previous**oder **RunningValue** nicht enthalten.  
  
-   Das*Expression* -Objekt darf keine geschachtelten Aggregate enthalten, die ein *recursive*-Objekt angeben.  
  
 Weitere Informationen finden Sie in der [Aggregatfunktionsreferenz (Berichts-Generator und SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) und unter [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Auflistungen (Berichts-Generator und SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Weitere Informationen zu rekursiven Aggregaten finden Sie unter [Creating Recursive Hierarchy Groups (Report Builder and SSRS) (Erstellen von rekursiven Hierarchiegruppen (Berichts-Generator und SSRS))](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="comparing-the-aggregate-and-sum-functions"></a>Vergleichen der Aggregate-Funktion und der Sum-Funktion  
 Die **Aggregate** -Funktion unterscheidet sich von numerischen Aggregatfunktionen wie **Sum** dadurch, dass die **Aggregate** -Funktion einen Wert zurückgibt, der vom Datenanbieter oder von der Datenverarbeitungserweiterung berechnet wird. Numerische Aggregatfunktionen wie **Sum** geben einen Wert zurück, der vom Berichtsprozessor für eine Gruppe von Daten in einem Dataset berechnet wird, das durch den *scope* -Parameter bestimmt wird. Weitere Informationen finden Sie in den im Thema [Aggregatfunktionsreferenz (Berichts-Generator und SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) aufgelisteten Aggregatfunktionen.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Codebeispiel wird ein Ausdruck veranschaulicht, der ein Serveraggregat für das Feld `LineTotal`abruft. Der Ausdruck wird einer Zelle in einer Zeile, die zur Gruppe `GroupbyOrder`gehört, hinzugefügt.  
  
```  
=Aggregate(Fields!LineTotal.Value, "GroupbyOrder")  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrucksverwendungen in Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Datentypen in Ausdrücken (Berichts-Generator und SSRS)](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
