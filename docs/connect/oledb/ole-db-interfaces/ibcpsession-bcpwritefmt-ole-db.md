---
title: Bcpwritefmt (OLE DB) | Microsoft Docs
description: 'Mithilfe von ibcpsession:: Bcpwritefmt so speichern Sie die Formatdateien in XML- oder Text-Format (OLE DB)'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
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
- IBCPSession::BCPWriteFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPWriteFmt method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: f193222038da47cdc1cc88cb3861bd739790f6d3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ibcpsessionbcpwritefmt-ole-db"></a>IBCPSession::BCPWriteFmt (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Schreibt für jede Spalte Formatinformationen in die Formatdatei.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HRESULT BCPWriteFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Hinweise  
 Die Formatdatei gibt das Datenformat einer durch Massenkopieren erstellten Datendatei an. Aufrufe von der [ibcpsession:: BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) und [ibcpsession:: BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) Methoden definieren Sie das Format der Datendatei. Die Methode **BCPWriteFmt** speichert diese Definition in der im Argument pwszFormatFile angegebenen Datei.  
  
 Die **BCPWriteFmt** -Methode kann die Formatdateien in XML- oder Textformat speichern. Dies muss angegeben werden, mithilfe der BCP_OPTION_XML-Steueroption der [ibcpsession:: Bcpcontrol](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) Methode.  
  
 Um eine gespeicherte Formatdatei zu laden, verwenden die [ibcpsession:: Bcpreadfmt](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md) Methode.  
  
## <a name="arguments"></a>Argumente  
 *pwszFormatFile*[in]  
 Pfad und Dateiname der Datei, die die Formatwerte für die Datendatei enthält.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 S_OK  
 Die Methode wurde erfolgreich ausgeführt.  
  
 E_FAIL  
 Ein anbieterspezifischer Fehler aufgetreten. Ausführliche Informationen erhalten Sie die [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) Schnittstelle.  
  
 E_OUTOFMEMORY  
 Fehler aufgrund nicht genügenden Arbeitsspeichers  
  
 E_UNEXPECTED  
 Die Methode wurde unerwartet aufgerufen. Z. B. die [ibcpsession:: BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) Methode vor dem Aufrufen dieser Methode nicht aufgerufen wurde.  
  
## <a name="see-also"></a>Siehe auch  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Durchführen von Massenkopiervorgängen](../../oledb/features/performing-bulk-copy-operations.md) 
  
  
