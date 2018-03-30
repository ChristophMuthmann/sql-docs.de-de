---
title: 'IRowsetFastLoad:: Commit (OLE DB) | Microsoft Docs'
description: IRowsetFastLoad::Commit (OLE DB)
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
- IRowsetFastLoad::Commit (OLE DB)
apitype: COM
helpviewer_keywords:
- Commit method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 93e3b1a7bf97da890e77e3c51d6c1f5bc6f67ee0
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Markiert das Ende eines Batches eingefügter Zeilen und schreibt die Zeilen in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabelle. Beispiele finden Sie in [Bulk Daten mithilfe von IRowsetFastLoad &#40;OLE DB-&#41; ](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) und [Senden von BLOB-Daten, SQL SERVER mithilfe von IROWSETFASTLOAD und ISEQUENTIALSTREAM &#40;OLE DB-&#41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HRESULT Commit(  
      BOOL fDone);  
```  
  
## <a name="arguments"></a>Argumente  
 *fDone*[in]  
 Wenn FALSE angegeben wird, behält das Rowset seine Gültigkeit und kann vom Consumer zum Einfügen zusätzlicher Zeilen verwendet werden. Wird TRUE angegeben, dann verliert das Rowset seine Gültigkeit, und der Consumer kann keine weiteren Einfügungen vornehmen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 S_OK  
 Die Methode wurde erfolgreich ausgeführt, und alle eingefügten Daten wurden in die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Tabelle geschrieben.  
  
 E_FAIL  
 Es ist ein anbieterspezifischer Fehler aufgetreten. Rufen Sie Fehlerinformationen für den betreffenden Fehlertext vom Anbieter ab.  
  
 E_UNEXPECTED  
 Die Methode wurde aufgerufen, auf eine zuvor durch für ungültig erklärt Rowset für das Massenkopieren der **IRowsetFastLoad:: Commit** Methode.  
  
## <a name="remarks"></a>Hinweise  
 Ein OLE DB-Treiber für SQL Server Rowset für das Massenkopieren verhält sich wie ein Rowset verzögerten Updatemodus. Wie der Benutzer Zeilendaten über das Rowset einfügt, werden eingefügte Zeilen in derselben Weise wie ausstehende einfügungen in ein Rowset unterstützender behandelt **IRowsetUpdate**.  
  
 Der Consumer muss aufgerufen werden der **Commit** Methode auf das Rowset für das Massenkopieren schreiben eingefügte Zeilen an die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabelle auf die gleiche Weise wie die **IRowsetUpdate:: Update** Methode dient zum Absenden ausstehende Zeilen an eine SQL Server-Instanz.  
  
 Wenn der Consumer seinen Verweis auf das Rowset für das Massenkopieren ohne Aufruf frei der **Commit** -Methode, alle eingefügten Zeilen, die nicht zuvor geschrieben verloren.  
  
 Der Consumer kann eingefügten Zeilen als batch durch Aufrufen der **Commit** Methode mit dem *fDone* -Argument auf "false" festgelegt. Wenn *fDone*ist auf "true" festgelegt, wird das Rowset ungültig. Ein Rowset für das ungültige Massenkopieren unterstützt nur die **ISupportErrorInfo** Schnittstelle und **IRowsetFastLoad:: Release** Methode.  
  
## <a name="see-also"></a>Siehe auch  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
