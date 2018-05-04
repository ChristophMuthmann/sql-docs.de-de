---
title: Datenquelleneigenschaften (OLE DB) | Microsoft Docs
description: Datenquelleneigenschaften (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 38d2318750d1db8953648eb13e0454c050a7cb55
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-properties-ole-db"></a>Datenquelleneigenschaften (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Der OLE DB-Treiber für SQL Server implementiert Datenquelleneigenschaften wie folgt aus.  
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|R/W: Lesen/Schreiben; Standardwert: Keiner<br /><br /> Beschreibung: Der Wert von DBPROP_CURRENTCATALOG meldet die aktuelle Datenbank für einen OLE DB-Treiber für SQL Server-Sitzung. Festlegen des Eigenschaftswerts hat dieselbe Auswirkung wie das Festlegen der aktuellen Datenbank mithilfe der [!INCLUDE[tsql](../../../includes/tsql-md.md)] verwenden *Datenbank* Anweisung.<br /><br /> Beginnend mit [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], sofern Sie aufrufen [Sp_defaultdb](../../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) , und geben Sie den Datenbanknamen in Kleinbuchstaben, auch wenn die Datenbank ursprünglich, mit einem Namen mit gemischter Groß-/Kleinschreibung erstellt wurde DBPROP_CURRENTCATALOG zurück den Namen in Kleinbuchstaben. In früheren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gibt DBPROP_CURRENTCATALOG den erwarteten Namen mit Groß- und Kleinbuchstaben zurück.|  
|DBPROP_MULTIPLECONNECTIONS|R/W: Lesen/Schreiben; Standardwert: VARIANT_FALSE<br /><br /> Beschreibung: Wenn während der Verbindung ein Befehl ausgeführt wird, der kein Rowset produziert, oder der ein Rowset produziert, das kein Servercursor ist, und Sie einen anderen Befehl ausführen, wird eine neue Verbindung erstellt, um den neuen Befehl auszuführen, wenn für DBPROP_MULTIPLECONNECTIONS VARIANT_TRUE festgelegt ist.<br /><br /> Eine andere Verbindung wird von der OLE DB-Treiber für SQL Server nicht erstellt werden, wenn DBPROP_MULTIPLECONNECTION VARIANT_FALSE festgelegt ist, oder wenn eine Transaktion für die Verbindung aktiv ist. Der OLE DB-Treiber für SQL Server gibt DB_E_OBJECTOPEN zurück, wenn DBPROP_MULTIPLECONNECTIONS VARIANT_FALSE lautet, und E_FAIL zurück, wenn eine aktive Transaktion vorhanden ist. Transaktionen und Sperren werden von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf Verbindungsbasis verwaltet. Wenn eine zweite Verbindung hergestellt wird, nutzen die Befehle auf den anderen Verbindungen Sperren nicht gemeinsam. Um zu gewährleisten, dass ein Befehl einen anderen nicht blockiert, halten Sie Zeilen gesperrt, die von dem anderen Befehl angefordert werden. Dies gilt auch beim Erstellen mehrerer Sitzungen.<br /><br /> Jede Sitzung verfügt über eine separate Verbindung.|  
  
 Im anbieterspezifischen Eigenschaftensatz DBPROPSET_SQLSERVERDATASOURCE definiert der OLE DB-Treiber für SQL Server die folgenden zusätzlichen Datenquelleneigenschaften.  
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|R/W: Lesen/Schreiben; Standardwert: VARIANT_FALSE<br /><br /> Beschreibung: Um Massenkopiervorgänge aus dem Speicher zu aktivieren, sollte die SSPROP_ENABLEFASTLOAD-Eigenschaft auf VARIANT_TRUE festgelegt werden. Mit dieser Eigenschaft legen Sie für die Datenquelle, die neu erstellte Sitzung lässt den Consumerzugriff auf die [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) Schnittstelle.<br /><br /> Wenn die Eigenschaft auf VARIANT_TRUE festgelegt ist **IRowsetFastLoad** Schnittstelle steht über **IOpenRowset:: OPENROWSET** durch die Anforderung der **IID_IRowsetFastLoad** -Schnittstelle oder durch Festlegen **SSPROP_IRowsetFastLoad** auf VARIANT_TRUE fest.|  
|SSPROP_ENABLEBULKCOPY|R/W: Lesen/Schreiben; Standardwert: VARIANT_FALSE<br /><br /> Beschreibung: Um Massenkopiervorgänge aus Dateien zu aktivieren, sollte die SSPROP_ENABLEBULKCOPY-Eigenschaft auf VARIANT_TRUE festgelegt werden. Wenn diese Eigenschaft für die Datenquelle festgelegt wurde, ist der Consumerzugriff auf die IBCPSession-Schnittstelle auf derselben Ebene verfügbar wie Sessions.<br /><br /> Auch SSPROP_IRowsetFastLoad muss auf VARIANT_TRUE festgelegt werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datenquellenobjekte & #40; OLE DB & #41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
