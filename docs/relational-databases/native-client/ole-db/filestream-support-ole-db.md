---
title: "FILESTREAM-Unterstützung (OLE DB) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2755343d0544a59acb19da4e54cc97b1c197ad2d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="filestream-support-ole-db"></a>FILESTREAM-Unterstützung (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Beginnend mit [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 unterstützt OLE DB die verbesserte FILESTREAM-Funktion. Weitere Informationen zu diesem Feature finden Sie unter [FILESTREAM-Unterstützung](../../../relational-databases/native-client/features/filestream-support.md). Beispiele finden Sie in [Filestream und OLE DB-](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Zum Senden und Empfangen von **varbinary(max)** Werte, die größer als 2 GB sind, eine Anwendung verwendet **DBTYPE_IUNKNOWN** in Parameter- und ergebnisbindungen. Für Parameter muss der Anbieter aufrufen IUnknown:: QueryInterface für ISequentialStream und Ergebnisse, die einer ISequentialStream-Schnittstelle zurückgibt.  
  
 Für OLE DB wird die Option ISequentialStream Werte zur Überprüfung gelockert werden. Beim *wType* ist **DBTYPE_IUNKNOWN** in der **DBBINDING** Struktur längenüberprüfung kann entweder durch das weglassen deaktiviert **DBPART_LENGTH** von *DwPart* oder durch Festlegen der Länge der Daten (Offset *ObLength* im Datenpuffer) auf ~ 0. In diesem Fall überprüft der Provider die Länge des Werts nicht und fordert alle Daten an (oder gibt sie zurück), die über den Datenstrom zur Verfügung stehen. Diese Änderung wird auf alle LOB-Typen (Large Object) und auf XML angewendet, allerdings nur, wenn eine Verbindung zu [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]-Servern (oder höher) besteht. Auf diese Weise erhalten Entwickler eine höhere Flexibilität, während sie die Konsistenz und Abwärtskompatibilität für vorhandene Anwendungen und Downlevelserver beibehalten.  
  
 Diese Änderung wirkt sich auf alle Schnittstellen, die Daten, die hauptsächlich IRowset:: GetData ICommand:: Execute und IRowsetFastLoad:: InsertRow übertragen.  
  
## <a name="see-also"></a>Siehe auch  
 [Programmierung für SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
