---
title: Freigeben von Deskriptoren | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0977ba814841ab2fa445a1009262e4a2bfd3a5b3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="freeing-descriptors"></a>Freigeben von Deskriptoren
Können explizit zugewiesene Deskriptoren reserviert, entweder explizit durch Aufrufen von **SQLFreeHandle** mit *HandleType* SQL_HANDLE_DESC oder implizit, wenn das Verbindungshandle freigegeben. Wenn ein explizit reservierte Deskriptor freigegeben wird, alle Anweisungshandles auf die freigegebenen Deskriptors automatisch angewendet, die auf die Deskriptoren implizit für sie reservierten zurückgesetzt.  
  
 Implizit zugeordnete Deskriptoren freigegeben werden können, nur durch das Aufrufen **SQLDisconnect**, dem löscht alle Anweisungen oder Deskriptoren zu öffnen, für die Verbindung oder durch Aufrufen von **SQLFreeHandle** mit einem  *HandleType* von SQL_HANDLE_STMT auf, um ein Anweisungshandle und alle der Anweisung zugeordneten implizit zugeordneten Deskriptoren freizugeben. Eine implizit zugeordnete Sicherheitsbeschreibung nicht freigegeben werden, durch den Aufruf **SQLFreeHandle** mit einem *HandleType* von SQL_HANDLE_DESC.  
  
 Ein implizit zugeordneten Deskriptor bleibt gültig, sogar wenn freigegeben, und **SQLGetDescField** für ihre Felder aufgerufen werden kann.
