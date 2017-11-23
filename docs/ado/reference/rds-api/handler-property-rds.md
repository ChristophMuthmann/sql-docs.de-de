---
title: Handlereigenschaft (RDS) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 15fa49306bf566b27f0d5e688a16050c9656032c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="handler-property-rds"></a>Handlereigenschaft (RDS)
Gibt den Namen eines Programms serverseitige Anpassung (Ereignishandler), die die Funktionalität des erweitert die [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), und alle Parameter verwendet, die *Handler*.  
  
 **Gilt für:** [RDS (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>Parameter  
 *DataControl*  
 Objektvariable stellt eine [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt.  
  
 *String*  
 Ein **Zeichenfolge** Wert, der den Namen der der Handler und alle Parameter enthält, die alle durch Trennzeichen getrennt (z. B. `"handlerName,parm1,parm2,...,parm` *N*`"`).  
  
## <a name="remarks"></a>Hinweise  
 Diese Eigenschaft unterstützt [Anpassung](../../../ado/guide/remote-data-service/datafactory-customization.md), eine Funktion, die Einstellung muss der [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft **AdUseClient**.  
  
 Der Name der der Handler und den zugehörigen Parametern ggf. durch Kommas getrennt (","). Führt zu unvorhersehbares Verhalten führen, wenn ein Semikolon (";") wird an einer beliebigen Stelle in *Zeichenfolge*. Sie können einen eigenen Handler schreiben, sofern dies unterstützt die **IDataFactoryHandler** Schnittstelle.  
  
 Der Name der Standardhandler ist **MSDFMAP. Handler**, und der Standardparameter ist eine Anpassungsdatei namens **MSDFMAP. INI**. Verwenden Sie diese Eigenschaft, um alternative Anpassungsdateien erstellt vom Serveradministrator aufzurufen.  
  
 Die Alternative zur Einstellung der **Handler** Eigenschaft ist die Angabe eines Handlers und Parameter in der ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md) Eigenschaft; d. h. "**Handler =**  *HandlerName, parameter1, parameter2,* ".  
  
## <a name="applies-to"></a>Gilt für  
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel für Dateneigenschaften Handler (VB)](../../../ado/reference/rds-api/handler-property-example-vb.md)   
 [DataFactory-Anpassung](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [DataFactory-Objekt (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


