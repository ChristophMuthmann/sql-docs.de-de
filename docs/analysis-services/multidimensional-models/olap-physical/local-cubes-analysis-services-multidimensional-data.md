---
title: "Lokale Cubes (Analysis Services – mehrdimensionale Daten) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: cubes [Analysis Services], local
ms.assetid: e52e1515-35a7-4dc3-9bbf-736d176ba0c7
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5872bd5a1efda8d8add71bc1ce0e089785352e11
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="local-cubes-analysis-services---multidimensional-data"></a>Lokale Cubes (Analysis Services - Mehrdimensionale Daten)
  Zum Erstellen, Aktualisieren oder Löschen lokaler Cubes muss ein ASSL-Skript oder ein AMO-Programm erstellt und ausgeführt werden.  
  
 Lokale Cubes und lokale Miningmodelle ermöglichen Analysen auf einer Clientarbeitsstation, wenn deren Verbindung mit dem Netzwerk getrennt ist. Beispielsweise könnte eine Clientanwendung den OLE DB-Anbieter für OLAP 9.0 (MSOLAP.3) aufrufen, der das lokale Cubemodul zum Erstellen und Abfragen von lokalen Cubes lädt, wie in der folgenden Abbildung dargestellt:  
  
 ![Clientarchitektur für lokale Cubes und Modelle](../../../analysis-services/multidimensional-models/olap-physical/media/as-localcubearch9.gif "Clientarchitektur für lokale Cubes und Modelle")  
  
 ADMOD.NET und Analysis Management Objects (AMO) laden zudem das lokale Cubemodul, wenn eine Interaktion mit lokalen Cubes erfolgt. Es kann nur mit einem einzelnen Prozess auf eine lokale Cubedatei zugegriffen werden, da das lokale Cubemodul eine lokale Cubedatei exklusiv sperrt, wenn eine Verbindung mit dem lokalen Cube hergestellt wird. Mit einem Prozess sind bis zu fünf gleichzeitige Verbindungen zulässig.  
  
 Eine CUB-Datei kann mehr als einen Cube bzw. ein Data Mining-Modell enthalten. Abfragen an die lokalen Cubes und Data Mining-Modelle werden vom lokalen Cubemodul verarbeitet und benötigen keine Verbindung mit einer [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Instanz.  
  
> [!NOTE]  
>  Die Verwendung von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] und [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] zum Verwalten lokaler Cubes wird nicht unterstützt.  
  
## <a name="local-cubes"></a>Lokale Cubes  
 Ein lokaler Cube erstellt und aufgefüllt, die aus einem vorhandenen Cube in einer [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz oder aus einer relationalen Datenquelle.  
  
|Quelle für Daten für lokalen Cube|Erstellungsmethode|  
|------------------------------------|---------------------|  
|Serverbasierter Cube|Sie können entweder die CREATE GLOBAL CUBE-Anweisung oder eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Scripting Language (ASSL)-Skript zum Erstellen und Auffüllen eines Cubes aus einem serverbasierten Cube. Weitere Informationen finden Sie unter [GLOBAL CUBE-Anweisung CREATE &#40; MDX &#41; ](../../../mdx/mdx-data-definition-create-global-cube.md) oder [Analysis Services Scripting Language &#40; ASSL XMLA &#41; ](../../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).|  
|Relationale Datenquelle|Mithilfe eines ASSL-Skripts können Sie einen Cube aus einer relationalen OLE DB-Datenbank erstellen und auffüllen. Wenn Sie einen lokalen Cube mithilfe von ASSL erstellen möchten, stellen Sie eine Verbindung mit einer lokalen Cubedatei (CUB) her und führen das ASSL-Skript auf dieselbe Weise aus, als wenn Sie ein ASSL-Skript für eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Instanz ausführen, um einen Servercube zu erstellen. Weitere Informationen finden Sie unter [Analysis Services Scripting Language &#40;ASSL für XMLA&#41;](../../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).|  
  
 Verwenden Sie die REFRESH CUBE-Anweisung, um einen lokalen Cube neu zu erstellen und seine Daten zu aktualisieren. Weitere Informationen finden Sie unter [REFRESH CUBE-Anweisung &#40; MDX &#41; ](../../../mdx/mdx-data-definition-refresh-cube.md).  
  
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
 Im Auftrag eines Benutzers auf einen lokalen Cube von einem Servercube zu erstellen, müssen Sie dem Benutzer erteilt **Drillthrough und lokaler Cube** Berechtigungen für den Servercube. Weitere Informationen finden Sie unter [gewähren, Cube oder modellberechtigungen &#40; Analysis Services &#41; ](../../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
 Lokale Cubes werden nicht wie Servercubes mithilfe von Rollen gesichert. Alle Benutzer mit Zugriff auf Dateiebene auf eine lokale Cubedatei können die darin enthaltenen Cubes abfragen. Sie können die **Verschlüsselungskennwort** Connection-Eigenschaft für eine lokale Cubedatei zum Festlegen eines Kennworts für die lokale Cubedatei. Zum Festlegen eines Kennworts für eine lokale Cubedatei ist es erforderlich, dass für alle zukünftigen Verbindungen mit der lokalen Cubedatei dieses Kennwort verwendet wird, damit die Datei abgefragt werden kann.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie GLOBAL CUBE-Anweisung &#40; MDX &#41;](../../../mdx/mdx-data-definition-create-global-cube.md)   
 [Entwickeln mit Analysis Services Scripting Language &#40; ASSL &#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [REFRESH CUBE-Anweisung &#40; MDX &#41;](../../../mdx/mdx-data-definition-refresh-cube.md)  
  
  
