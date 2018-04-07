---
title: Ändern von Kennwörtern programmgesteuert | Microsoft Docs
description: Ändern von Kennwörtern programmgesteuert mithilfe von OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], password expiration
- OLE DB Driver for SQL Server, passwords
- passwords [SQL Server], expiration
- MSOLEDBSQL, password expiration
- expiration [OLE DB Driver for SQL Server]
- passwords [SQL Server], modifying
- expired passwords [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, password expiration
- modifying passwords
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3a0f5c0b835836c8dc51f824d2e62bef83cff511
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="changing-passwords-programmatically"></a>Programmgesteuertes Ändern von Kennwörtern
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] konnte nur ein Administrator ein abgelaufenes Kennwort eines Benutzers zurücksetzen. Beginnend mit [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], OLE DB-Treiber für SQL Server unterstützt, die von abgelaufenen Kennwörtern programmgesteuert über OLE DB-Treiber und über Änderungen an der **SQL Server-Anmeldung** Dialogfelder.  
  
> [!NOTE]  
>  Fordern Sie, wenn möglich, Benutzer dazu auf, ihre Anmeldeinformationen zur Laufzeit einzugeben, um zu vermeiden, diese Informationen in einem persistenten Format speichern zu müssen. Wenn Sie ihre Anmeldeinformationen persistent speichern müssen, verschlüsseln Sie sie mithilfe der [Win32 Crypto-API](http://go.microsoft.com/fwlink/?LinkId=64532). Weitere Informationen zur Verwendung von Kennwörtern finden Sie unter [Strong Passwords](../../../relational-databases/security/strong-passwords.md).  
  
## <a name="sql-server-login-error-codes"></a>Fehlercodes bei der SQL Server-Anmeldung  
 Wenn eine Verbindung aufgrund von Authentifizierungsproblemen nicht hergestellt werden kann, wird für die Anwendung einer der folgenden SQL Server-Fehlercodes bereitgestellt, um Diagnose und Wiederherstellung zu erleichtern.  
  
|SQL Server-Fehlercode|Fehlermeldung|  
|---------------------------|-------------------|  
|15113|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Fehler bei der Kennwortüberprüfung. Das Konto ist gesperrt.|  
|18463|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Fehler bei der Kennwortänderung. Das Kennwort kann zurzeit nicht verwendet werden.|  
|18464|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Fehler bei der Kennwortänderung. Das Kennwort erfüllt nicht richtlinienanforderungen ist zu kurz.|  
|18465|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Fehler bei der Kennwortänderung. Das Kennwort erfüllt nicht richtlinienanforderungen, weil er zu lang ist.|  
|18466|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Fehler bei der Kennwortänderung. Das Kennwort ist nicht komplex genug und erfüllt daher nicht die Anforderungen der Windows-Richtlinie.|  
|18467|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Fehler bei der Kennwortänderung. Das Kennwort erfüllt nicht die Anforderungen der Kennwortfilter-DLL.|  
|18468|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Fehler bei der Kennwortänderung. Unerwarteter Fehler während der Kennwortüberprüfung.|  
|18487|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Das Kennwort des Kontos ist abgelaufen.|  
|18488|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Das Kennwort des Kontos muss geändert werden.|  
  
## <a name="ole-db-driver-for-sql-server"></a>OLE DB-Treiber für SQLServer  
 Der OLE DB-Treiber für SQL Server unterstützt das Ablaufen von Kennwörtern über eine Benutzerschnittstelle und programmgesteuert.  
  
### <a name="ole-db-user-interface-password-expiration"></a>OLE DB-Benutzeroberfläche für abgelaufene Kennwörter  
 Der OLE DB-Treiber für SQL Server unterstützt das Ablaufen von Kennwörtern durch Änderungen an der **SQL Server-Anmeldung** Dialogfelder. Wenn der Wert DBPROP_INIT_PROMPT auf DBPROMPT_NOPROMPT festgelegt wird, schlägt der erste Verbindungsversuch fehl, wenn das Kennwort abgelaufen ist.  
  
 Wenn DBPROP_INIT_PROMPT in einen anderen Wert festgelegt wurde, sieht der Benutzer die **SQL Server-Anmeldung** Dialogfeld, unabhängig davon, ob das Kennwort abgelaufen ist. Der Benutzer kann dann auf die **Optionen** Schaltfläche aus, und überprüfen Sie **Kennwort ändern** zum Ändern des Kennworts.  
  
 Wenn der Benutzer auf OK klickt und das Kennwort abgelaufen ist, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fordert den Benutzer zur Eingabe und Bestätigung eines neuen Kennworts mithilfe der **SQL Server-Kennwort ändern** Dialogfeld.  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>OLE DB-Eingabeaufforderungsverhalten und gesperrte Konten  
 Verbindungsversuche schlagen möglicherweise fehl, weil das Konto gesperrt wurde. Wenn dies nach der Anzeige des tritt auf, die **SQL Server-Anmeldung** Dialogfeld Fehlermeldung des Servers für den Benutzer angezeigt wird und der Verbindungsversuch wird abgebrochen. Er kann auch auftreten, befolgen die Anzeige der **SQL Server-Kennwort ändern** Dialogfeld, wenn der Benutzer einen falschen Wert für das alte Kennwort eingibt. In diesem Fall wird dieselbe Fehlermeldung angezeigt, und der Verbindungsversuch wird abgebrochen.  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>OLE DB-Verbindungspooling, Ablauf von Kennwörtern und gesperrte Konten  
 Ein Konto kann gesperrt werden oder das dazugehörige Kennwort ablaufen, solange die Verbindung noch in einem Verbindungspool aktiv ist. Der Server überprüft bei zwei Gelegenheiten auf abgelaufene Kennwörter und gesperrte Konten. Zunächst findet eine Überprüfung statt, wenn eine Verbindung hergestellt wird. Die zweite Überprüfung wird nach dem Zurücksetzen einer Verbindung ausgeführt, wenn die Verbindung aus dem Verbindungspool entfernt wird.  
  
 Falls der Zurücksetzungsversuch fehlschlägt, wird die Verbindung aus dem Pool entfernt, und ein Fehler wird zurückgegeben.  
  
### <a name="ole-db-programmatic-password-expiration"></a>Programmgesteuerter Ablauf von Kennwörtern in OLE DB  
 Der OLE DB-Treiber für SQL Server unterstützt das Ablaufen von Kennwörtern durch das Hinzufügen der Eigenschaft SSPROP_AUTH_OLD_PASSWORD (Typ "VT_BSTR"), die dem DBPROPSET_SQLSERVERDBINIT-Eigenschaftensatz hinzugefügt wurde.  
  
 Die vorhandene Password-Eigenschaft verweist auf DBPROP_AUTH_PASSWORD und wird verwendet, um das neue Kennwort zu speichern.  
  
> [!NOTE]  
>  In der Verbindungszeichenfolge legt die "Old Password"-Eigenschaft SSPROP_AUTH_OLD_PASSWORD fest. Dies entspricht dem aktuellen (möglicherweise abgelaufenen) Kennwort, das nicht über eine Anbieterzeichenfolgen-Eigenschaft verfügbar ist.  
  
 Der Anbieter speichert den Wert dieser Eigenschaft nicht persistent. Wenn diese Eigenschaft festgelegt ist, verwendet der Anbieter nicht den Verbindungspool für die erste Verbindung, da eine neue Verbindung hergestellt wird. Wenn die Kennwortänderung ordnungsgemäß vorgenommen werden konnte, kann die aktuelle Verbindung nicht wiederverwendet werden, da sie weiterhin das alte Kennwort verwendet, das nach der Kennwortänderung ungültig wird. Wenn die Anmeldung erfolgreich ist, löscht der Anbieter zudem diese Eigenschaft. Bei späteren Versuchen, das alte Kennwort abzurufen, wird VT_EMPTY zurückgegeben.  
  
> [!NOTE]  
>  SSPROP_AUTH_OLD_PASSWORD sollte nie persistent gespeichert werden, da es nur verwendet wird, wenn ein Kennwort abgelaufen ist.  
  
 Beachten Sie, dass der Anbieter jedes Mal, wenn die Old Password-Eigenschaft festgelegt ist, davon ausgeht, dass versucht wird, das Kennwort zu ändern, es sei denn, es ist auch die Windows-Authentifizierung angegeben, die immer Vorrang hat.  
  
 Wenn Windows-Authentifizierung verwendet wird, führt das alte Kennwort anzugeben entweder zu DB_E_ERRORSOCCURRED oder DB_S_ERRORSOCCURRED abhängig davon, ob das alte Kennwort bzw. als erforderlich oder OPTIONAL angegeben wurde, und der Statuswert der DBPROPSTATUS_ CONFLICTINGBADVALUE wird zurückgegeben, *DwStatus*. Dies wird erkannt, wenn **IDBInitialize:: Initialize** aufgerufen wird.  
  
 Wenn ein Versuch, das Kennwort zu ändern, unerwartet fehlschlägt, gibt der Server den Fehlercode 18468 zurück. Für den Verbindungsversuch wird ein Standard-OLEDB-Fehler zurückgegeben.  
  
 Weitere Informationen zum DBPROPSET_SQLSERVERDBINIT-Eigenschaftensatz finden Sie unter [Initialisierungs- und Autorisierungseigenschaften](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  

  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Features](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
