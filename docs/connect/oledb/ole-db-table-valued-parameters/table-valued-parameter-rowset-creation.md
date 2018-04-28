---
title: Tabellenwertparameter-Rowseterstellung | Microsoft Docs
description: Statische und dynamische Erstellen von Tabellenwertparameter-Rowsets
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fef8896ce93a3ce8250b9640f60f778ea2de4d13
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="table-valued-parameter-rowset-creation"></a>Tabellenwertparameter-Rowseterstellung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Consumer können zwar ein beliebiges Rowsetobjekt für Tabellenwertparameter bereitstellen, typische Rowsetobjekte werden jedoch mit Back-End-Datenspeichern implementiert und bieten somit nur eine eingeschränkte Leistung. Aus diesem Grund ermöglicht der OLE DB-Treiber für SQL Server-Consumer ein spezielles Rowsetobjekt auf speicherinternen Daten zu erstellen. Dieses spezielle, in-Memory Rowsetobjekt ist ein neues COM-Objekt, das ein Tabellenwertparameter-Rowset bezeichnet. Es bietet ähnliche Funktionen wie Parametersätze.  
  
 Tabellenwertparameter-Rowsetobjekte werden explizit vom Consumer für Eingabeparameter durch mehrere Schnittstellen auf Sitzungsebene erstellt. Es gibt eine Instanz des einem Tabellenwertparameter-Rowsetobjekts pro Tabellenwertparameter. Der Consumer kann die Tabellenwertparameter-Rowsetobjekte entweder durch Bereitstellen der Metadateninformationen, die bereits bekannt sind (statisches Szenario), oder durch Ermitteln über Anbieterschnittstellen (dynamisches Szenario) erstellen. In den folgenden Abschnitten werden diese beiden Szenarien beschrieben.  
  
## <a name="static-scenario"></a>Statisches Szenario  
 Wenn die Typinformationen bekannt ist, verwendet der Consumer ITableDefinitionWithConstraints::CreateTableWithConstraints ein Tabellenwertparameter-Rowsetobjekt instanziieren, das einem Tabellenwertparameter entspricht.  
  
 Die *Guid* Feld (*pTableID* Parameter) enthält die besondere GUID (CLSID_ROWSET_TVP). Die *PwszName* Member enthält den Namen des Tabellenwertparameter-Typs, die der Consumer instanziieren möchte. Die *eKind* Feld wird auf DBKIND_GUID_NAME gesetzt. Dieser Name ist erforderlich, wenn die Anweisung ad-hoc-SQL ist; der Name ist optional, wenn es sich um einen Aufruf einer Prozedur ist.  
  
 Bei der Aggregation übergibt der Consumer die *pUnkOuter* Parameter controlling IUnknown.  
  
 Die Tabellenwertparameter-Rowset-Objekteigenschaften sind schreibgeschützt, sodass der Consumer wird nicht zum Festlegen von Eigenschaften im *RgPropertySets*.  
  
 Für die *RgPropertySets* Mitglied jeder DBCOLUMNDESC-Struktur der Consumer kann zusätzliche Eigenschaften für jede Spalte angeben. Diese Eigenschaften gehören zum DBPROPSET_SQLSERVERCOLUMN-Eigenschaftensatz. Sie ermöglichen es Ihnen, berechnete und standardmäßige Einstellungen für jede Spalte anzugeben. Sie unterstützen auch vorhandene Spalteneigenschaften, z. B. NULL-Zulässigkeit und Identität.  
  
 Um die entsprechenden Informationen aus einem Tabellenwertparameter-Rowsetobjekt abzurufen, verwendet der Consumer IRowsetInfo:: GetProperties.  
  
 Zum Abrufen von Informationen über das Null-Zeichen, eindeutig ist, berechnet, und Aktualisieren des Status der einzelnen Spalten, kann der Consumer IColumnsRowset:: GetColumnsRowset oder IColumnsInfo:: GetColumnInfo verwenden. Diese Methoden stellen ausführliche Informationen über jede Tabellenwertparameter-Rowsetspalte bereit.  
  
 Der Consumer gibt den Typ jeder Spalte des Tabellenwertparameters an. Es ähnelt der Angabe von Spalten beim Erstellen der Tabelle in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Der Consumer erhält ein Tabellenwertparameter-Rowsetobjekt aus der OLE DB-Treiber für SQL Server über die *PpRowset* output-Parameter.  
  
## <a name="dynamic-scenario"></a>Dynamisches Szenario  
 Wenn der Consumer keine Typinformationen hat, sollte IOpenRowset:: OPENROWSET zum Instanziieren von Tabellenwertparameter-Rowsetobjekten verwendet werden. Der Consumer muss dem Anbieter somit nur den Typnamen zur Verfügung stellen.  
  
 In diesem Szenario erhält der Anbieter im Namen des Consumers Typinformationen zu einem Tabellenwertparameter-Rowsetobjekt vom Server.  
  
 Die *pTableID* und *pUnkOuter* Parameter wie beim statischen Szenario festgelegt werden soll. Der OLE DB-Treiber für SQL Server klicken Sie dann die Typinformationen (Spalteninformationen und Einschränkungen) vom Server abgerufen, und ein Tabellenwertparameter-Rowsetobjekt durch Zurückgeben der *PpRowset* Parameter. Dieser Vorgang erfordert Kommunikation mit dem Server, und daher nicht so gut beim statischen Szenario. Das dynamische Szenario funktioniert nur mit parametrisierten Prozeduraufrufen.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellenwertparameter &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Verwenden des Table-Valued Parameters & #40; OLE DB & #41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
