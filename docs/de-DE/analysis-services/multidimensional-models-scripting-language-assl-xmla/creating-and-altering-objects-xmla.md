---
title: Erstellen und Ändern von Objekten (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0089b086d6e2da0ce171ad517e9e558dd06d8f72
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="creating-and-altering-objects-xmla"></a>Erstellen und Ändern von Objekten (XMLA)
  Hauptobjekte können unabhängig erstellt, geändert und gelöscht werden. Zu den Hauptobjekten gehören die folgenden Objekte:  
  
-   Server  
  
-   Datenbanken  
  
-   Dimensionen  
  
-   Cubes  
  
-   Measuregruppen  
  
-   Partitionen  
  
-   Perspektiven  
  
-   Miningmodelle  
  
-   Rollen  
  
-   Einem Server oder einer Datenbank zugeordnete Befehle  
  
-   Datenquellen  
  
 Verwenden Sie die [erstellen](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md) Befehl zum Erstellen von ein Hauptobjekt auf einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], und die [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) Befehl aus, um ein vorhandenes Objekt auf einer Instanz zu ändern. Beide Befehle werden ausgeführt, mit der [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) Methode.  
  
## <a name="creating-objects"></a>Erstellen von Objekten  
 Beim Erstellen von Objekten mithilfe der **erstellen** -Methode, müssen Sie zunächst das übergeordnete Objekt, das enthält identifizieren die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zu erstellendes Objekt wäre. Bestimmen Sie das übergeordnete Objekt durch die Bereitstellung eines Objektverweis in der [ParentObject](../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md) Eigenschaft von der **erstellen** Befehl. Jeder Objektverweis enthält die Objektbezeichner, die erforderlich sind, zur eindeutigen Identifizierung das übergeordnete Objekt für die **erstellen** Befehl. Weitere Informationen über Objektverweise finden Sie unter [definieren und Identifizieren von Objekten &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md).  
  
 Beispielsweise müssen Sie einen Objektverweis auf einen Cube bereitstellen, um eine neue Measuregruppe für den Cube zu erstellen. Der Objektverweis für den Cube in der **ParentObject** Eigenschaft enthält sowohl einen Datenbankbezeichner als auch einen cubebezeichner, wie der gleiche cubebezeichner potenziell von einer anderen Datenbank verwendet werden kann.  
  
 Die [ObjectDefinition](../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md) Element enthält Analysis Services Scripting Language (ASSL)-Elemente, die definieren, das Hauptobjekt erstellt werden soll. Weitere Informationen über ASSL finden Sie unter [Entwickeln mit Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Wenn Sie festlegen, die **AllowOverwrite** Attribut des der **erstellen** Befehl auf "true", können Sie ein vorhandenes Hauptobjekt mit dem angegebenen Bezeichner überschreiben. Andernfalls tritt ein Fehler auf, wenn im übergeordneten Objekt bereits ein Hauptobjekt mit dem gleichen Bezeichner vorhanden ist.  
  
 Weitere Informationen zu den **erstellen** Befehl, finden Sie unter [Element erstellen &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md).  
  
### <a name="creating-session-objects"></a>Erstellen von Sitzungsobjekten  
 Sitzungsobjekte sind temporäre Objekte, die nur für die explizite oder implizierte Sitzung zur Verfügung stehen, die von einer Clientanwendung verwendet werden. Bei Beendigung der Sitzung werden diese gelöscht. Sie können Sitzungsobjekte erstellen, durch Festlegen der **Bereich** Attribut des der **erstellen** Befehl *Sitzung*.  
  
> [!NOTE]  
>  Bei Verwendung der *Sitzung* festlegen, die **ObjectDefinition** Element darf nur [Dimension](../../analysis-services/scripting/objects/dimension-element-assl.md), [Cube](../../analysis-services/scripting/objects/cube-element-assl.md), oder [ MiningModel](../../analysis-services/scripting/objects/miningmodel-element-assl.md) ASSL-Elemente.  
  
## <a name="altering-objects"></a>Ändern von Objekten  
 Beim Ändern von Objekten mithilfe der **Alter** -Methode, müssen Sie zunächst das Objekt, das geändert werden, indem Sie einen Objektverweis in identifizieren die [Objekt](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) Eigenschaft von der **Alter**Befehl. Jeder Objektverweis enthält die Objektbezeichner, die zur eindeutigen Identifizierung des Objekts benötigt die **Alter** Befehl. Weitere Informationen über Objektverweise finden Sie unter [definieren und Identifizieren von Objekten &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md).  
  
 Beispielsweise müssen Sie einen Objektverweis auf einen Cube bereitstellen, um die Struktur eines Cubes zu ändern. Der Objektverweis für den Cube in der **Objekt** Eigenschaft enthält sowohl einen Datenbankbezeichner als auch einen cubebezeichner, wie der gleiche cubebezeichner potenziell von einer anderen Datenbank verwendet werden kann.  
  
 Die **"objectdefinition"** -Element enthält ASSL-Elemente, die zu ändernden Hauptobjekts definieren. Weitere Informationen über ASSL finden Sie unter [Entwickeln mit Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Wenn Sie festlegen, die **AllowCreate** Attribut des der **Alter** Befehl auf "true", können Sie das angegebene Hauptobjekt erstellen, wenn das Objekt nicht vorhanden ist. Andernfalls tritt ein Fehler auf, wenn ein angegebenes Hauptobjekt nicht bereits vorhanden ist.  
  
### <a name="using-the-objectexpansion-attribute"></a>Verwenden des ObjectExpansion-Attributs  
 Wenn Sie nur die Eigenschaften des Hauptobjekts ändern und sind nicht nebenobjekte, die im Hauptobjekt enthalten sind, legen Sie die **ObjectExpansion** Attribut des der **Alter** -Befehl an *' ObjectProperties '*. Die **ObjectDefinition** Eigenschaft ist dann nur die Elemente für die Eigenschaften des Hauptobjekts enthalten hat und die **Alter** -Befehl lässt die unverändert Hauptobjekt gehörenden nebenobjekte.  
  
 Um nebenobjekte für ein Hauptobjekt neu definieren, müssen Sie festlegen, die **ObjectExpansion** -Attribut *ExpandFull* und die Objektdefinition muss alle nebenobjekte sind Objekte, die im Hauptobjekt enthalten sind enthalten. Wenn die **ObjectDefinition** Eigenschaft von der **Alter** Befehl schließt nicht explizit ein nebenobjekt aus, die im Hauptobjekt enthalten sind, wird das kleinere Objekt, das nicht enthalten war, wurde gelöscht.  
  
### <a name="altering-session-objects"></a>Ändern von Sitzungsobjekten  
 So ändern Sie die Session-Objekte erstellt, indem die **erstellen** Befehl, legen die **Bereich** Attribut des der **Alter** Befehl *Sitzung*.  
  
> [!NOTE]  
>  Bei Verwendung der *Sitzung* festlegen, die **ObjectDefinition** Element darf nur [Dimension](../../analysis-services/scripting/objects/dimension-element-assl.md), [Cube](../../analysis-services/scripting/objects/cube-element-assl.md), oder [ MiningModel](../../analysis-services/scripting/objects/miningmodel-element-assl.md) ASSL-Elemente.  
  
## <a name="creating-or-altering-subordinate-objects"></a>Erstellen oder Ändern von untergeordneten Objekten  
 Obwohl eine **erstellen** oder **Alter** Befehl erstellt oder ändert Sie nur eine oberste Hauptobjekt, das Hauptobjekt erstellt oder geändert wird, darf Definitionen innerhalb der einschließenden  **"Objectdefinition"** -Eigenschaft für andere Haupt- und Nebenversionsnummern Objekte, die, die ihm untergeordnet sind. Z. B. Wenn Sie einen Cube definieren, geben Sie die übergeordnete Datenbank in **ParentObject**, und innerhalb der Cubedefinition in **ObjectDefinition** können Sie Measuregruppen für den Cube und innerhalb des Measures definieren Gruppen können Sie Partitionen für jede Measuregruppe definieren. Ein Nebenobjekt kann nur unter dem Hauptobjekt definiert werden, das es enthält. Weitere Informationen über Haupt-und nebenobjekte finden Sie unter [Datenbankobjekte &#40;Analysis Services – mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="description"></a>Description  
 Das folgende Beispiel erstellt eine relationale Datenquelle, verweist der [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] Beispiel [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank.  
  
### <a name="code"></a>Code  
  
```  
<Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    </ParentObject>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ImpersonationInfo>  
                <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
            </ImpersonationInfo>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT0S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Create>  
```  
  
### <a name="description"></a>Description  
 Im folgenden Beispiel wird die im vorherigen Beispiel erzeugte relationale Datenquelle so geändert, dass der Abfragetimeout der Datenquelle nach 30 Sekunden einsetzt.  
  
### <a name="code"></a>Code  
  
```  
<Alter ObjectExpansion="ObjectProperties" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DataSourceID>AdventureWorksDW2012</DataSourceID>  
    </Object>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=fr-dwk-02;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT30S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Alter>  
```  
  
### <a name="comments"></a>Kommentare  
 Die **ObjectExpansion** Attribut des der **Alter** Befehlssatz wurde um *' ObjectProperties '*. Mit dieser Einstellung kann die [ImpersonationInfo](../../analysis-services/scripting/properties/impersonationinfo-element-assl.md) -Element, ein nebenobjekt aus der Datenquelle, die in definierten Auszuschließendes **"objectdefinition"**. Daher bleiben die Informationen zum Identitätswechsel für die Datenquelle auf "Service Account" festgelegt, wie es im ersten Beispiel angegeben ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Execute-Methode &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)   
 [Entwickeln mit Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
