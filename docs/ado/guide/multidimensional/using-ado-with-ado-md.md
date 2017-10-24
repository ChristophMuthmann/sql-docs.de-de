---
title: Verwenden von ADO mit ADO MD | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 38df55c27ced6e0a7b32c321e2b3968bedb73aa1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-ado-with-ado-md"></a>Verwenden von ADO mit ADO MD
ADO und ADO MD sind verwandte aber separate Objektmodelle. ADO stellt Objekte für das Herstellen einer Verbindung mit Datenquellen, Ausführen von Befehlen, Abrufen von Tabellendaten und Schemametadaten in einem tabellarischen Format und Anzeigen von Anbieter-Fehlerinformationen bereit. ADO MD bietet Objekte zum Abrufen von mehrdimensionalen Daten und Anzeigen von Metadaten von mehrdimensionalen Schema.  
  
 Bei der Arbeit mit einem MDP können Sie auswählen, ADO, ADO MD oder beides mit Ihrer Anwendung verwenden. Durch Verweisen auf beide Bibliotheken innerhalb des Projekts, müssen Sie Vollzugriff auf die Funktionalität, die von Ihrem MDP bereitgestellt.  
  
 Es ist häufig nützlich für Consumer eine vereinfachte, tabellarische Darstellung eines mehrdimensionalen Datasets zu erhalten. Hierzu können Sie mithilfe von ADO [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt. Geben Sie die Quelle für Ihre [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) als die ***Quelle*** -Parameter für die [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) Methode eine **Recordset**, anstatt als Quelle für ein ADO MD **Cellset**.  
  
 Es kann auch zum Anzeigen der Schemametadaten in einer tabellarischen Ansicht nicht als Hierarchie von Objekten nützlich sein. Das ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) Methode für die [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt ermöglicht es dem Benutzer, öffnen Sie eine **Recordset** , die die Schemainformationen enthält. Die ***QueryType*** Parameter von der **OpenSchema** Methode besitzt mehrere [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) Werte, die speziell MDPs betreffen. Die Werte lauten wie folgt:  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 Um Enumerationswerte von ADO mit ADO MD-Eigenschaften oder Methoden verwenden, muss das Projekt ADO und ADO MD-Bibliotheken verweisen. Sie können z. B. das ADO **AdState** Enumerationswerte mit der ADO MD [Zustand](../../../ado/reference/ado-md-api/state-property-ado-md.md) Eigenschaft. Weitere Informationen dazu, wie Verweise auf Bibliotheken herstellen finden Sie in der Dokumentation zu Ihrem Entwicklungstool.  
  
 Weitere Informationen zu den ADO-Objekte und Methoden finden Sie unter der [ADO-API-Referenz](../../../ado/reference/ado-api/ado-api-reference.md).  
  
## <a name="see-also"></a>Siehe auch  
 [ADO MD-Objektmodell](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Übersicht über multidimensionale Schemas und Daten](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programmieren mit ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Arbeiten mit mehrdimensionalen Daten](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)

