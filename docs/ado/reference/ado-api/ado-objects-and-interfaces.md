---
title: ADO-Objekte und Schnittstellen | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and interfaces
- objects [ADO]
ms.assetid: d0b7e254-c89f-4406-b846-a060ef038c30
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 047e1a7a0cafee0b562edc5b3ec47f9f4dd3989d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ado-objects-and-interfaces"></a>ADO-Objekte und Schnittstellen
Die Beziehungen zwischen diesen Objekten werden dargestellt, der [ADO-Objektmodell](../../../ado/reference/ado-api/ado-object-model.md).  
  
 Jedes Objekt kann in der entsprechenden Auflistung enthalten sein. Angenommen, ein [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt enthalten sein kann, einer [Fehler](../../../ado/reference/ado-api/errors-collection-ado.md) Auflistung. Weitere Informationen finden Sie unter [ADO-Auflistungen](../../../ado/reference/ado-api/ado-collections.md) oder eine bestimmte Sammlung Thema.  
  
|||  
|-|-|  
|[IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)|Zum Abrufen der zugrunde liegenden OLE DB-Befehl von einem Objekt ADOCommand verwendet.|  
|[ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)|Erstellt ein ADO **Datensatz** Objekt aus einer OLE DB- **Zeile** Objekt in einer C-/C++-Anwendung.|  
|[ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)|Erstellt ein ADO **Recordset** Objekt aus einer OLE DB- **Rowset** Objekt in einer C-/C++-Anwendung.|  
|[ADOStreamConstruction-Schnittstelle](../../../ado/reference/ado-api/adostreamconstruction-interface.md)|Erstellt ein ADO **Stream** Objekt aus einer OLE DB- **IStream** Objekt in einer C-/C++-Anwendung.|  
|[Befehl](../../../ado/reference/ado-api/command-object-ado.md)|Definiert einen bestimmten Befehl, den Sie für eine Datenquelle ausführen möchten.<br /><br /> Die **Befehl** Objekt ist nicht sicher für Skripting.|  
|[Verbindung](../../../ado/reference/ado-api/connection-object-ado.md)|Stellt eine offene Verbindung mit einer Datenquelle dar.<br /><br /> Die **Verbindung** Objekt für die Skripterstellung sicher ist.|  
|[IDSOShapeExtensions-Schnittstelle](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)|Ruft das zugrunde liegende Objekt für den OLE DB-Datenquelle für die SHAPE-Anbieters ab.|  
|[Fehler](../../../ado/reference/ado-api/error-object.md)|Enthält Details über Data Access-Fehlern, die auf einem einzelnen Vorgang im Zusammenhang mit dem Anbieter beziehen.<br /><br /> Die **Fehler** Objekt ist nicht sicher für Skripting.|  
|[Feld](../../../ado/reference/ado-api/field-object.md)|Stellt eine Spalte von Daten mit einem gemeinsamen Datentyp.|  
|[Parameter](../../../ado/reference/ado-api/parameter-object.md)|Stellt einen Parameter oder das zugeordnete Argument eine **Befehl** -Objekt auf Grundlage einer parametrisierten Abfrage oder gespeicherte Prozedur.<br /><br /> Die **Parameter** Objekt ist nicht sicher für Skripting.|  
|[Eigenschaft](../../../ado/reference/ado-api/property-object-ado.md)|Stellt ein dynamisches Merkmal eines ADO-Objekts, das vom Anbieter definiert ist.|  
|[Datensatz](../../../ado/reference/ado-api/record-object-ado.md)|Stellt eine Zeile mit einem **Recordset**, oder ein Verzeichnis oder eine Datei in einem Dateisystem. Die **Datensatz** Objekt für die Skripterstellung sicher ist.|  
|[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)|Stellt den Satz von Datensätzen aus einer Basistabelle oder die Ergebnisse eines ausgeführten Befehls dar. Zu jedem Zeitpunkt die **Recordset** Objekt bezieht sich auf nur einen einzelnen Datensatz in der Gruppe als der aktuelle Datensatz.<br /><br /> Die **Recordset** Objekt für die Skripterstellung sicher ist.|  
|[Stream](../../../ado/reference/ado-api/stream-object-ado.md)|Stellt einen binären Datenstrom dar.<br /><br /> Die **Stream** Objekt für die Skripterstellung sicher ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-API-Referenz](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO-Auflistungen](../../../ado/reference/ado-api/ado-collections.md)   
 [Dynamische Eigenschaften von ADO.NET](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO--Enumerationskonstanten](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Anhang B: ADO-Fehler](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO-Ereignisse](../../../ado/reference/ado-api/ado-events.md)   
 [ADO-Methoden](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO-Objektmodell](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO-Eigenschaften](../../../ado/reference/ado-api/ado-properties.md)
