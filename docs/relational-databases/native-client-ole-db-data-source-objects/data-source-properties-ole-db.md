---
title: Datenquelleneigenschaften (OLE DB) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-data-source-objects
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 6e14fefc-4e0b-4847-a833-4cf0abe65d50
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2ff8690685f30c0698ba640b599f9f683d4ea854
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="data-source-properties-ole-db"></a>Datenquelleneigenschaften (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter implementiert Datenquelleneigenschaften wie folgt.  
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|R/W: Lesen/Schreiben; Standardwert: Keiner<br /><br /> Beschreibung: Der Wert von DBPROP_CURRENTCATALOG meldet die aktuelle Datenbank für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-anbietersitzung. Festlegen des Eigenschaftswerts hat dieselbe Auswirkung wie das Festlegen der aktuellen Datenbank mithilfe der [!INCLUDE[tsql](../../includes/tsql-md.md)] verwenden *Datenbank* Anweisung.<br /><br /> Beginnend mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], sofern Sie aufrufen [Sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) , und geben Sie den Datenbanknamen in Kleinbuchstaben, auch wenn die Datenbank ursprünglich, mit einem Namen mit gemischter Groß-/Kleinschreibung erstellt wurde DBPROP_CURRENTCATALOG zurück den Namen in Kleinbuchstaben. In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt DBPROP_CURRENTCATALOG den erwarteten Namen mit Groß- und Kleinbuchstaben zurück.|  
|DBPROP_MULTIPLECONNECTIONS|R/W: Lesen/Schreiben; Standardwert: VARIANT_FALSE<br /><br /> Beschreibung: Wenn während der Verbindung ein Befehl ausgeführt wird, der kein Rowset produziert, oder der ein Rowset produziert, das kein Servercursor ist, und Sie einen anderen Befehl ausführen, wird eine neue Verbindung erstellt, um den neuen Befehl auszuführen, wenn für DBPROP_MULTIPLECONNECTIONS VARIANT_TRUE festgelegt ist.<br /><br /> Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter erstellt keine weitere Verbindung, wenn DBPROP_MULTIPLECONNECTION VARIANT_FALSE festgelegt ist, oder wenn eine Transaktion für die Verbindung aktiv ist. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter gibt DB_E_OBJECTOPEN zurück, wenn DBPROP_MULTIPLECONNECTIONS VARIANT_FALSE lautet, und E_FAIL zurück, wenn eine aktive Transaktion vorhanden ist. Transaktionen und Sperren werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf Verbindungsbasis verwaltet. Wenn eine zweite Verbindung hergestellt wird, nutzen die Befehle auf den anderen Verbindungen Sperren nicht gemeinsam. Um zu gewährleisten, dass ein Befehl einen anderen nicht blockiert, halten Sie Zeilen gesperrt, die von dem anderen Befehl angefordert werden. Dies gilt auch beim Erstellen mehrerer Sitzungen.<br /><br /> Jede Sitzung verfügt über eine separate Verbindung.|  
  
 Im anbieterspezifischen Eigenschaftensatz DBPROPSET_SQLSERVERDATASOURCE der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter definiert die folgenden zusätzlichen Datenquelleneigenschaften.  
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|R/W: Lesen/Schreiben; Standardwert: VARIANT_FALSE<br /><br /> Beschreibung: Um Massenkopiervorgänge aus dem Speicher zu aktivieren, sollte die SSPROP_ENABLEFASTLOAD-Eigenschaft auf VARIANT_TRUE festgelegt werden. Mit dieser Eigenschaft legen Sie für die Datenquelle, die neu erstellte Sitzung lässt den Consumerzugriff auf die [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) Schnittstelle.<br /><br /> Wenn die Eigenschaft auf VARIANT_TRUE festgelegt ist **IRowsetFastLoad** Schnittstelle steht über **IOpenRowset:: OPENROWSET** durch die Anforderung der **IID_IRowsetFastLoad** -Schnittstelle oder durch Festlegen **SSPROP_IRowsetFastLoad** auf VARIANT_TRUE fest.|  
|SSPROP_ENABLEBULKCOPY|R/W: Lesen/Schreiben; Standardwert: VARIANT_FALSE<br /><br /> Beschreibung: Um Massenkopiervorgänge aus Dateien zu aktivieren, sollte die SSPROP_ENABLEBULKCOPY-Eigenschaft auf VARIANT_TRUE festgelegt werden. Wenn diese Eigenschaft für die Datenquelle festgelegt wurde, ist der Consumerzugriff auf die IBCPSession-Schnittstelle auf derselben Ebene verfügbar wie Sessions.<br /><br /> Auch SSPROP_IRowsetFastLoad muss auf VARIANT_TRUE festgelegt werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datenquellenobjekte &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
