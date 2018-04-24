---
title: Erforderliche Clienteinstellungen | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
ms.assetid: e776b4e3-fcc4-4bfb-a7e8-5ffae1d83833
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9323561f533cf4d7f0b11aa23ed5da5b8cdce768
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="required-client-settings"></a>Erforderlichen Clienteinstellungen
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Geben Sie die folgenden Einstellungen aus, um eine benutzerdefinierte **DataFactory** Handler.  
  
-   Geben Sie "Anbieter = MS-Remote" in der [Verbindung Object (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) Objekt [Anbieter-Eigenschaft (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) Eigenschaft oder die **Verbindung** -Objekt Verbindungszeichenfolge "**Anbieter**= "Schlüsselwort.  
  
-   Legen Sie die [CursorLocation-Eigenschaft (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft **AdUseClient**.  
  
-   Geben Sie den Namen des ereignishandlers zur Verwendung in der [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md) des Objekts **Handler** -Eigenschaft, oder die [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) Verbindungszeichenfolge des Objekts " **Handler**= "Schlüsselwort. (Den Handler kann nicht festgelegt werden, der **Verbindung** Objekt Verbindungszeichenfolge.)  
  
 RDS stellt einen Standard-Handler bereit, auf dem Server mit dem Namen **MSDFMAP. Handler**. (Die Standarddatei für die Anpassung heißt MSDFMAP. INI.)  
  
 **Beispiel**  
  
 Angenommen, in den folgenden Abschnitten **MSDFMAP. INI** und der Name der Datenquelle, AdvWorks, zuvor definiert wurden:  
  
```  
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 Die folgenden Codeausschnitte sind in Visual Basic geschrieben:  
  
## <a name="rdsdatacontrol-version"></a>RDS. DataControl-Version  
  
```  
Dim dc as New RDS.DataControl  
Set dc.Handler = "MSDFMAP.Handler"  
Set dc.Server = "http://yourServer"  
Set dc.Connect = "Data Source=CustomerDatabase"  
Set dc.SQL = "CustomerById(4)"  
dc.Refresh  
```  
  
## <a name="recordset-version"></a>Recordset-Version  
  
```  
Dim rs as New ADODB.Recordset  
rs.CursorLocation = adUseClient  
```  
  
 Geben Sie entweder die [Handler-Eigenschaft (RDS)](../../../ado/reference/rds-api/handler-property-rds.md) Eigenschaft oder das Schlüsselwort; die [Anbieter-Eigenschaft (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) Eigenschaft oder das Schlüsselwort und die *CustomerById* und  *CustomerDatabase* Bezeichner. Öffnen Sie dann die **Recordset** Objekt  
  
 RS. Öffnen Sie "CustomerById(4)", "Handler = MSDFMAP. Handler;"& _  
  
```  
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=http://yourServer"  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Connect-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [SQL-Abschnitt der Anpassung](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Anpassung UserList Dateiabschnitt](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory-Anpassung](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Erforderlichen Clienteinstellungen](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Grundlegendes zu der Anpassungsdatei](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Schreiben Ihres eigenen benutzerdefinierten Handlers](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)






















