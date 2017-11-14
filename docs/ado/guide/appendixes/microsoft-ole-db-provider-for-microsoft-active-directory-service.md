---
title: "Microsoft OLE DB-Anbieter für Microsoft Active Directory-Dienst | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADSI provider [ADO]
- Active Directory Service Interfaces provider [ADO]
- providers [ADO], OLE DB provider for Active Directory service
- OLE DB provider for Active Directory service [ADO]
ms.assetid: f9e81452-5675-4cfc-9949-cfbd2fe57534
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cc6946f6944cf37f85759847f2c8db852d120461
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Microsoft OLE DB-Anbieter für Microsoft Active Directory-Dienst
Die Active Directory Service Interfaces (ADSI)-Anbieter ermöglicht ADO zur Verbindung mit heterogenen Verzeichnisdienste über ADSI. So erhält ADO-Anwendungen nur-Lese Zugriff auf die Microsoft Windows NT 4.0 oder Microsoft Windows 2000-Verzeichnisdienste, zusätzlich zu den LDAP-kompatibles Verzeichnisdienst und Novell-Verzeichnisdienste. ADSI selbst basiert auf ein Anbietermodell, damit bei einem neuen Anbieter gewähren Zugriff auf ein anderes Verzeichnis wird die ADO-Anwendung darauf nahtlos zugreifen werden. Der ADSI-Anbieter Freethread- und Unicode aktiviert ist.  
  
## <a name="connection-string-parameters"></a>Parameter für Verbindungszeichenfolgen  
 Zur Verbindung mit diesem Anbieter Festlegen der **Anbieter** Argument der ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md) -Eigenschaft wie folgt:  
  
```  
ADSDSOObject  
```  
  
 Lesen der [Anbieter](../../../ado/reference/ado-api/provider-property-ado.md) Eigenschaft wird auch dieser Zeichenfolge zurück.  
  
## <a name="typical-connection-string"></a>Typische Verbindungszeichenfolge  
 Eine typische Verbindungszeichenfolge für diesen Anbieter lautet wie folgt:  
  
```  
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 Die Zeichenfolge besteht aus den folgenden Schlüsselwörtern.  
  
|Schlüsselwort|Description|  
|-------------|-----------------|  
|**Anbieter**|Gibt den OLE DB-Anbieter für Active Directory-Dienst an.|  
|**Benutzer-ID**|Gibt den Benutzernamen an. Wenn dieses Schlüsselwort ausgelassen wird, wird die aktuelle Anmeldung verwendet.|  
|**Kennwort**|Gibt das Kennwort des Benutzers an. Wenn dieses Schlüsselwort ausgelassen wird. Anschließend wird die aktuelle Anmeldung verwendet.|  
  
> [!NOTE]
>  Wenn Sie ein Datenquellenanbieter, die Windows-Authentifizierung unterstützt Verbindung, müssen Sie angeben **Trusted_Connection = Yes** oder **Integrated Security = SSPI** anstelle von Benutzer-ID und Kennwort die Informationen in der Verbindungszeichenfolge angegeben.  
  
## <a name="command-text"></a>Befehlstext  
 Eine Textzeichenfolge vierteiligen Befehl wird vom Anbieter in der folgenden Syntax erkannt:  
  
```  
"Root; Filter; Attributes[; Scope]"  
```  
  
|Wert|Description|  
|-----------|-----------------|  
|*Root*|Gibt an, die **"ADsPath"** Objekt aus, das die Suche (d. h. vom Stamm der Suche) zu starten.|  
|*Filter*|Gibt den Suchfilter im Format RFC 1960 an.|  
|*Attribute*|Gibt eine durch Trennzeichen getrennte Liste von Attributen, die zurückgegeben werden.|  
|*Bereich*|Optional. Ein **Zeichenfolge** den Bereich der Suche angibt. Kann einen der folgenden Werte annehmen:<br /><br /> -Basis – Suchen Sie nur das Basisobjekt (Stammverzeichnis für die Suche).<br />-Ebene – Suchen Sie nur eine Ebene.<br />-Unterstruktur – Suchen Sie die gesamte Unterstruktur.|  
  
 Beispiel:  
  
```  
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 Der Anbieter unterstützt auch SQL SELECT-Anweisung für Befehlstext. Beispiel:  
  
```  
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>Hinweise  
 Der Anbieter akzeptiert keine Aufrufe von gespeicherten Prozeduren oder einfache Tabellennamen (z. B. die [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) Eigenschaft werden immer **AdCmdText**). Finden Sie in der Active Directory-Dienstschnittstellen-Dokumentation für eine ausführlichere Beschreibung der Befehl Textelemente.  
  
## <a name="recordset-behavior"></a>Recordset-Verhalten  
 Die folgenden Tabellen enthalten die Funktionen, die über eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) mithilfe dieses Anbieters geöffnet. Nur der statische Cursor-Datentyp (**AdOpenStatic**) verfügbar ist.  
  
 Weitere Informationen zu **Recordset** Verhalten für die Anbieterkonfiguration kann durch Ausführen der [unterstützt](../../../ado/reference/ado-api/supports-method.md) Methode und Auflisten von der [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung von der  **Recordset** zu bestimmen, ob die anbieterspezifische dynamische Eigenschaften vorhanden sind.  
  
 **Verfügbarkeit von ADO-Recordset Standardeigenschaften:**  
  
|Eigenschaft|Verfügbarkeit|  
|--------------|------------------|  
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|Lese-/Schreibzugriff|  
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|Lese-/Schreibzugriff|  
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|Schreibgeschützt|  
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|Schreibgeschützt|  
|[Lesezeichen](../../../ado/reference/ado-api/bookmark-property-ado.md)|Lese-/Schreibzugriff|  
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|Lese-/Schreibzugriff|  
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|immer **AdUseServer**|  
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|immer **AdOpenStatic**|  
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|immer **AdEditNone**|  
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|Schreibgeschützt|  
|[Filter](../../../ado/reference/ado-api/filter-property.md)|Lese-/Schreibzugriff|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|Lese-/Schreibzugriff|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|Nicht verfügbar|  
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|Lese-/Schreibzugriff|  
|["PageCount"](../../../ado/reference/ado-api/pagecount-property-ado.md)|Schreibgeschützt|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|Lese-/Schreibzugriff|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|Schreibgeschützt|  
|[Quelle](../../../ado/reference/ado-api/source-property-ado-recordset.md)|Lese-/Schreibzugriff|  
|[Status](../../../ado/reference/ado-api/state-property-ado.md)|Schreibgeschützt|  
|[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)|Schreibgeschützt|  
  
 **Verfügbarkeit von Standardmethoden für die ADO-Recordset:**  
  
|Methode|Verfügbar?|  
|------------|----------------|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|Nein|  
|[Abbrechen](../../../ado/reference/ado-api/cancel-method-ado.md)|Nein|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|Nein|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|Nein|  
|[Klon](../../../ado/reference/ado-api/clone-method-ado.md)|ja|  
|[Schließen](../../../ado/reference/ado-api/close-method-ado.md)|ja|  
|[Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|Nein|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|ja|  
|[Verschieben](../../../ado/reference/ado-api/move-method-ado.md)|ja|  
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|ja|  
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|ja|  
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|ja|  
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|ja|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|ja|  
|[Öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md)|ja|  
|[Requery](../../../ado/reference/ado-api/requery-method.md)|ja|  
|[Erneut synchronisieren](../../../ado/reference/ado-api/resync-method.md)|ja|  
|[Unterstützt](../../../ado/reference/ado-api/supports-method.md)|ja|  
|[Update](../../../ado/reference/ado-api/update-method.md)|Nein|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|Nein|  
  
 Weitere Informationen zu ADSI und die Einzelheiten des Anbieters finden Sie in den Active Directory-Dienstschnittstellen-Dokumentation oder besuchen Sie die ADSI-Webseite.  
  
## <a name="see-also"></a>Siehe auch  
 [CommandType-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [ConnectionString-Eigenschaft (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)   
 [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Anbietereigenschaft (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Unterstützt-Methode](../../../ado/reference/ado-api/supports-method.md)

