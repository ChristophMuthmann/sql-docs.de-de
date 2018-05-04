---
title: Lokale Cubes (Analysis Services – mehrdimensionale Daten) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e7e55fb95d852714be54ccfb01547ddb6064694
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="local-cubes-analysis-services---multidimensional-data"></a>Lokale Cubes (Analysis Services - Mehrdimensionale Daten)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Zum Erstellen, Aktualisieren oder Löschen lokaler Cubes muss ein ASSL-Skript oder ein AMO-Programm erstellt und ausgeführt werden.  
  
 Lokale Cubes und lokale Miningmodelle ermöglichen Analysen auf einer Clientarbeitsstation, wenn deren Verbindung mit dem Netzwerk getrennt ist. Beispielsweise könnte eine Clientanwendung den OLE DB-Anbieter für OLAP 9.0 (MSOLAP.3) aufrufen, der die lokale Cube-Engine zum Erstellen und Abfragen von lokalen Cubes lädt, wie in der folgenden Abbildung dargestellt:  
  
 ![Clientarchitektur für lokale Cubes und Modelle](../../../analysis-services/multidimensional-models/olap-physical/media/as-localcubearch9.gif "Clientarchitektur für lokale Cubes und Modelle")  
  
 ADMOD.NET und Analysis Management Objects (AMO) laden zudem die lokale Cube-Engine, wenn eine Interaktion mit lokalen Cubes erfolgt. Es kann nur mit einem einzelnen Prozess auf eine lokale Cubedatei zugegriffen werden, da die lokale Cube-Engine eine lokale Cubedatei exklusiv sperrt, wenn eine Verbindung mit dem lokalen Cube hergestellt wird. Mit einem Prozess sind bis zu fünf gleichzeitige Verbindungen zulässig.  
  
 Eine CUB-Datei kann mehr als einen Cube bzw. ein Data Mining-Modell enthalten. Abfragen an die lokalen Cubes und Data Mining-Modelle werden von der lokalen Cube-Engine verarbeitet und benötigen keine Verbindung mit einer [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Instanz.  
  
> [!NOTE]  
>  Die Verwendung von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] und [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] zum Verwalten lokaler Cubes wird nicht unterstützt.  
  
## <a name="local-cubes"></a>Lokale Cubes  
 Ein lokaler Cube erstellt und aufgefüllt, die aus einem vorhandenen Cube in einer [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz oder aus einer relationalen Datenquelle.  
  
|Quelle für Daten für lokalen Cube|Erstellungsmethode|  
|------------------------------------|---------------------|  
|Serverbasierter Cube|Sie können entweder die CREATE GLOBAL CUBE-Anweisung oder eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Scripting Language (ASSL)-Skript zum Erstellen und Auffüllen eines Cubes aus einem serverbasierten Cube. Weitere Informationen finden Sie unter [GLOBAL CUBE-Anweisung CREATE &#40;MDX&#41; ](../../../mdx/mdx-data-definition-create-global-cube.md) oder [Analysis Services Scripting Language &#40;ASSL XMLA&#41;](../../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).|  
|Relationale Datenquelle|Mithilfe eines ASSL-Skripts können Sie einen Cube aus einer relationalen OLE DB-Datenbank erstellen und auffüllen. Wenn Sie einen lokalen Cube mithilfe von ASSL erstellen möchten, stellen Sie eine Verbindung mit einer lokalen Cubedatei (CUB) her und führen das ASSL-Skript auf dieselbe Weise aus, als wenn Sie ein ASSL-Skript für eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Instanz ausführen, um einen Servercube zu erstellen. Weitere Informationen finden Sie unter [Analysis Services Scripting Language &#40;ASSL für XMLA&#41;](../../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).|  
  
 Verwenden Sie die REFRESH CUBE-Anweisung, um einen lokalen Cube neu zu erstellen und seine Daten zu aktualisieren. Weitere Informationen finden Sie unter [REFRESH CUBE-Anweisung &#40;MDX&#41;](../../../mdx/mdx-data-definition-refresh-cube.md).  
  
### <a name="local-cubes-created-from-server-based-cubes"></a>Aus serverbasierten Cubes erstellte lokale Cubes  
 Wenn lokale Cubes anhand von serverbasierten Cubes erstellt werden, sind folgende Überlegungen zu berücksichtigen:  
  
-   Distinct Count Measures werden nicht unterstützt.  
  
-   Wenn Sie ein Measure hinzufügen, müssen Sie auch mindestens eine Dimension aufnehmen, die sich auf das hinzuzufügende Measure bezieht. Weitere Informationen zu dimensionsbeziehungen mit Measuregruppen finden Sie unter [Dimensionsbeziehungen](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
-   Wenn Sie eine Über-/Unterordnungshierarchie hinzufügen, werden die Ebenen und Filter einer Über-/Unterordnungshierarchie ignoriert, und die gesamte Über-/Unterordnungshierarchie wird aufgenommen.  
  
-   Elementeigenschaften werden nicht erstellt.  
  
-   Wenn Sie ein semiadditives Measure aufnehmen, sind keine Segmente für die Account-Dimension und die Time-Dimension zulässig.  
  
-   Bezugsdimensionen werden stets materialisiert.  
  
-   Wenn Sie eine m:n-Dimension einschließen, gelten die folgenden Regeln:  
  
    -   Die m:n-Dimension kann nicht segmentiert werden.  
  
    -   Sie müssen ein Measure aus der Measurezwischengruppe hinzufügen.  
  
    -   Sie können keine der Dimensionen segmentieren, die für die beiden an der m:n-Beziehung beteiligten Measuregruppen gleichzeitig vorhanden sind.  
  
-   Es werden nur die berechneten Elemente, benannten Mengen und Zuweisungen im lokalen Cube angezeigt, die auf Measures und Dimensionen beruhen, die dem lokalen Cube hinzugefügt wurden. Ungültige berechnete Elemente, benannte Mengen und Zuweisungen werden automatisch ausgeschlossen.  
  
### <a name="security"></a>Sicherheit  
 Im Auftrag eines Benutzers auf einen lokalen Cube von einem Servercube zu erstellen, müssen Sie dem Benutzer erteilt **Drillthrough und lokaler Cube** Berechtigungen für den Servercube. Weitere Informationen finden Sie unter [Erteilen von Cube-oder modellberechtigungen &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
 Lokale Cubes werden nicht wie Servercubes mithilfe von Rollen gesichert. Alle Benutzer mit Zugriff auf Dateiebene auf eine lokale Cubedatei können die darin enthaltenen Cubes abfragen. Sie können die **Verschlüsselungskennwort** Connection-Eigenschaft für eine lokale Cubedatei zum Festlegen eines Kennworts für die lokale Cubedatei. Zum Festlegen eines Kennworts für eine lokale Cubedatei ist es erforderlich, dass für alle zukünftigen Verbindungen mit der lokalen Cubedatei dieses Kennwort verwendet wird, damit die Datei abgefragt werden kann.  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE GLOBAL CUBE-Anweisung &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-global-cube.md)   
 [Entwickeln mit Analysis Services Scripting Language &#40;ASSL&#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [REFRESH CUBE-Anweisung &#40;MDX&#41;](../../../mdx/mdx-data-definition-refresh-cube.md)  
  
  
