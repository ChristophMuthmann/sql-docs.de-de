---
title: ASSL-Objekte und-Objekteigenschaften | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 17b88ba72205f2364a65f2d6cc88fe19b820985e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="assl-objects-and-object-characteristics"></a>ASSL-Objekte und -Objekteigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Objekte in Analysis Services Scripting Language (ASSL) folgen spezifischen Richtlinien in Bezug auf Objektgruppen, Vererbung, Benennung, Erweiterung und Verarbeitung.  
  
## <a name="object-groups"></a>Objektgruppen  
 Alle [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Objekte weisen eine XML-Darstellung. Die Objekte sind in zwei Gruppen unterteilt:  
  
 **Hauptobjekte**  
 Hauptobjekte können unabhängig erstellt, geändert und gelöscht werden. Zu den Hauptobjekten gehören:  
  
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
  
 Hauptobjekte haben die folgenden Eigenschaften, um ihren Verlauf und Status nachzuverfolgen.  
  
-   **CreatedTimestamp**  
  
-   **LastSchemaUpdate**  
  
-   **LastProcessed** (wenn geeignet)  
  
> [!NOTE]  
>  Die Klassifizierung eines Objekts als Hauptobjekt wirkt sich darauf aus, wie eine Instanz von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] dieses Objekt behandelt und wie es in der Objektdefinitionssprache gehandhabt wird. Diese Klassifizierung ist jedoch nicht garantiert, die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Verwaltungs-und Entwicklungstools werden das unabhängige erstellen, ändern oder Löschen dieser Objekte zulassen.  
  
 **Nebenobjekte**  
 Nebenobjekte sind Objekte, die nur im Rahmen des Erstellens, Änderns oder Löschens des übergeordneten Hauptobjekts erstellt, geändert oder gelöscht werden können. Zu den Nebenobjekten gehören:  
  
-   Hierarchien und Ebenen  
  
-   Attribute  
  
-   Measures  
  
-   Miningmodellspalten  
  
-   Einem Cube zugeordnete Befehle  
  
-   Aggregationen  
  
## <a name="object-expansion"></a>ObjectExpansion  
 Mit der **ObjectExpansion** -Beschränkung kann der Grad der Erweiterung des vom Server zurückgegebenen ASSL XML-Werts festgelegt werden. Für diese Beschränkung sind die in der folgenden Tabelle aufgeführten Optionen verfügbar.  
  
|Enumerationswert|Zulässige \<Alter >|Description|  
|-----------------------|---------------------------|-----------------|  
|*ReferenceOnly*|nein|Gibt nur den Namen, die ID und den Timestamp für das angeforderte Objekt und alle enthaltenen Hauptobjekte rekursiv zurück.|  
|*' ObjectProperties '*|ja|Erweitert das angeforderte Objekt und die enthaltenen Nebenobjekte, aber gibt keine enthaltenen Hauptobjekte zurück.|  
|*' ExpandObject '*|nein|Wie *ObjectProperties*, gibt jedoch auch den Namen, die ID und den Timestamp für enthaltene Hauptobjekte zurück.|  
|*ExpandFull*|ja|Erweitert das angeforderte Objekt und alle enthaltenen Objekte vollständig und rekursiv.|  
  
 In diesem ASSL-Verweisabschnitt wird die *ExpandFull* -Darstellung beschrieben. Alle anderen **ObjectExpansion** -Ebenen werden von dieser Ebene abgeleitet.  
  
## <a name="object-processing"></a>Objektverarbeitung  
 ASSL enthält schreibgeschützte Elemente oder Eigenschaften (z. B. **LastProcessed**), die gelesen werden können, aus der [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz, jedoch ausgelassen werden, wenn Befehlsskripts an die Instanz übermittelt werden. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ignoriert geänderte Werte für schreibgeschützte Elemente ohne Warnmeldungen oder Fehler an.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ignoriert auch unpassende oder irrelevante Eigenschaften, ohne Überprüfungsfehler auszulösen. Beispielsweise sollte das X-Element nur vorhanden sein, wenn das Y-Element einen besonderen Wert aufweist. Die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Instanz ignoriert das X-Element, anstatt es zu überprüfen, mit dem Wert des Y-Elements.  
  
  
