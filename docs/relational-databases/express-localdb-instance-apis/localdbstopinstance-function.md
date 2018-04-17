---
title: LocalDBStopInstance-Funktion | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: localdb
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- LocalDBStopInstance
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 4bd73187-0aac-4f03-ac54-2b78e41917e5
caps.latest.revision: 17
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e544c02117f42a4d5c2938ef74899cbee41f5f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="localdbstopinstance-function"></a>LocalDBStopInstance-Funktion
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Beendet die angegebene SQL Server Express LocalDB-Instanz.  
  
 **Headerdatei:** sqlncli.h  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT LocalDBStopInstance(  
           PCWSTR pInstanceName,  
           DWORD dwFlags,   
           ULONG ulTimeout   
);  
```  
  
## <a name="parameters"></a>Parameter  
 *pInstanceName*  
 [Eingabe] Der Name der LocalDB-Instanz, die angehalten werden soll.  
  
 *dwFlags*  
 [Eingabe] Ein Flagwert oder eine Kombination der Flagwerte, die den Weg zum Beenden der Instanz angibt.  
  
 Verfügbare Flags:  
  
 LOCALDB_SHUTDOWN_KILL_PROCESS  
 Sofortiges Herunterfahren unter Verwendung des Betriebssystembefehls zum Beenden von Prozessen.  
  
 LOCALDB_SHUTDOWN_WITH_NOWAIT  
 Herunterfahren mithilfe des Transact-SQL-Befehls der WITH NOWAIT-Option.  
  
 Wenn keines der Flags festgelegt ist, wird die LocalDB-Instanz mithilfe des Transact-SQL-Befehls SHUTDOWN heruntergefahren. Wenn beide Flags festgelegt sind, hat das LOCALDB_SHUTDOWN_KILL_PROCESS-Flag Vorrang.  
  
 *ulTimeout*  
 [Eingabe] Die Wartezeit in Sekunden, bis dieser Vorgang abgeschlossen ist. Wenn dieser Wert 0 beträgt, kehrt diese Funktion sofort zurück, ohne zu warten, bis die LocalDB-Instanz beendet ist.  
  
## <a name="returns"></a>Rückgabewert  
 S_OK  
 Die Funktion wurde erfolgreich ausgeführt.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB ist nicht auf dem Computer installiert.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Mindestens ein angegebener Eingabeparameter ist ungültig.  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 Der angegebene Instanzname ist ungültig.  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-instance.md)  
 Die Instanz ist nicht vorhanden.  
  
 [LOCALDB_ERROR_WAIT_TIMEOUT](../../relational-databases/express-localdb-error-messages/localdb-error-wait-timeout.md)  
 Beim versuchten Abrufen der Synchronisierungssperren ist ein Timeout aufgetreten.  
  
 [LOCALDB_ERROR_INSTANCE_STOP_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-instance-stop-failed.md)  
 Der Beendigungsvorgang wurde nicht innerhalb der angegebenen Zeit abgeschlossen.  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../../relational-databases/express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 Der Pfad, unter dem die Instanz gespeichert werden soll, ist länger als MAX_PATH.  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 Ein Benutzerprofilordner kann nicht abgerufen werden.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 Auf einen Instanzordner kann nicht zugegriffen werden.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 Auf eine Instanzregistrierung kann nicht zugegriffen werden.  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../../relational-databases/express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 Eine Instanzkonfiguration ist beschädigt.  
  
 [LOCALDB_ERROR_CALLER_IS_NOT_OWNER](../../relational-databases/express-localdb-error-messages/localdb-error-caller-is-not-owner.md)  
 API-Aufrufer ist kein Eigentümer der LocalDB-Instanz.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Ein unerwarteter Fehler ist aufgetreten. Weitere Informationen finden Sie im Ereignisprotokoll.  
  
## <a name="remarks"></a>Hinweise  
 Ein Codebeispiel, in dem die LocalDB-API verwendet wird, finden Sie unter [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Express LocalDB-Header und -Versionsinformationen](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
