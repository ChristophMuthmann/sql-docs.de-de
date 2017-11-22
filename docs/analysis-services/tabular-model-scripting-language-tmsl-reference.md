---
title: Tabular Model Scripting Language (TMSL)-Referenz | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c700d7f8-7e01-4052-a9ad-8200dd4009f2
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 02d8617161c4d2a023ea5b91e5e4fc2074c6c07d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="tabular-model-scripting-language-tmsl-reference"></a>Tabular Model Scripting Language (TMSL)-Referenz

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

  Tabular Model Scripting Language (TMSL) ist der Befehl und Objekt Modell-Definition-Syntax für Analysis Services-Tabellenmodell-Datenbanken mit Kompatibilitätsgrad 1200 oder höher. TMSL kommuniziert mit Analysis Services über das XMLA-Protokoll, in dem die [XMLA. Führen Sie](../analysis-services/xmla/xml-elements-methods-execute.md) Methode akzeptiert beide JSON-basierte **Anweisung** Skripts in TMSL als auch die herkömmlichen XML-basierte Skripts in [Analysis Services Scripting Language &#40; ASSL XMLA &#41; ](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).  
  
 Schlüsselelemente des TMSL umfassen Folgendes:  
  
-   Tabellarische Metadaten, die auf Grundlage Semantik für tabellarische Modelle. Ein tabellarisches Modell besteht aus Tabellen, Spalten und Beziehungen. Entsprechende Objektdefinitionen in TMSL sind jetzt, nicht überraschend, Tabellen, Spalten, Beziehungen und So weiter.  
  
     Ein neues Metadatenmodul unterstützt diese Definitionen.  
  
-   Definitionen von Systemobjekten werden als JSON statt XML strukturiert.  
  
 Davon ausgenommen sind wie die Nutzlast (in JSON oder XML) formatiert ist werden sowohl TMSL der ASSL funktional äquivalent wie sie geben Befehle und Metadaten, die XMLA-Methoden, die für die Server-Kommunikation und Datenübertragung verwendet.  
  
## <a name="how-to-use-tmsl"></a>Gewusst wie: Verwenden Sie TMSL  
 Die einfachste Möglichkeit zum Untersuchen TMSL-Skripts wird die Befehle CREATE, ALTER, DELETE oder Prozess in SQL Server Management Studio (SSMS) für ein Modell verwendet, die Sie bereits kennen. Angenommen, Sie ein vorhandenes Modell verwenden, denken Sie daran, zuerst auf den Kompatibilitätsgrad 1200 oder höher aktualisieren.  
  
1.  Suchen Sie den Befehl, die Sie verwenden möchten: [Befehle in Tabular Model Scripting Language &#40; TMSL &#41;](../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md)  
  
2.  Überprüfen Sie den Objektverweis für die Definition für Objekte, die im Befehl verwendet: [Objektdefinitionen in Tabular Model Scripting Language &#40; TMSL &#41;](../analysis-services/tabular-models-scripting-language-objects/tmsl-reference-tabular-objects.md)  
  
3.  Wählen Sie eine Methode zum Senden von TMSL-Skript aus:  
  
    -   XMLA-Fenster in Management Studio  
  
    -   **Invoke-Ascmd** über AMO PowerShell ([Cmdlet "Invoke-ASCmd"](../analysis-services/powershell/invoke-ascmd-cmdlet.md))  
  
    -   [Analysis Services-Task "DDL ausführen"](../integration-services/control-flow/analysis-services-execute-ddl-task.md) in SSIS.  
  
## <a name="model-definition-schema"></a>Modellschema-definition  
 Der folgende Screenshot zeigt eine abgekürzte Version des Schemas reduziert, um die wichtigsten Objekte anzuzeigen.  
  
 ![SSAS_TabularMetadata](../analysis-services/media/ssas-tabularmetadata.JPG "SSAS_TabularMetadata")  
  
## <a name="scripting-languages-in-analysis-services"></a>Skriptsprachen in Analysis Services  
 Analysis Services unterstützt ASSL und TMSL Skriptsprachen. Nur tabellarische Modelle mit Kompatibilitätsgrad 1200 oder höher erstellt werden in TMS im JSON-Format beschrieben.  
  
 [Analysis Services Scripting Language &#40; ASSL XMLA &#41; ](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md) war die erste Skriptsprache und ist immer noch die einzige Skriptsprache für mehrdimensionale Modelle und tabellarische Modelle mit niedrigeren Kompatibilitätsgraden (1100 oder 1103). In ASSL tabellarischer Modelle auf Kompatibilitätsgrad 110 X beschriebenen mehrdimensionale ausgedrückt, z. B. **Cube** (für ein Modell) und **Measuregroup** (für eine Tabelle).  
  
> [!NOTE]  
>  In [SQL Server Data Tools (SSDT), können Sie ein upgrade einer früheren Version Tabellenmodell durch Verwendung der TMSL Uplink seine **CompatibilityLevel** auf 1200 oder höher. Denken Sie daran, dass das Upgrade nicht rückgängig gemacht werden. Sichern Sie vor dem Upgrade, die das Modell für den Fall, dass Sie die ursprüngliche Version später benötigen.  
  
 In der folgenden Tabelle ist die scripting Language-Matrix für Analysis Services-Datenmodelle in den verschiedenen Versionen, bestimmte Kompatibilitätsgrade.  

||||||  
|-|-|-|-|-|  
|**Version**|**Multidimensional**|**Tabellarische 110 x**|**Tabellarische 1200**| **Tabellarische 1400** |
|Azure Analysis Services|NA|NA|TMSL|TMSL| 
|SQL Server 2017|ASSL|ASSL|TMSL|TMSL| 
|SQL Server 2016|ASSL|ASSL|TMSL|TMSL| 
|SQL Server 2014|ASSL|ASSL|NA|NA|   
|SQL Server 2012|ASSL|ASSL|NA|NA|  

  
## <a name="see-also"></a>Siehe auch  
 [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services Scripting Language &#40; ASSL XMLA &#41;](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [Bestimmen des Servermodus einer Analysis Services-Instanz](../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
