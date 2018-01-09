---
title: Mit aktiviertem Schreibzugriff Dimensionen | Microsoft Docs
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
- write-enabled dimensions [Analysis Services]
- dimensions [Analysis Services], write-enabled
- dimension writeback [Analysis Services]
- write-enabled cubes [Analysis Services]
- writeback [Analysis Services], dimensions
ms.assetid: 0bac050d-cd3b-427b-884a-65a91be89500
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 175199b7090abc373e0ac39d1e99e81480df4e2e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="write-enabled-dimensions"></a>Dimensionen mit aktiviertem Schreibzugriff
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
 Die Daten in einer Dimension sind im Allgemeinen schreibgeschützt. In bestimmten Szenarien kann es jedoch erwünscht sein, den Schreibzugriff für eine Dimension zu aktivieren. Wenn in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]für eine Dimension der Schreibschutz aktiviert wird, können Anwender der Unternehmenssoftware und Administratoren den Inhalt der Dimension ändern und die unmittelbaren Auswirkungen der Änderungen auf die Hierarchien der Dimension anzeigen. Der Schreibzugriff kann für jede Dimension aktiviert werden, die auf einer einzelnen Tabelle basiert. In einer Dimension mit aktiviertem Schreibzugriff können Benutzer im geschäftlichen Bereich und Administratoren Attributelemente innerhalb der Dimension ändern, verschieben, hinzufügen und löschen. Diese Updates werden zusammenfassend als *Rückschreiben von Dimensionen*bezeichnet.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]unterstützt das Rückschreiben für alle Dimensionsattribute, und jedes Element einer Dimension kann geändert werden. Für einen Cube oder eine Partition mit aktiviertem Schreibzugriff werden die Updates in einer Rückschreibetabelle getrennt von den Quelltabellen des Cubes gespeichert. Allerdings werden die Updates für eine Dimension mit aktiviertem Schreibzugriff direkt in der Tabelle der Dimension gespeichert. Auch wenn die Dimension mit aktiviertem Schreibzugriff in einen Cube mit mehreren Partitionen eingebunden ist und einige oder alle der zugehörigen Datenquellen über Kopien der Dimensionstabelle verfügen, wird während eines Rückschreibevorgangs zudem nur die Originaltabelle aktualisiert.  
  
 Dimensionen mit aktiviertem Schreibzugriff und Cubes mit aktiviertem Schreibzugriff weisen unterschiedliche, jedoch sich ergänzende Funktionen auf. Durch eine Dimension mit aktiviertem Schreibzugriff erhalten Anwender der Unternehmenssoftware und Administratoren die Möglichkeit, Elemente zu aktualisieren, wohingegen sie durch einen Cube mit aktiviertem Schreibzugriff in die Lage versetzt werden, Zellenwerte zu aktualisieren. Obwohl sich diese zwei Funktionen ergänzen, müssen Sie sie nicht kombiniert verwenden. Eine Dimension muss nicht in einen Cube eingebunden sein, damit das Rückschreiben von Dimensionen verwendet werden kann. So kann eine Dimension mit aktiviertem Schreibzugriff auch in einen Cube eingebunden sein, für den der Schreibzugriff nicht aktiviert wurde. Für die Aktivierung des Schreibzugriffs von Dimensionen und Cubes und für die Verwaltung ihrer Sicherheit verwenden Sie unterschiedliche Verfahren.  
  
 Beim Rückschreiben von Dimensionen gelten die folgenden Einschränkungen:  
  
-   Beim Erstellen eines neuen Elements müssen Sie jedes Attribut in einer Dimension angeben. Sie können kein Element einfügen, ohne dabei einen Wert für das Schlüsselattribut der Dimension anzugeben. Deshalb unterliegt das Erstellen von Elementen allen Beschränkungen (z.&#160;B. von NULL verschiedene Schlüsselwerte), die für die Dimensionstabelle definiert sind.  
  
-   Das Rückschreiben von Dimensionen wird nur für Sternschemas unterstützt. Mit anderen Worten: Eine Dimension muss auf einer einzelnen Dimensionstabelle basieren, die direkt mit einer Faktentabelle verknüpft ist. Nachdem Sie den Schreibzugriff einer Dimension aktiviert haben, überprüft [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diese Anforderung, wenn Sie eine Bereitstellung zu einer vorhandenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank ausführen oder ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt erstellen.  
  
 Jedes vorhandene Element einer Rückschreibedimension kann geändert oder gelöscht werden. Wenn ein Element gelöscht wird, wird die Löschung an alle untergeordneten Elemente weitergegeben. So würden beispielsweise in einer Customer-Dimension mit den Attributen CountryRegion, Province, City und Customer durch das Löschen eines CountryRegion-Attributs alle Provinzen, Städte und Kunden gelöscht, die zum gelöschten Land bzw. zur gelöschten Region gehören. Wenn ein Land bzw. eine Region nur über eine Provinz verfügt, würden beim Löschen dieser Provinz auch das Land bzw. die Region gelöscht.  
  
 Elemente einer Rückschreibedimension können nur innerhalb derselben Ebene verschoben werden. So könnte beispielsweise eine Stadt auf die City-Ebene in einem anderen Land bzw. einer anderen Region oder Provinz verschoben werden, nicht aber auf die Province- oder CountryRegion-Ebene. In einer Über-/Unterordnungshierarchie sind alle Elemente Blattelemente, weshalb ein Element zu allen Ebenen verschoben werden kann, außer zur **(All)** -Ebene.  
  
 Wird ein Element in einer Über-/Unterordnungshierarchie gelöscht, werden die untergeordneten Elemente zum übergeordneten Element verschoben. Für das gelöschte Element sind Updateberechtigungen in der relationalen Tabelle erforderlich, nicht aber für die verschobenen Elemente. Wenn eine Anwendung ein Element in einer Über-/Unterordnungshierarchie verschiebt, kann die Anwendung im UPDATE-Vorgang angeben, ob nachfolgende Werte des Elements zusammen mit dem Element verschoben werden sollen oder zum übergeordneten Element des Elements verschoben werden sollen. Zum rekursiven Löschen eines Elements in einer Über-/Unterordnungshierarchie muss ein Benutzer über Updateberechtigungen in der relationalen Tabelle für das Element und alle nachfolgenden Werte des Elements verfügen.  
  
> [!NOTE]  
>  Updates für das übergeordnete Attribut in einer Über-/Unterordnungshierarchie dürfen keine Updates für irgendwelche anderen Eigenschaften oder Attribute enthalten.  
  
 Alle Änderungen an einer Dimension führen zur Änderung der Dimensionsstruktur. Jede Änderung an einer Dimension wird als einzelne Transaktion angesehen, die eine inkrementelle Verarbeitung zum Aktualisieren der Dimensionsstruktur erfordert. Für Dimensionen mit aktiviertem Schreibzugriff gelten dieselben Verarbeitungsanforderungen wie für jede andere Dimension.  
  
> [!NOTE]  
>  Das Rückschreiben für Dimensionen wird nicht von verknüpften Dimensionen unterstützt.  
  
## <a name="security"></a>Security  
 Nur Anwender der Unternehmenssoftware und Administratoren in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankrollen, denen die Lese-/Schreibberechtigung für die Dimension gewährt wurde, können eine Dimension mit aktiviertem Schreibzugriff aktualisieren. Sie können für jede Rolle steuern, welche Elemente aktualisiert werden können und welche nicht. Damit Anwender der Unternehmenssoftware und Administratoren eine Dimension mit aktiviertem Schreibzugriff aktualisieren können, muss ihre Clientanwendung diese Funktionalität unterstützen. Für solche Benutzer muss die Dimension mit aktiviertem Schreibzugriff in einen Cube eingebunden sein, der nach der letzten Änderung der Dimension verarbeitet wurde. Weitere Informationen finden Sie unter [Autorisieren des Zugriffs auf Objekte und Vorgänge &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md).  
  
 Benutzer und Gruppen, die zur Administratorrolle gehören, können die Attributelemente einer Dimension mit aktiviertem Schreibzugriff aktualisieren, selbst wenn die Dimension nicht in einen Cube eingebunden ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Eigenschaften von Datenbankdimensionen](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)   
 [Partitionen mit aktiviertem Schreibzugriff](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [Dimensionen &#40;Analysis Services – mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
