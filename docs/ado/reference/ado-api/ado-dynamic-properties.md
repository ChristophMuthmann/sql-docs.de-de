---
title: Dynamische Eigenschaften von ADO.NET | Microsoft Docs
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
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fca9f032f5a72df58b18206c8441365ce3c8a746
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="ado-dynamic-properties"></a>Dynamische Eigenschaften von ADO.NET
Dynamische Eigenschaften hinzugefügt werden können die [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Sammlungen von der [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md), [Befehl](../../../ado/reference/ado-api/command-object-ado.md), oder [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekte. Die Quelle für diese Eigenschaften ist entweder ein Datenanbieter, wie z. B. die [OLE DB-Anbieter für SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), oder ein Dienstanbieter, wie z. B. die [Microsoft Cursor Service für OLE DB-](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md). Finden Sie in der entsprechenden Datenanbieter oder die Service Provider Dokumentation weitere Informationen zu einer bestimmten dynamische Eigenschaft.  
  
 Die [ADO dynamische Property-Index](../../../ado/reference/ado-api/ado-dynamic-property-index.md) stellt einen Querverweis zwischen den ADO- und OLE DB-Namen für jede dynamische Eigenschaft der standard OLE DB-Anbieter bereit.  
  
 Die folgenden dynamischen Eigenschaften sind besonders interessant, und auch in den Quellen, die weiter oben erwähnt wurden dokumentiert sind. Spezielle Funktionen mit ADO ist in der ADO-Hilfethemen in der folgenden Liste beschrieben.  
  
|||  
|-|-|  
|[Optimieren](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|Gibt an, ob für dieses Feld ein Index erstellt werden soll.|  
|[Auffordern](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|Gibt an, ob der OLE DB-Anbieter den Benutzer zur Initialisierungsinformationen aufzufordern sollten.|  
|[Umstrukturieren von Namen](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Gibt einen Namen für die **Recordset** Objekt.|  
|[Resync-Befehl](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Gibt an, ein Befehl Benutzer bereitgestellte Zeichenfolge, die **Resync** Probleme der Methode zum Aktualisieren der Daten in der Tabelle mit dem Namen der **eindeutige Tabelle** dynamische Eigenschaft.|  
|[Eindeutige Tabelle, eindeutiges Schema, eindeutige Katalog](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**Eindeutige Tabelle** gibt den Namen der Basistabelle, auf denen Updates, einfügungen und löschungen zulässig sind.<br /><br /> **Eindeutiges Schema** gibt an, das Schema oder der Name des Besitzers der Tabelle.<br /><br /> **Eindeutige Katalog** gibt an, den Katalog oder die Namen der Datenbank, die die Tabelle enthält.|  
|[Aktualisieren Sie die erneute Synchronisierung](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|Gibt an, ob die **UpdateBatch** Methode einen impliziten gefolgt **Resync** Vorgangs-Methode, und wenn dies der Fall ist, den Bereich dieses Vorgangs.|  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-API-Referenz](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO-Auflistungen](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO--Enumerationskonstanten](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Anhang B: ADO-Fehler](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO-Ereignisse](../../../ado/reference/ado-api/ado-events.md)   
 [ADO-Methoden](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO-Objektmodell](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO-Objekte und Schnittstellen](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Eigenschaften von ADO.NET](../../../ado/reference/ado-api/ado-properties.md)

