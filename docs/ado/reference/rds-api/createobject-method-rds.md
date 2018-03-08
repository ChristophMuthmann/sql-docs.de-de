---
title: CreateObject-Methode (RDS) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aeca3cd5d525a3712511a3d7fd59f82210c041e0
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="createobject-method-rds"></a>CreateObject-Methode (RDS)
Erstellt den Proxy für das Zielobjekt für Business und gibt einen Zeiger darauf zurück. Die Proxy-Pakete und marshallt Daten an den serverseitigen Stub für die Kommunikation mit dem Business-Objekt zum Senden von Anforderungen und Daten über das Internet. Für Objekte der in-Process-Komponente keine Proxys verwendet werden, nur ein Zeiger auf das Objekt wird bereitgestellt.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
 Remote Data Service unterstützt die folgenden Protokolle: HTTP, HTTPS (HTTP over Secure Socket Layer), DCOM und in-Process.  
  
|Protokoll|Syntax|  
|--------------|------------|  
|HTTP|Set object = DataSpace.CreateObject("ProgId", "http://awebsrvr")|  
|HTTPS|Set object = DataSpace.CreateObject("ProgId", "https://awebsrvr")|  
|DCOM|Set object = DataSpace.CreateObject("ProgId", "computername")|  
|In-Process|Set object = DataSpace.CreateObject("ProgId", "")|  
  
## <a name="parameters"></a>Parameter  
 *Objekt*  
 Ein Object-Variablen, die ein Objekt ergibt, der im angegebenen Typ ist *ProgID*.  
  
 *DataSpace*  
 Objektvariable stellt eine [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) Objekt, das zum Erstellen einer Instanz des neuen Objekts verwendet.  
  
 *ProgID*  
 Ein **Zeichenfolge** Wert, der die Angabe ein serverseitiges Geschäftsobjekt, das die Anwendung von Geschäftsregeln implementiert programmatischen Bezeichner enthält.  
  
 *Awebsrvr* oder *Computername*  
 Ein **Zeichenfolge** Wert, der stellt eine URL identifiziert die Internetinformationsdienste (Internet Information Services, IIS)-Webserver, auf dem eine Instanz des Server-Business-Objekts erstellt wird.  
  
## <a name="remarks"></a>Hinweise  
 Die *HTTP-Protokoll* ist das Standardprotokoll für die Web; *HTTPS* ist eine sichere Webprotokoll. Verwenden der *DCOM-Protokolls* beim Ausführen einer lokalen Netzwerk ohne HTTP. Die *prozessintern* Protokoll ist eine lokale Dynamic Link Library (DLL), ein Netzwerk nicht verwendet.  
  
## <a name="applies-to"></a>Gilt für  
 [DataSpace-Objekt (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [DataFactory-Objekt, Abfragemethode und CreateObject-Methode (Beispiel (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [DataSpace-Objekt und CreateObject-Methode (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [CreateRecordset-Methode (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)


