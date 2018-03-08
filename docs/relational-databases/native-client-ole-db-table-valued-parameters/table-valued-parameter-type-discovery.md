---
title: Tabellenwertparameter-Typermittlung | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8cb2c68a50c97ca1e51dea778c81c5b9d5c60737
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="table-valued-parameter-type-discovery"></a>Tabellenwertparameter-Typermittlung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Der Consumer – d. h. die Clientanwendung mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter – können den Typ für jeden Befehlsparameter ermitteln, wenn der Befehlstext des OLE DB-Anbieters erhalten hat. Nachdem der Typ des einem Tabellenwertparameter bekannt ist, kann der Consumer die Metadateninformationen für jede einzelne der Tabellenwertparameter-Spalte ermitteln.  
  
 Die Typinformationen für Prozedurparameter wird von ICommandWithParameters:: GetParameterInfo für die meisten Parametertypen unterstützt. Beginnend mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], mit der Einführung von benutzerdefinierten Typen und die **Xml** Datentyp GetParameterInfo-Methode wurde nicht für diesen Zweck ausreichend, da es nicht möglich ist, geben Sie einen benutzerdefinierten Typ war Informationen (Name, Schema und Katalog) über ICommandWithParameters. Eine neue Schnittstelle, ISSCommandWithParameters, wurde definiert, um erweiterte Typinformationen bereitzustellen.  
  
 Für Tabellenwertparameter verwenden Sie auch die ISSCommandWithParameters-Schnittstelle, um ausführliche Informationen zu ermitteln. Der Client ruft ISSCommandWithParameters::GetParameterInfo nach der Vorbereitung der Command-Objekt. Für Tabellenwertparameter-Parameter der *wType* -Element der DBPARAMINFO-Struktur wird vom Anbieter auf DBTYPE_TABLE festgelegt. Die *UlParamSize* -Feld der DBPARAMINFO-Struktur hat einen Wert von ~ 0.  
  
 Der Consumer würde dann weitere Eigenschaften (Tabellenwertparameter Katalogname, Schemaname für Tabellenwertparameter-Typ Tabellenwertparameter Typname, Spaltenreihenfolge und Standardspalten) anzufordern, indem Sie ISSCommandWithParamters:: GetParameterProperties.  
  
 Nachdem der Typname bekannt ist, rufen Sie die einzelne Spalte-Informationen, die der Consumer entweder aufrufen muss IOpenRowset::OpenRowsetor erhalten das DBSCHEMA_TABLE_TYPE_COLUMNS-Rowset durch Festlegen des Tabellenwertparameter-Typnamens als Tabellennamen.  
  
## <a name="see-also"></a>Siehe auch  
 [Table-Valued Parameters &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Verwenden des Table-Valued Parameters &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
