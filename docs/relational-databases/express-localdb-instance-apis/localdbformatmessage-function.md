---
title: Funktion "localdbformatmessage" | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- LocalDBFormatMessage
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 31b3152a-94cf-4f75-a31b-296d7dd16dbe
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: df02d647b06b45d2de772ff11737dbba9504a184
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="localdbformatmessage-function"></a>LocalDBFormatMessage-Funktion
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Gibt die lokalisierte Textbeschreibung für den angegebenen SQL Server Express LocalDB-Fehler zurück.  
  
 **Headerdatei:** sqlncli.h  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT LocalDBFormatMessage(  
           HRESULT hrLocalDB,  
           DWORD dwFlags,   
           DWORD dwLanguageId,   
           LPWSTR wszMessage,   
           LPDWORD lpcchMessage   
);  
```  
  
## <a name="parameters"></a>Parameter  
 *hrLocalDB*  
 [Eingabe] Der LocalDB-Fehlercode.  
  
 *dwFlags*  
 [Eingabe] Die Flags, die das Verhalten dieser Funktion angeben.  
  
 Verfügbare Flags:  
  
 LOCALDB_TRUNCATE_ERR_MESSAGE  
 Wenn der Eingabepuffer zu kurz ist, wird die Fehlermeldung abgeschnitten, damit sie in den Puffer passt.  
  
 *dwLanguageId*  
 [Eingabe] Die gewünschte Sprache (LANGID) oder 0, falls die Win32 FormatMessage-Sprachreihenfolge verwendet wird.  
  
 *wszMessage*  
 [Ausgabe] Der Puffer zum Speichern der LocalDB-Fehlermeldung.  
  
 *lpcchMessage*  
 [Eingabe/Ausgabe] Bei Eingabe enthält dieses Objekt die Größe des *wszMessage* -Puffers in Zeichen. Wenn der angegebene Puffer zu klein ist, enthält dieses Objekt bei Ausgabe die erforderliche Puffergröße in Zeichen, einschließlich sämtlicher nachfolgender Nullen. Wenn die Funktion erfolgreich ausgeführt wird, enthält dieses Objekt die Anzahl der Zeichen in der Meldung, ohne nachfolgende Nullen.  
  
## <a name="returns"></a>Rückgabewert  
 S_OK  
 Die Funktion wurde erfolgreich ausgeführt.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB ist nicht auf dem Computer installiert.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Mindestens ein angegebener Eingabeparameter ist ungültig.  
  
 [LOCALDB_ERROR_UNKNOWN_ERROR_CODE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-error-code.md)  
 Die angeforderte Meldung ist nicht vorhanden.  
  
 [LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-language-id.md)  
 Die Meldung ist in der angeforderten Sprache nicht verfügbar.  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../../relational-databases/express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 Der Eingabepuffer *wszMessage* ist zu kurz. Abschneiden wird nicht angefordert.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Ein unerwarteter Fehler ist aufgetreten. Weitere Informationen finden Sie im Ereignisprotokoll.  
  
## <a name="remarks"></a>Hinweise  
 Ein Codebeispiel, in dem die LocalDB-API verwendet wird, finden Sie unter [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Express LocalDB-Header und -Versionsinformationen](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
