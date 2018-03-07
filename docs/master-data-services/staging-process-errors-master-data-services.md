---
title: Fehler des Stagingprozesses (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- staging process [Master Data Services], error messages
ms.assetid: 0d9be0dd-638f-4dd4-92b2-253fda655455
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0560f760a619630bb0ccc9183b30674da89d5f8
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2018
---
# <a name="staging-process-errors-master-data-services"></a>Fehler des Stagingprozesses (Master Data Services)
  Nach Abschluss des Stagingprozesses verfügen alle in den Stagingtabellen verarbeitete Datensätze über einen Werte in der Spalte ErrorCode. Diese Werte sind in der folgenden Tabelle aufgeführt.  
  
|Code|Fehler|Tritt auf, wenn/Details|Gilt für Tabelle|  
|----------|-----------|--------------------------|----------------------|  
|210001|Der gleiche Elementcode ist in der Stagingtabelle mehrmals vorhanden.|In Ihrer Stagingbatch ist der gleiche Elementcode mehrmals vorhanden. Keines der Elemente wird erstellt oder aktualisiert.|Blatt<br /><br /> Konsolidiert<br /><br /> Beziehung|  
|210003|Die Attributwerte verweisen auf ein Element, das nicht vorhanden oder inaktiv ist.|Wenn Sie domänenbasierte Attribute bereitstellen, müssen Sie den Code und nicht den Namen verwenden. Gilt für **ImportType0**, **1**und **2**.|Blatt<br /><br /> Konsolidiert|  
|210006|Der Elementcode ist inaktiv.|**ImportType** = **1** , und Sie haben einen Elementcode angegeben, der nicht vorhanden ist.|Blatt<br /><br /> Konsolidiert<br /><br /> Beziehung|  
|210032|Der Hierarchiename fehlt oder ist nicht gültig.|Die explizite Hierarchie wurde nicht gefunden, oder der **HierarchyName** -Wert war leer.|Konsolidiert<br /><br /> Beziehung|  
|210035|Da keine Geschäftsregel zur Codegenerierung vorhanden ist, wird der **MemberCode** benötigt.|Beim Erstellen oder Aktualisieren von Elementen ist ein **MemberCode** immer erforderlich, außer wenn Sie die automatische Codegenerierung verwenden. Weitere Informationen finden Sie unter [Automatische Codeerstellung &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md).|Blatt<br /><br /> Konsolidiert|  
|210036|Da eine Geschäftsregel zur Codegenerierung vorhanden ist, wird der **MemberCode** nicht benötigt.|Beim Erstellen oder Aktualisieren von Elementen ist ein **MemberCode** nicht erforderlich, wenn Sie die automatische Codegenerierung verwenden. Sie können jedoch einen Code angeben, wenn Sie dies möchten. Weitere Informationen finden Sie unter [Automatische Codeerstellung &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md).|Blatt<br /><br /> Konsolidiert|  
|210041|"ROOT" ist kein gültiger Elementcode.|Der **MemberCode** -Wert enthält das Wort "ROOT".|Blatt<br /><br /> Konsolidiert<br /><br /> Beziehung|  
|210042|"MDMUNUSED" ist kein gültiger Elementcode.|Der **MemberCode** -Wert enthält das Wort "MDMUNUSED".|Blatt<br /><br /> Konsolidiert<br /><br /> Beziehung|  
|210052|Der MemberCode kann nicht deaktiviert werden, da er als domänenbasierter Attributwert verwendet wird.|Wenn **ImportType** = **3** oder **4**ist, schlägt das Staging fehl, wenn das Element als Attributwert für andere Elemente verwendet wird. Legen Sie den Wert entweder mithilfe von **ImportType5** **6** auf NULL fest, oder ändern Sie die Werte vor dem Ausführen des Stagingprozesses.|Blatt<br /><br /> Konsolidiert|  
|300002|Der Elementcode ist nicht gültig.|Beziehungen: Entweder ist der übergeordnete oder der untergeordnete Elementcode nicht vorhanden.<br /><br /> Blatt oder konsolidiert: **ImportType** = **3** oder **4** und der Elementcode ist nicht vorhanden.|Blatt<br /><br /> Konsolidiert<br /><br /> Beziehung|  
|300004|Der Elementcode ist bereits vorhanden.|**ImportType** = **1** , und Sie haben einen Elementcode verwendet, der bereits in der Entität vorhanden ist.|Blatt<br /><br /> Konsolidiert|  
|210011|Wenn **RelationshipType** **1**ist, kann der **ParentCode** kein Blattelement sein.|Stellen Sie sicher, dass der **ParentCode** -Wert ein konsolidierter Elementcode ist.|Beziehung|  
|210015|Der Elementcode für eine Hierarchie und einen Batch ist in der Stagingtabelle mehrmals vorhanden.|Sie haben für eine explizite Hierarchie im gleichen Batch mehrmals den Speicherort des gleichen Elements angegeben.|Beziehung|  
|210016|Die Beziehung konnte nicht erstellt werden, da sie einen Zirkelverweis verursachen würde.|Dieser Fehler tritt auf, wenn Sie versuchen, ein untergeordnetes Element als übergeordnetes Element zuzuweisen.|Beziehung|  
|210046|Das Element kann kein gleichgeordnetes Element von Root sein.|Dieser Fehler tritt auf, wenn **RelationshipType** = **2** (gleichgeordnet) und entweder **ParentCode** oder **ChildCode** **Root**sind. Elemente können sich nicht auf der gleichen Ebene wie der Stammknoten befinden. Sie können nur untergeordnete Elemente sein.|Beziehung|  
|210047|Das Element kann kein gleichgeordnetes Element von "Nicht verwendet" sein.|Dieser Fehler tritt auf, wenn **RelationshipType** = **2** (gleichgeordnet) und entweder **ParentCode** oder **ChildCode** **Unused**sind. Elemente können nur untergeordnete Elemente des Knotens "Nicht verwendet" sein.|Beziehung|  
|210048|**ParentCode** und **ChildCode** können nicht identisch sein.|Der **ParentCode** -Wert ist identisch mit dem **ChildCode** -Wert. Diese Werte müssen unterschiedlich sein.|Beziehung|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anzeigen von Fehlern, die während des Stagings auftreten &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [Übersicht: Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)  
  
  
