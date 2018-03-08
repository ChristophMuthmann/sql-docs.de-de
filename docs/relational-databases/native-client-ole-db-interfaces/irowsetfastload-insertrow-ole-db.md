---
title: 'IRowsetFastLoad:: InsertRow (OLE DB) | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-interfaces
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords: InsertRow method
ms.assetid: 594d3461-34d2-41e7-8ad4-bd2753601ab6
caps.latest.revision: "37"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f3b7e73fa767ef0d07f8e43553bdaff5c7365ea4
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="irowsetfastloadinsertrow-ole-db"></a>IRowsetFastLoad::InsertRow (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Fügt dem Rowset für das Massenkopieren eine Zeile hinzu. Beispiele finden Sie in [Bulk Daten mithilfe von IRowsetFastLoad &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) und [Senden von BLOB-Daten mit SQL SERVER mithilfe von IROWSETFASTLOAD und ISEQUENTIALSTREAM &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HRESULT InsertRow(  
      HACCESSOR hAccessor,  
      void* pData);  
```  
  
## <a name="arguments"></a>Argumente  
 *hAccessor*[in]  
 Das Handle des Accessors, der die Zeilendaten für das Massenkopieren definiert. Der Accessor, auf den verwiesen wird, ist ein Zeilenaccessor, der den consumer-eigenen Speicher bindet, in dem sich die Datenwerte befinden.  
  
 *pData*[in]  
 Ein Zeiger zum consumer-eigenen Speicher, in dem sich die Datenwerte befinden. Weitere Informationen finden Sie unter [DBBINDING-Strukturen](http://go.microsoft.com/fwlink/?LinkId=65955).  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 S_OK  
 Die Methode wurde erfolgreich ausgeführt. Alle gebundenen Statuswerte für alle Spalten weisen den Wert DBSTATUS_S_OK oder DBSTATUS_S_NULL auf.  
  
 E_FAIL  
 Ein Fehler ist aufgetreten. Fehlerinformationen sind über die Fehlerschnittstellen des Rowsets verfügbar.  
  
 E_INVALIDARG  
 Das *pData* -Argument wurde auf einen NULL-Zeiger festgelegt.  
  
 E_OUTOFMEMORY  
 SQLNCLI11 konnte keinen ausreichenden Arbeitsspeicher zum Ausführen der Anforderung zuordnen.  
  
 E_UNEXPECTED  
 Die Methode wurde aufgerufen, auf eine zuvor durch für ungültig erklärt Rowset für das Massenkopieren der [IRowsetFastLoad:: Commit](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md) Methode.  
  
 DB_E_BADACCESSORHANDLE  
 Das vom Consumer bereitgestellte *hAccessor* -Argument ist ungültig.  
  
 DB_E_BADACCESSORTYPE  
 Der angegebene Accessor war kein Zeilenaccessor oder hat keinen consumer-eigenen Arbeitsspeicher angegeben.  
  
## <a name="remarks"></a>Hinweise  
 Fehler beim Konvertieren von Consumer Daten in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datentyp für eine Spalte bewirkt, dass eine E_FAIL-Rückgabe aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter. Daten übertragen werden können, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für ein beliebiges **InsertRow** Methode oder nur **Commit** Methode. lDie Consumer-Anwendung kann die **InsertRow** -Methode mehrere Male mit fehlerhaften Daten aufrufen, bevor eine Meldung eintrifft, dass die Daten nicht korrekt sind. Die **Commit** -Methode gewährleistet, dass alle Daten ordnungsgemäß vom Consumer angegeben werden. Der Consumer kann die **Commit** -Methode gegebenenfalls verwenden, um die Daten zu überprüfen.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] massenkopierten Rowsets Native Client OLE DB-Anbieter weisen nur Schreibzugriff. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter macht keine Methoden, die Abfragen von Consumern hinsichtlich des Rowsets. Um die Verarbeitung zu beenden, kann der Consumer seine Verweise auf Freigeben der [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) -Schnittstelle ohne die **Commit** Methode. Es gibt keine Möglichkeit, auf von Consumern eingefügte Zeilen im Rowset zuzugreifen und deren Werte zu ändern oder diese einzeln aus dem Rowset zu entfernen.  
  
 Massenkopierte Zeilen werden auf dem Server für formatiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Das Zeilenformat entspricht den Optionen, die eventuell für die Verbindung oder die Sitzung festgelegt wurden, wie z. B. ANSI_PADDING. Diese Option auf festgelegt ist, wird standardmäßig für jede Verbindung, die über die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter.  
  
## <a name="see-also"></a>Siehe auch  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
