---
title: Aktionen in mehrdimensionalen Modellen | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 03d7e3fd90aeb130988eb79d1c9849043f5d56f1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="actions-in-multidimensional-models"></a>Aktionen in mehrdimensionalen Modellen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Eine Aktion ist ein vom Endbenutzer initiierter Vorgang, der auf einem ausgewählten Cube oder Teil eines Cubes ausgeführt wird. Der Vorgang kann eine Anwendung mit dem ausgewählten Element als Parameter starten, oder er kann Informationen zum ausgewählten Element abrufen. Weitere Informationen zu Aktionstypen finden Sie unter [Aktionen &#40;Analysis Services – Mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
 Mithilfe der Registerkarte **Aktionen** des Cube-Designers können Sie Aktionen für einen Cube erstellen. Geben Sie Folgendes an:  
  
 **Name**  
 Wählen Sie einen Namen für die Aktion aus.  
  
 **Aktionsziel**  
 Wählen Sie das Objekt aus, dem die Aktion angefügt wird. In Clientanwendungen wird die Aktion grundsätzlich angezeigt, wenn der Endbenutzer das Zielobjekt ausgewählt hat; jedoch bestimmt die Clientanwendung, welcher Endbenutzervorgang Aktionen anzeigt. Wählen Sie für **Zieltyp**aus den folgenden Objekten aus:  
  
-   Attributelemente  
  
-   Zellen  
  
-   Cube  
  
-   Dimensionselemente  
  
-   Hierarchy  
  
-   Hierarchieelemente  
  
-   Ebene  
  
-   Ebenenelemente  
  
 Nachdem Sie den Zielobjekttyp ausgewählt haben, wählen Sie unter **Zielobjekt**das Cubeobjekt vom entsprechenden Typ aus.  
  
 **Bedingung (Optional)**  
 Geben Sie einen optionalen MDX-Ausdruck (Multidimensional Expressions) an, der zu einem Booleschen Wert aufgelöst wird. Beim Wert **True**wird die Aktion für das angegebene Ziel durchgeführt. Beim Wert **False**wird die Aktion nicht durchgeführt.  
  
 **Aktionsinhalt**  
 Wählen Sie den Typ der Aktion aus. In der folgenden Tabelle werden die verfügbaren Aktionstypen zusammengefasst.  
  
|Typ|Description|  
|----------|-----------------|  
|Dataset|Ruft ein Dataset ab.|  
|Proprietär|Führt einen Vorgang über eine Schnittstelle aus, die nicht in dieser Tabelle aufgelistet ist.|  
|Rowset|Ruft ein Rowset ab.|  
|Statement|Gibt einen OLE DB-Befehl zurück.|  
|URL|Zeigt eine veränderliche Seite in einem Internetbrowser an.|  
  
 Geben Sie für **Aktionsausdruck**die Parameter an, die beim Ausführen der Aktion übergeben werden. Die Syntax muss zu einer Zeichenfolge ausgewertet werden, und Sie müssen einen in MDX geschriebenen Ausdruck einschließen. Der MDX-Ausdruck kann z. B. einen Teil des Cubes anzeigen, der in die Syntax eingeschlossen ist. MDX-Ausdrücke werden ausgewertet, bevor die Parameter übergeben werden. Darüber hinaus steht Ihnen der MDX-Generator zur Verfügung, der Sie bei der Erstellung von MDX-Ausdrücken unterstützt.  
  
 **Weitere Eigenschaften**  
 Wählen Sie die Eigenschaft aus. In der folgenden Tabelle werden die verfügbaren Eigenschaften zusammengefasst.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**Aufruf**|Gibt an, wie die Aktion ausgeführt wird. Die Standardeinstellung Interaktiv gibt an, dass die Aktion ausgeführt wird, wenn ein Benutzer auf ein Objekt zugreift. Die möglichen Einstellungen sind:<br /><br /> Batch<br /><br /> Interaktiv<br /><br /> Beim Öffnen|  
|**Application**|Beschreibt die Anwendung der Aktion.|  
|**Beschreibung**|Beschreibt die Aktion.|  
|**Beschriftung**|Stellt eine Beschriftung bereit, die für die Aktion angezeigt wird. Handelt es sich bei der Beschriftung um MDX, geben Sie **True** für **Beschriftung ist MDX**an.|  
|**Beschriftung ist MDX**|Geben Sie **True** an, wenn es sich bei der Beschriftung um MDX handelt; andernfalls geben Sie **False** an.|  
  
> [!NOTE]  
>  Sie müssen Analysis Services Scripting Language (ASSL) oder Analysis Management Objects (AMO) verwenden, um HTML- und Befehlszeilen-Aktionstypen zu definieren. Weitere Informationen finden Sie unter [Action-Element &#40;ASSL&#41;](../../analysis-services/scripting/objects/action-element-assl.md), [Type-Element &#40;Action&#41; &#40;ASSL&#41;](../../analysis-services/scripting/properties/type-element-action-assl.md) und [Programmieren von erweiterten AMO OLAP-Objekten](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-advanced-objects.md).  
  
## <a name="creating-a-reporting-action"></a>Erstellen einer Berichtsaktion  
 Der Berichtsserver antwortet auf URL-basierte Anforderungen nach Berichten. Klicken Sie zum Erstellen einer Berichtsaktion im Menü **Cube** auf **Neue Berichtsaktion**. Eine Berichtsaktion zeichnet sich durch die folgenden spezifischen Optionen aus.  
  
 **Berichtsserver**  
 Die in der folgenden Tabelle beschriebenen Eigenschaften sind spezifisch für den Berichtsserver.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**Servername**|Name des Computers, auf dem der Berichtsserver ausgeführt wird.|  
|**Serverpfad**|Der vom Berichtsserver verfügbar gemachte Pfad.|  
|**Berichtsformat**|HTML5, HTML3, Excel oder PDF.|  
  
> [!NOTE]  
>  In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]können Sie in der Servernameneigenschaft Transport Layer Security (https:) angeben.  
  
 **Parameter (Optional)**  
 Die Parameter werden als Bestandteil der URL-Zeichenfolge an den Server gesendet, wenn die Aktion erstellt wird. Dazu gehören **Parametername** und **Parameterwert**, wobei es sich um einen MDX-Ausdruck handelt.  
  
 Die Berichtsserver-URL setzt sich wie folgt zusammen:  
  
```  
  
http://  
host  
/  
virtualdirectory  
/Path&  
parametername1  
=  
parametervalue1  
& ...  
```  
  
 Beispiel:  
  
```  
http://localhost/ReportServer/Sales/YearlySalesByCategory?rs:Command=Render&Region=West  
```  
  
## <a name="creating-a-drillthrough-action"></a>Erstellen einer Drillthroughaktion  
 Eine Drillthroughaktion wird durch eine Rowsetaktion definiert, die als Drillthroughanweisung an die Clientanwendung zurückgegeben wird. Das Aktionsziel ist ein Mitglied einer Measuregruppe. Klicken Sie zum Erstellen einer neuen Drillthroughaktion im Menü **Cube** auf **Neue Drillthroughaktion**. Eine Drillthroughaktion zeichnet sich durch die folgenden spezifischen Optionen aus:  
  
 **Drillthroughspalten**  
 Wählen Sie eine oder mehrere Dimensionen aus und für jede Dimension die durch die Aktion an die Clientanwendung zurückgegebenen Drillthroughspalten.  
  
## <a name="see-also"></a>Siehe auch  
 [Cubes in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
