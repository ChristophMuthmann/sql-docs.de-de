---
title: OpenSchema-Methode | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::OpenSchema
- Connection15::raw_OpenSchema
helpviewer_keywords:
- OpenSchema method [ADO]
ms.assetid: 850cf3ce-f18f-4e7c-8597-96c1dc504866
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e4f733285741c3ddc23716ed43efd93375a3de4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="openschema-method"></a>OpenSchema-Methode
Ruft die Schemainformationen für die Datenbank vom Anbieter ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt, das Schemainformationen enthält. Die **Recordset** als schreibgeschützte, statische Cursor geöffnet wird. Die *QueryType* bestimmt, welche Spalten in angezeigt werden die **Recordset**.  
  
#### <a name="parameters"></a>Parameter  
 *QueryType*  
 Alle [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) Wert, der den Typ des auszuführenden Schemaabfragen darstellt.  
  
 *Kriterien*  
 Optional. Ein Array von Abfrage-Einschränkungen für die einzelnen *QueryType* option gemäß [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md).  
  
 *SchemaID*  
 Die GUID für einen Anbieter Schemaabfragen nicht vom OLE DB-Spezifikation definiert. Dieser Parameter ist erforderlich, wenn *QueryType* festgelegt ist, um **AdSchemaProviderSpecific**ist, andernfalls ist er nicht verwendet.  
  
## <a name="remarks"></a>Hinweise  
 Die **OpenSchema** Methodenrückgabe selbsterklärende Informationen über die Datenquelle, z. B. welche Tabellen in der Datenquelle den Spalten in den Tabellen vorhanden sind und die Datentypen unterstützt.  
  
 Die *QueryType* Argument ist eine GUID, der angibt, die Spalten (Schemas) zurückgegeben. OLE DB-Spezifikation hat eine vollständige Liste der Schemas an.  
  
 Die *Kriterien* -Argument begrenzt die Ergebnisse einer Abfrage Schema. *Kriterien* gibt ein Array von Werten, die auftreten, müssen in eine entsprechende Teilmenge der Spalten, Einschränkungsspalten, in der resultierenden aufgerufen **Recordset**.  
  
 Die Konstante **AdSchemaProviderSpecific** wird verwendet, für die *QueryType* Argument, wenn der Anbieter eine eigene nicht standardmäßige Schemaabfragen außerhalb dieser definiert bereits aufgeführt. Wenn diese Konstante verwendet wird, die *SchemaID* Argument ist erforderlich, um die GUID der Schemaabfrage auszuführende übergeben. Wenn *QueryType* festgelegt ist, um **AdSchemaProviderSpecific** jedoch *SchemaID* nicht angegeben wird, führt zu einem Fehler wird.  
  
 Anbieter sind nicht erforderlich, um alle OLE DB-Standardschema Abfragen zu unterstützen. Insbesondere nur **AdSchemaTables**, **AdSchemaColumns**, und **AdSchemaProviderTypes** OLE DB-Spezifikation erforderlich sind. Der Anbieter ist jedoch nicht erforderlich, zur Unterstützung der *Kriterien* Einschränkungen zuvor für diese Abfragen aufgeführt.  
  
> [!NOTE]
>  **Remote Datendienstnutzung** der **OpenSchema** Methode ist nicht verfügbar für eine clientseitige [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt.  
  
> [!NOTE]
>  In Spalten, die eine vier-Byte-Ganzzahl ohne Vorzeichen (DBTYPE UI4) in Visual Basic die **Recordset** zurückgegeben, die aus der **OpenSchema** Methode für die **Verbindung** Objekt kann nicht verglichen Sie mit anderen Variablen werden. Weitere Informationen zu OLE DB-Datentypen finden Sie unter [Datentypen in OLE DB (OLE DB)](http://msdn.microsoft.com/en-us/6039292f-74e0-49b2-b133-17bc117ebf6a) und [Anhang A: Datentypen](http://msdn.microsoft.com/en-us/e3a0533a-2196-4eb0-a31e-92fe9556ada6) in der Microsoft OLE DB Programmer's Reference.  
  
> [!NOTE]
>  **Visual C/C++-Benutzer** clientseitige Cursor nicht verwendet werden soll, Abrufen von "ORDINAL_POSITION" eines Spaltenschemas in ADO gibt eine Variante des Typs VT_R8 in MDAC 2.7, MDAC 2.8 und Windows Data Access Components (Windows DAC) 6.0, während in MDAC verwendet 2.6 ist VT_I4. Programme, die nur Aussehen für eine Variante für MDAC 2.6 geschrieben zurückgegebene Typ VT_I4 eine 0 (null) für jede Ordnungszahl, wenn Sie im MDAC 2.7 MDAC 2.8 und Windows DAC 6.0 ohne Änderung ausgeführt erhalten würden. Diese Änderung wurde vorgenommen, da der Datentyp, den OLE DB-zurückgibt DBTYPE_UI4 ist, und in der signierten VT_I4-Typ ist nicht genügend Platz für alle möglichen Werte ungekürzt möglicherweise stattfinden und wodurch ein Verlust von Daten enthalten.  
  
## <a name="applies-to"></a>Gilt für  
 [Connection-Objekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [OpenSchema-Methode (Beispiel) (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [OpenSchema-Methode (VC++-Beispiel)](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Open-Methode (ADO-Verbindung)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open-Methode (ADO-Datensatz)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open-Methode (ADO-Datenstrom)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Anhang A: Daten und Dienstanbieter](../../../ado/guide/appendixes/appendix-a-providers.md)
