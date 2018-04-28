---
title: 'Ibcpsession:: Bcpreadfmt (OLE DB) | Microsoft Docs'
description: 'Mithilfe von ibcpsession:: Bcpreadfmt zum Lesen von Daten aus einer Formatdatei (OLE DB)'
ms.custom: ''
ms.date: 03/26/2018
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
- IBCPSession::BCPReadFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPReadFmt method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b4fa9b54be41682c266bb9583473f79dda2efb38
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>'IBCPSession::BCPReadFmt' (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Liest für jede Spalte Formatinformationen aus der Formatdatei.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HRESULT BCPReadFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Hinweise  
 Die **BCPReadFmt** -Methode wird verwendet, um Daten aus einer Formatdatei zu lesen, die das Format der Daten in der Datendatei angibt. Diese Methode kann die korrekte Version der Formatdatei ermitteln. Sie kann automatisch erkennen, ob die Formatdatei im XML-Format oder dem alten Textformat abgefasst ist und sich entsprechend verhält. Die Versionen der Format-Dateien, die von der OLE DB-Treiber für SQL Server-BCP unterstützt werden Version 6.0 oder höher.  
  
 Nach der **BCPReadFmt** -Methode die Formatwerte, nimmt Sie geeignete Aufrufe an die [ibcpsession:: BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) und [ibcpsession:: BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) Methoden. Der Benutzer muss eine Formatdatei nicht analysieren, um diese Aufrufe zu tätigen.  
  
 Um eine Formatdatei zu speichern, rufen die [Bcpwritefmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md) Methode. Aufrufe der **BCPReadFmt** -Methode können auf gespeicherte Formate verweisen. Alternativ dazu kann das Hilfsprogramm zum Massenkopieren (**bcp**) benutzerdefinierte Datenformate in Dateien speichern, auf die mit der **BCPReadFmt** -Methode verwiesen werden kann.  
  
 Die **BCP_OPTION_DELAYREADFMT** Wert, der die *eOption* Parameter [ibcpsession:: Bcpcontrol](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) ändert das Verhalten von ibcpsession:: Bcpreadfmt.  
  
## <a name="arguments"></a>Argumente  
 *pwszFormatFile*[in]  
 Pfad und Dateiname der Datei, die die Formatwerte für die Datendatei enthält.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 S_OK  
 Die Methode wurde erfolgreich ausgeführt.  
  
 E_FAIL  
 Ein anbieterspezifischer Fehler aufgetreten ist, ausführliche Informationen erhalten Sie über die [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) Schnittstelle.  
  
 E_OUTOFMEMORY  
 Fehler aufgrund von nicht genügend Arbeitsspeicher.  
  
 E_UNEXPECTED  
 Die Methode wurde unerwartet aufgerufen. Z. B. die [ibcpsession:: BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) Methode vor dem Aufrufen dieser Methode nicht aufgerufen wurde.  
  
## <a name="see-also"></a>Siehe auch  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Durchführen von Massenkopiervorgängen](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
