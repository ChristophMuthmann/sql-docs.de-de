---
title: Tabellenwertparameter-Typermittlung | Microsoft Docs
description: Table-Valued Parameter eine Typermittlung mithilfe von OLE DB-Treiber für SQL Server
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
- table-valued parameters, type discovery
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87d6bf89729f27a9b0e75b9abe92891d2dbb8d1f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="table-valued-parameter-type-discovery"></a>Tabellenwertparameter-Typermittlung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Der Consumer – d. h. die Clientanwendung mithilfe der OLE DB-Treiber für SQL Server – können den Typ für jeden Befehlsparameter ermitteln, wenn der Befehlstext des OLE DB-Anbieters erhalten hat. Nachdem der Typ des einem Tabellenwertparameter bekannt ist, kann der Consumer die Metadateninformationen für jede einzelne der Tabellenwertparameter-Spalte ermitteln.  
  
 Die Typinformationen für Prozedurparameter wird von ICommandWithParameters:: GetParameterInfo für die meisten Parametertypen unterstützt. Beginnend mit [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], mit der Einführung von benutzerdefinierten Typen und die **Xml** Datentyp GetParameterInfo-Methode wurde nicht für diesen Zweck ausreichend, da es nicht möglich ist, geben Sie einen benutzerdefinierten Typ war Informationen (Name, Schema und Katalog) über ICommandWithParameters. Eine neue Schnittstelle, ISSCommandWithParameters, wurde definiert, um erweiterte Typinformationen bereitzustellen.  
  
 Für Tabellenwertparameter verwenden Sie auch die ISSCommandWithParameters-Schnittstelle, um ausführliche Informationen zu ermitteln. Der Client ruft ISSCommandWithParameters::GetParameterInfo nach der Vorbereitung der Command-Objekt. Für Tabellenwertparameter der *wType* -Element der DBPARAMINFO-Struktur wird vom Anbieter auf DBTYPE_TABLE festgelegt. Die *UlParamSize* -Feld der DBPARAMINFO-Struktur hat einen Wert von ~ 0.  
  
 Der Consumer würde dann weitere Eigenschaften (Tabellenwertparameter Katalogname, Schemaname für Tabellenwertparameter-Typ Tabellenwertparameter Typname, Spaltenreihenfolge und Standardspalten) anzufordern, indem Sie ISSCommandWithParamters:: GetParameterProperties.  
  
 Nachdem der Typname bekannt ist, rufen Sie die einzelne Spalte-Informationen, die der Consumer entweder aufrufen muss IOpenRowset::OpenRowsetor erhalten das DBSCHEMA_TABLE_TYPE_COLUMNS-Rowset durch Festlegen des Tabellenwertparameter-Typnamens als Tabellennamen.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellenwertparameter &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Verwenden des Table-Valued Parameters & #40; OLE DB & #41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
