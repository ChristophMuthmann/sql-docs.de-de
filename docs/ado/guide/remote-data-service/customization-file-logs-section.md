---
title: Anpassungsdatei protokolliert Abschnitt | Microsoft Docs
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
- logs section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: a368e264-865c-41ee-be00-d9097255c2ea
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37bcfdea2c98295d2869cd4bc5766e89758e2773
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="customization-file-logs-section"></a>Anpassung Dateiabschnitt-Protokolle
Die **Protokolle** Abschnitt enthält einen Protokolleintrag für die Datei, der den Namen einer Datei angibt, die Fehler beim Ausführen des zeichnet die **DataFactory**.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
 Ein Protokolleintrag für die Datei besitzt das Format:  
  
```  
  
err=  
FileName  
  
```  
  
## <a name="remarks"></a>Hinweise  
  
|Teil|Description|  
|----------|-----------------|  
|**err**|Eine Literalzeichenfolge, die dies weist darauf hin handelt es sich um einen Protokolleintrag für die Datei.|  
|*FileName*|Einen vollständigen Pfad und Dateinamen ein. Der Name der Standard ist **c:\msdfmap.log**.|  
  
 Die Protokolldatei enthält den Benutzernamen, HRESULT, Datum und Zeit der einzelnen Fehler an.  
  
## <a name="see-also"></a>Siehe auch  
 [Connect-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [SQL-Abschnitt der Anpassung](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Anpassung UserList Dateiabschnitt](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory-Anpassung](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Erforderlichen Clienteinstellungen](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Grundlegendes zu der Anpassungsdatei](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Schreiben Ihres eigenen benutzerdefinierten Handlers](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


