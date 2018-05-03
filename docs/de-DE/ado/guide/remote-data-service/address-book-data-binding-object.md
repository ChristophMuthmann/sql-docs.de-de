---
title: Adresse Buch Datenbindungsfunktionen Objekt | Microsoft Docs
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
- RDS scenarios [ADO], data-binding object
- address book application scenario [ADO], data-binding object
ms.assetid: 080c1925-d453-4b89-92ac-c93591490518
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c5945e4f8e89bd60a90da3a9901075b08faa9bf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="address-book-data-binding-object"></a>Adressobjekt Book-Datenbindung
Das Adressbuch-Anwendung verwendet die [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt so binden Sie Daten aus der SQL Server-Datenbank auf ein visuelles Objekt (in diesem Fall eine DHTML-Tabelle) in der Anwendung Client HTML-Seite. Ereignisgesteuerte VBScript-Programmlogik verwendet die [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) an:  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
-   Die Datenbank abzufragen, Senden von Aktualisierungen an die Datenbank und aktualisieren Sie das Datenraster.  
  
-   Ermöglichen Sie Benutzern, die erste Seite als Nächstes vorherige verschieben, oder zum letzten Datensatz im Datenraster an.  
  
 Der folgende Code definiert die **RDS. DataControl** Komponente:  
  
```  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="http://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 Das Objekttag definiert die **RDS. DataControl** Komponente in der Anwendung. Das Tag enthält zwei Arten von Parametern:  
  
-   Die generische Objekttag zugeordnet.  
  
-   Die speziellen der **RDS. DataControl** Objekt.  
  
## <a name="generic-object-tag-parameters"></a>Generisches Objekt Tag-Parameter  
 Die folgende Tabelle beschreibt die Netzwerkprotokollkonfiguration verknüpft sind mit Objekttag.  
  
|Parameter|Description|  
|---------------|-----------------|  
|***CLASSID***|Eine eindeutige, 128-Bit-Zahl, die den Typ des eingebetteten Objekts an das System identifiziert. Dieser Bezeichner wird in der Registrierung des lokalen Computers System verwaltet. (Für die Klassen-IDs der **RDS. DataControl** Objekt, finden Sie unter [RDS. RDS](../../../ado/reference/rds-api/datacontrol-object-rds.md).)|  
|***ID***|Definiert einen dokumentweiten Bezeichner für das eingebettete Objekt ab, das im Code angezeigt werden soll.|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>RDS. DataControl Tag-Parameter  
 Die folgende Tabelle beschreibt die Parameter, die spezifisch für die **RDS. DataControl** Objekt. (Eine vollständige Liste der **RDS. DataControl** Objekt, Parameter, und wann Sie zu implementieren, finden Sie unter [RDS. RDS](../../../ado/reference/rds-api/datacontrol-object-rds.md).)  
  
|Parameter|Description|  
|---------------|-----------------|  
|[SERVER](../../../ado/reference/rds-api/server-property-rds.md)|Wenn Sie HTTP verwenden, wird der Wert ist der Name des Servercomputers vorangestellt `http://`.|  
|[CONNECT](../../../ado/reference/rds-api/connect-property-rds.md)|Stellt die erforderlichen Verbindungsinformationen für die **RDS. DataControl** zur Verbindung mit SQL Server.|  
|[SQL](../../../ado/reference/rds-api/sql-property.md)|Legt fest oder gibt die Abfragezeichenfolge zum Abrufen der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).|  
  
## <a name="see-also"></a>Siehe auch  
 [Adress Book-Befehlsschaltflächen](../../../ado/guide/remote-data-service/address-book-command-buttons.md)


