---
title: Testen der ODBC-Verbindung | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- testing connections [ODBC]
- ODBC driver for Oracle [ODBC], testing connections
ms.assetid: 5e671665-2aba-49a7-8871-70784d8b3cc9
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba90587f40b3c7ef21f0dd1b6169ad6b0ab1b119
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="testing-the-odbc-connection"></a>Testen der ODBC-Verbindung
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Bei der Problembehandlung der ODBC-Zugriff auf Oracle 7.x und 8 RDBMS-Server, ist es möglicherweise erforderlich, um zu überprüfen, ob die zugrunde liegende SQL * Net und Adapter für Oracle-Protokoll ordnungsgemäß installiert. Zu diesem Zweck verwenden Sie das Hilfsprogramm Oracle bereitgestellte Nettest.exe im Verzeichnis Orawin\Bin.  
  
 Nettest ist ein einfaches Utility, die versucht, melden Sie sich an den ausgewählten Server mit nur der installierten SQL * Net-Software, die Teil der Oracle-Client ist. Das Dienstprogramm fordert einen Anmeldenamen, verbinden Sie das Kennwort und TNS Zeichenfolge. Wenn der Oracle-Client ordnungsgemäß installiert ist, zeigt das Hilfsprogramm einfach "Ping erfolgreich." Wenn die Anmeldung nicht erfolgreich war, müssen Sie ein Datenbankadministrator konsultieren.
