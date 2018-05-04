---
title: Connect-Abschnitt der Anpassungsdatei | Microsoft Docs
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
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 12d1560220a9c281425a1d75c43f0ef95845d611
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="customization-file-connect-section"></a>Connect-Abschnitt der Anpassungsdatei
Das Standardverhalten des ereignishandlers ist, alle Verbindungen zu verweigern. Die **verbinden** Abschnitt gibt Ausnahmen zu diesem Verhalten. Angenommen, wenn alle der **verbinden** Abschnitte wurden, fehlt oder ist leer, und klicken Sie dann standardmäßig keine Verbindungen hergestellt werden konnte.  
  
 Die **verbinden** Abschnitt kann enthalten:  
  
-   Ein Eintrag, der angibt, die standardmäßig Zugriff Lese- und Schreibvorgänge, die für diese Verbindung zulässig. Wenn kein Standard-Access-Eintrag im Abschnitt vorhanden ist, wird der Abschnitt ignoriert.  
  
-   Eine neue Verbindungszeichenfolge, die von der Clientverbindungszeichenfolge ersetzt.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
 Ein Zugriffseintrag besitzt das Format:  
  
```  
  
Access=  
accessRight  
  
```  
  
 Ein Ersetzung Verbindungszeichenfolgeneintrag besitzt das Format:  
  
```  
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>Hinweise  
  
|Teil|Description|  
|----------|-----------------|  
|**Verbinden**|Eine Literalzeichenfolge, die dies weist darauf hin handelt es sich um einen Verbindungszeichenfolgeneintrag.|  
|***connectionString***|Eine Zeichenfolge, die die gesamte Clientverbindungszeichenfolge ersetzt.|  
|**Zugriff**|Eine Literalzeichenfolge, die dies weist darauf hin handelt es sich um einen Eintrag.|  
|***accessRight***|Einer der folgenden Zugriffsrechte:<br /><br /> -   **NoAccess** – Benutzer kann nicht auf die Datenquelle zugreifen.<br />-   **ReadOnly** – der Benutzer kann die Datenquelle lesen.<br />-   **ReadWrite** – Benutzer Lese- oder Schreibzugriff auf die Datenquelle.|  
  
 Wenn Sie eine Verbindung (in Effekt, deaktivieren das Standardverhalten für die Handler) zulassen möchten, legen Sie den Access-Eintrag der **Standard verbinden** -Abschnitt hinzu `Access=ReadWrite`, und löschen, oder kommentieren Sie Sie aus einer anderen **verbinden** *Bezeichner* Abschnitt.  
  
## <a name="see-also"></a>Siehe auch  
 [Anpassung Dateiabschnitt-Protokolle](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [SQL-Abschnitt der Anpassung](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Anpassung UserList Dateiabschnitt](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory-Anpassung](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Erforderlichen Clienteinstellungen](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Grundlegendes zu der Anpassungsdatei](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Schreiben Ihres eigenen benutzerdefinierten Handlers](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



