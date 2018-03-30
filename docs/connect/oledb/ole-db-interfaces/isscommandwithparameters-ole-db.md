---
title: ISSCommandWithParameters (OLE DB) | Microsoft Docs
description: ISSCommandWithParameters (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fd350eb8c63a95d0ba64950be2ab689696fef0e5
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ISSCommandWithParameters** Schnittstelle verfügbar macht, Unterstützung für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML und benutzerdefinierte Typen (UDT). Es ist eine optionale Schnittstelle, die von der OLE DB-Kernschnittstelle erbt **ICommandWithParameters**. Zusätzlich zu den drei von geerbten Methoden **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**, und **SetParameterInfo**; **ISSCommandWithParameters** bietet zwei neue Methoden, mit dem Server-spezifische Datentypen zu behandeln sind.  
  
> [!NOTE]  
>  Die **ISSCommandWithParameters** Schnittstelle kann verwendet werden, wenn Dienstkomponenten verwendet werden, aber die Dienstkomponenten nicht diese Schnittstelle verwenden.  
  
|Methode|Description|  
|------------|-----------------|  
|[Isscommandwithparameters:: Getparameterproperties &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|Gibt eine **SSPARAMPROPS** -Eigenschaftssatzstruktur im Array für jeden UDT- oder XML-Parameter zurück, der dem Befehl übergeben wurde. Für andere Parametertypen wird hingegen keine Struktur zurückgegeben.|  
|[Isscommandwithparameters:: SetParameterProperties &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|Legt die Parametereigenschaften auf einer Einzelparameterbasis nach Ordnungszahl fest oder legt Massenparametereigenschaften durch Angabe eines Arrays von **SSPARAMPROPS** -Strukturen fest.|  
  
## <a name="see-also"></a>Siehe auch  
 [Schnittstellen &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [Verwenden von XML-Datentypen](../../oledb/features/using-xml-data-types.md)   
 [Verwenden von benutzerdefinierten Typen](../../oledb/features/using-user-defined-types.md)  
  
  
