---
title: Servereigenschaft (RDS) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- RDS::IBindMgr21::Server
helpviewer_keywords:
- Server property [RDS]
ms.assetid: d2727ce7-da9f-4271-ae3c-9334ef477c14
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 05ff98ce99d444a9b5dfc1aac035920a29482d7c
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="server-property-rds"></a>Servereigenschaft (RDS)
Gibt das Protokoll (Internet Information Services, IIS), Namen und die Kommunikation an.  
  
 Sie können festlegen, die **Server** Eigenschaft zur Entwurfszeit in den OBJECT-Tags des der[RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) -Objekts oder zur Laufzeit im Skriptcode.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
 **HTTP**  
  
 Während der Entwurfszeit-syntax  
  
```  
  
<PARAM NAME="Server" VALUE="http:  
//awebsrvr:port  
">  
  
```  
  
 Laufzeit-syntax  
  
```  
  
DataControl  
.Server="http://  
awebsrvr:port  
"  
  
```  
  
 **HTTPS**  
  
 Während der Entwurfszeit-syntax  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 Laufzeit-syntax  
  
```  
  
DataControl.Server="https://awebsrvr:port"  
```  
  
 **DCOM**  
  
 Während der Entwurfszeit-syntax  
  
```  
  
<PARAM NAME="Server" VALUE="  
computername  
">  
  
```  
  
 Laufzeit-syntax  
  
```  
  
DataControl.Server="computername"  
```  
  
 **In-process**  
  
 Während der Entwurfszeit-syntax  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 Laufzeit-syntax  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>Parameter  
 *Awebsrvr*oder *Computername*  
 Ein **Zeichenfolge** Wert, der ein Internet oder Intranetpfad oder Namen des Computers enthält, wenn der Server auf einem Remotecomputer; oder eine leere Zeichenfolge ist, wenn der Server auf dem lokalen Computer befindet.  
  
 *port*  
 Optional. Ein Port, der für die Verbindung zu einem Server mit IIS verwendet wird. Die Portnummer wird festgelegt, in Internet Explorer (auf der **Ansicht** im Menü klicken Sie auf **Optionen**, und wählen Sie dann die **Verbindung** Registerkarte) oder in IIS.  
  
 *DataControl*  
 Objektvariable stellt eine **RDS. DataControl** Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Der Server ist der Speicherort, in dem die **RDS. DataControl** Anforderung (d. h. eine Abfrage oder Aktualisierung) verarbeitet wird. Standardmäßig werden alle Anforderungen verarbeitet, durch die [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) Objekt [MSDFMAP. Handler](../../../ado/guide/remote-data-service/datafactory-customization.md) Komponente und [MSDFMAP. INI](../../../ado/guide/remote-data-service/understanding-the-customization-file.md) Datei auf dem angegebenen Server. Beachten Sie, dass beim Ändern von Servern zum Abstimmen von Einstellungen in der alten und neuen **MSDFMAP. INI** Dateien. Inkompatibilitäten möglicherweise Anforderungen, die erfolgreich auf einem Server auf einen anderen ein Fehler auf. Wenn die Server-Eigenschaft auf die leere Zeichenfolge festgelegt ist "", werden diese Objekte auf dem lokalen Computer verwendet werden.  
  
## <a name="applies-to"></a>Gilt für  
 [RDS (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Server-Eigenschaft-Beispiel (VBScript)](../../../ado/reference/rds-api/server-property-example-vbscript.md)   
 [Connect-Eigenschaft (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [SQL-Eigenschaft](../../../ado/reference/rds-api/sql-property.md)   
 [SubmitChanges-Methode (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)



