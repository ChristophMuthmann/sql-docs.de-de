---
title: FILESTREAM-Unterstützung (OLE DB) | Microsoft Docs
description: FILESTREAM-Unterstützung (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efbe3ce15444b0c6556cf3cef0267e99bb55657f
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2018
---
# <a name="filestream-support-ole-db"></a>FILESTREAM-Unterstützung (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Beginnend mit [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] und OLE DB-Treiber für SQL Server, OLE DB unterstützt die verbesserte FILESTREAM-Funktion. Weitere Informationen zu diesem Feature finden Sie unter [FILESTREAM-Unterstützung](../../oledb/features/filestream-support.md). Beispiele finden Sie in [Filestream und OLE DB-](../../oledb/ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Zum Senden und Empfangen von **varbinary(max)** Werte, die größer als 2 GB sind, eine Anwendung verwendet **DBTYPE_IUNKNOWN** in Parameter- und ergebnisbindungen. Für Parameter muss der Anbieter aufrufen IUnknown:: QueryInterface für ISequentialStream und Ergebnisse, die einer ISequentialStream-Schnittstelle zurückgibt.  
  
 Für OLE DB wird die Option ISequentialStream Werte zur Überprüfung gelockert werden. Beim *wType* ist **DBTYPE_IUNKNOWN** in der **DBBINDING** Struktur längenüberprüfung kann entweder durch das weglassen deaktiviert **DBPART_LENGTH** von *DwPart* oder durch Festlegen der Länge der Daten (Offset *ObLength* im Datenpuffer) auf ~ 0. In diesem Fall überprüft der Provider die Länge des Werts nicht und fordert alle Daten an (oder gibt sie zurück), die über den Datenstrom zur Verfügung stehen. Diese Änderung wird auf alle LOB-Typen (Large Object) und auf XML angewendet, allerdings nur, wenn eine Verbindung zu [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]-Servern (oder höher) besteht. Auf diese Weise erhalten Entwickler eine höhere Flexibilität, während sie die Konsistenz und Abwärtskompatibilität für vorhandene Anwendungen und Downlevelserver beibehalten.  
  
 Diese Änderung wirkt sich auf alle Schnittstellen, die Daten, die hauptsächlich IRowset:: GetData ICommand:: Execute und IRowsetFastLoad:: InsertRow übertragen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [OLE DB-Treiber für SQL Server-Programmierung](../../oledb/oledb-driver-for-sql-server-programming.md)  
  
  
