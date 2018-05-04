---
title: FILESTREAM-Unterstützung (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: native-client-ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad770eec958d612578dcf53971443679ed3a1fd3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="filestream-support-ole-db"></a>FILESTREAM-Unterstützung (OLE DB)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Beginnend mit [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 unterstützt OLE DB die verbesserte FILESTREAM-Funktion. Weitere Informationen zu diesem Feature finden Sie unter [FILESTREAM-Unterstützung](../../../relational-databases/native-client/features/filestream-support.md). Beispiele finden Sie in [Filestream und OLE DB-](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Zum Senden und Empfangen von **varbinary(max)** Werte, die größer als 2 GB sind, eine Anwendung verwendet **DBTYPE_IUNKNOWN** in Parameter- und ergebnisbindungen. Für Parameter muss der Anbieter aufrufen IUnknown:: QueryInterface für ISequentialStream und Ergebnisse, die einer ISequentialStream-Schnittstelle zurückgibt.  
  
 Für OLE DB wird die Option ISequentialStream Werte zur Überprüfung gelockert werden. Beim *wType* ist **DBTYPE_IUNKNOWN** in der **DBBINDING** Struktur längenüberprüfung kann entweder durch das weglassen deaktiviert **DBPART_LENGTH** von *DwPart* oder durch Festlegen der Länge der Daten (Offset *ObLength* im Datenpuffer) auf ~ 0. In diesem Fall überprüft der Provider die Länge des Werts nicht und fordert alle Daten an (oder gibt sie zurück), die über den Datenstrom zur Verfügung stehen. Diese Änderung wird auf alle LOB-Typen (Large Object) und auf XML angewendet, allerdings nur, wenn eine Verbindung zu [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]-Servern (oder höher) besteht. Auf diese Weise erhalten Entwickler eine höhere Flexibilität, während sie die Konsistenz und Abwärtskompatibilität für vorhandene Anwendungen und Downlevelserver beibehalten.  
  
 Diese Änderung wirkt sich auf alle Schnittstellen, die Daten, die hauptsächlich IRowset:: GetData ICommand:: Execute und IRowsetFastLoad:: InsertRow übertragen.  
  
## <a name="see-also"></a>Siehe auch  
 [Programmierung für SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
