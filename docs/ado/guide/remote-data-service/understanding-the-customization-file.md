---
title: Grundlegendes zur Anpassungsdatei | Microsoft Docs
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
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 99a565fe6ee25f1fb8d0911b80c0b629c02b3cdf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-the-customization-file"></a>Grundlegendes zu der Anpassungsdatei
Jede Überschrift des Abschnitts in der Anpassungsdatei besteht aus eckige Klammern (**[]**), die einen Typ und die Parameter enthält. Die vier Abschnittstypen werden durch die Literalzeichenfolgen angegeben **verbinden**, **Sql**, **Userlist**, oder **Protokolle**. Der Parameter ist die Literalzeichenfolge, der Standardwert, eine vom Benutzer angegebenen Bezeichner oder nichts an.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Jeder Abschnitt ist daher mit einem der folgenden Abschnittsheader gekennzeichnet:  
  
```  
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 Den Abschnittsnamen bestehen aus folgenden Teilen.  
  
|Teil|Description|  
|----------|-----------------|  
|**connect**|Eine literale Zeichenfolge, die eine Verbindungszeichenfolge ändert.|  
|**sql**|Eine literale Zeichenfolge, die eine Befehlszeichenfolge ändert.|  
|**userlist**|Eine literale Zeichenfolge, die die Zugriffsrechte eines bestimmten Benutzers ändert.|  
|**logs**|Ein Zeichenfolgenliteral, das eine Aufzeichnung Ausführungsfehler Protokolldatei angibt.|  
|**default**|Ein Zeichenfolgenliteral, das verwendet wird, wenn kein Bezeichner angegeben wird oder gefunden.|  
|*identifier*|Eine Zeichenfolge, die eine Zeichenfolge in entspricht dem **verbinden** oder **Befehl** Zeichenfolge.<br /><br /> -Verwenden Sie diesen Abschnitt aus, wenn der Überschrift des Abschnitts enthält **verbinden** und die Bezeichner in der Verbindungszeichenfolge gefunden wird.<br />-Verwenden Sie diesen Abschnitt aus, wenn der Überschrift des Abschnitts enthält **Sql** und die Bezeichner in der Befehlszeichenfolge gefunden wird.<br />-Verwenden Sie diesen Abschnitt aus, wenn der Überschrift des Abschnitts enthält **Userlist** und die ID-Zeichenfolge entspricht einem **verbinden** Abschnitt Bezeichner.|  
  
 Die **DataFactory** Ruft den Handler auf, und übergeben Sie Clientparameter. Der Handler sucht nach ganzen Zeichenfolgen in die Clientparameter, die Bezeichner in den entsprechenden Abschnitt-Headern übereinstimmen. Wenn eine Übereinstimmung gefunden wird, werden die Inhalte des Abschnitts an den Clientparameter angewendet.  
  
 Ein bestimmtes Bereichs wird in den folgenden Situationen verwendet:  
  
-   Ein **verbinden** Abschnitt wird verwendet, wenn der Wertteil des Clients die Schlüsselwort, eine Verbindung herstellen "**Datenquelle = *** Wert*", entspricht einer **verbinden** Abschnitt Bezeichner *.*  
  
-   Ein **Sql** Abschnitt wird verwendet, wenn die Clientbefehlszeichenfolge eine Zeichenfolge enthält, die entspricht einer **Sql** Abschnitt Bezeichner.  
  
-   Ein **verbinden** oder **Sql** Abschnitt mit einem Standardparameter wird verwendet, wenn kein übereinstimmender Bezeichner vorhanden ist.  
  
-   Ein **Userlist** Abschnitt wird verwendet, wenn die **Userlist** Abschnitt Bezeichner entspricht einer **verbinden** Abschnitt Bezeichner. Wenn eine Übereinstimmung auftritt, den Inhalt der **Userlist** Abschnitt gelten für die Verbindung, unterliegt die **verbinden** Abschnitt.  
  
-   Die Zeichenfolge in eine Zeichenfolge Verbindung oder Befehl den Bezeichner in einem stimmt nicht überein **verbinden** oder **Sql** Abschnitt Header, und es gibt keine **verbinden** oder **Sql**  Abschnitt Header mit einem Standardparameter, und klicken Sie dann die Clientzeichenfolge ohne Änderungen verwendet wird.  
  
-   Die **Protokolle** Abschnitt wird verwendet, wenn die **DataFactory** in Betrieb ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Connect-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Anpassung Dateiabschnitt-Protokolle](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [SQL-Abschnitt der Anpassung](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Anpassung UserList Dateiabschnitt](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory-Anpassung](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Erforderlichen Clienteinstellungen](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Schreiben Ihres eigenen benutzerdefinierten Handlers](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)




















