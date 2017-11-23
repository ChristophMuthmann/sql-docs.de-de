---
title: Connect-Eigenschaft (RDS) | Microsoft Docs
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
helpviewer_keywords: Connect property [ADO]
ms.assetid: dbad5e77-b213-4eb8-aecf-d60f203fdb59
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb6a9a33267b70f83eb9a3c559ec24e5e1427af7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="connect-property-rds"></a>Connect-Eigenschaft (RDS)
Gibt den Namen der Datenbank, von dem die Abfrage und Update-Vorgänge ausgeführt werden.  
  
 Sie können festlegen, die **verbinden** Eigenschaft zur Entwurfszeit in den [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekttags des Objekts, oder zur Laufzeit in Skriptcode (z. B. VBScript).  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>Parameter  
 *"ConnectionString"*  
 Eine gültige Verbindungszeichenfolge. Weitere allgemeine Informationen zu Verbindungszeichenfolgen finden Sie unter der ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md) Eigenschaft oder der Dokumentation Ihres Anbieters.  
  
> [!NOTE]
>  Angeben von MS Remote als Anbieter für die **RDS. DataControl** würde ein Szenario mit vier Ebenen erstellen. Szenarien, die mehr als drei Ebenen wurden nicht getestet und sollte nicht benötigt werden.  
  
 *DataControl*  
 Objektvariable stellt eine **RDS. DataControl** Objekt.  
  
## <a name="applies-to"></a>Gilt für  
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Verbinden Sie die Eigenschaft-Beispiel (VBScript)](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [Query-Methode (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Refresh-Methode (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges-Methode (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


