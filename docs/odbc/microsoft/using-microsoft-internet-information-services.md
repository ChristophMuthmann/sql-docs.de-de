---
title: Mit Microsoft Internet Information Services | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], IIS
- internet information services [ODBC]
- IIS [ODBC]
ms.assetid: 3328f2f1-b34a-472f-82cf-ad49768ff061
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 75659769b4d0318fa21494a3f2ca3262836c69eb
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-microsoft-internet-information-services"></a>Verwenden Microsoft Internetinformationsdienste
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Wenn Sie über Probleme beim Herstellen einer Verbindung von innerhalb eines IIS-Skripts (insbesondere, wenn ein Fehler ORA-12641 angezeigt) verfügen, fügen Sie die folgende Zeile auf die Datei Sqlnet.ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 Dadurch wird der sichere Netzwerkdienste deaktiviert, damit Sie mithilfe der anonymen Authentifizierung eine Verbindung herstellen können.
