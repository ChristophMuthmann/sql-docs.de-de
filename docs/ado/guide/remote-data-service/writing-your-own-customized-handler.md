---
title: Schreiben einen eigene benutzerdefinierten Ereignishandler | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b780e2027e64f7832fd622e66e1d908696d24b0e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="writing-your-own-customized-handler"></a>Schreiben Sie einen eigene benutzerdefinierten Handler
Sie möchten einem eigenen Handler zu schreiben, wenn Sie einen IIS-Server-Administrator möchte die Standardeinstellung für die Unterstützung von RDS werden jedoch mehr Kontrolle über die benutzeranforderungen und Zugriffsrechte.  
  
 Die MSDFMAP. Ereignishandler implementiert die **IDataFactoryHandler** Schnittstelle.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="idatafactoryhandler-interface"></a>IDataFactoryHandler-Schnittstelle  
 Diese Schnittstelle verfügt über zwei Methoden **GetRecordset** und **eine erneute Verbindung**. Beide Methoden erfordern, die die [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft festgelegt werden, um **AdUseClient**.  
  
 Beide Methoden akzeptieren Argumente, die nach dem ersten Komma in der "**Handler =**" Schlüsselwort. Beispielsweise `"Handler=progid,arg1,arg2;"` Argumentzeichenfolge übergibt `"arg1,arg2"`, und `"Handler=progid"` wird ein null-Argument übergeben.  
  
## <a name="getrecordset-method"></a>GetRecordset-Methode  
 Diese Methode fragt die Datenquelle und erstellt einen neuen [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekt mit den angegebenen Argumenten. Die **Recordset** muss geöffnet sein, mit **AdLockBatchOptimistic** und müssen nicht asynchron geöffnet werden.  
  
### <a name="arguments"></a>Argumente  
 ***Conn*** der Verbindungszeichenfolge angegeben.  
  
 ***Args*** die Argumente für den Handler.  
  
 ***Abfrage*** der Befehlstext für eine Abfrage.  
  
 ***PpRS*** den Zeiger, in dem die **Recordset** zurückgegeben werden soll.  
  
## <a name="reconnect-method"></a>Reconnect-Methode  
 Diese Methode wird die Datenquelle aktualisiert. Er erstellt ein neues [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) -Objekt und fügt die angegebenen **Recordset**.  
  
### <a name="arguments"></a>Argumente  
 ***Conn*** der Verbindungszeichenfolge angegeben.  
  
 ***Args*** die Argumente für den Handler.  
  
 ***pRS*** ein **Recordset** Objekt.  
  
## <a name="msdfhdlidl"></a>msdfhdl.idl  
 Dies ist die Schnittstellendefinition für **IDataFactoryHandler** , angezeigt wird, der **///msdfhdl.idl** Datei.  
  
```  
[  
  uuid(D80DE8B3-0001-11d1-91E6-00C04FBBBFB3),  
  version(1.0)  
]  
library MSDFHDL  
{  
    importlib("stdole32.tlb");  
    importlib("stdole2.tlb");  
  
    // TLib : Microsoft ActiveX Data Objects 2.0 Library  
    // {00000200-0000-0010-8000-00AA006D2EA4}  
    #ifdef IMPLIB  
    importlib("implib\\x86\\release\\ado\\msado15.dll");  
    #else  
    importlib("msado20.dll");  
    #endif  
  
    [  
      odl,  
      uuid(D80DE8B5-0001-11d1-91E6-00C04FBBBFB3),  
      version(1.0)  
    ]  
    interface IDataFactoryHandler : IUnknown  
    {  
HRESULT _stdcall GetRecordset(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] BSTR query,  
      [out, retval] _Recordset **ppRS);  
  
// DataFactory will use the ActiveConnection property  
// on the Recordset after calling Reconnect.  
   HRESULT _stdcall Reconnect(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] _Recordset *pRS);  
    };  
};  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Connect-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Anpassung Dateiabschnitt-Protokolle](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [SQL-Abschnitt der Anpassung](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Anpassung UserList Dateiabschnitt](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory-Anpassung](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Erforderlichen Clienteinstellungen](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Grundlegendes zu der Anpassungsdatei](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)


