---
title: Die Bedeutung der Cursorposition | Microsoft Docs
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
- server-side cursors [ADO]
- cursors [ADO], client-side
- client-side cursors [ADO]
- cursors [ADO], server-side
ms.assetid: 70ef5b1c-0459-41a1-b796-031f61a29a8a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5699c8c7bc3ab1ed54d9411ff889e43e8cf334d5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="the-significance-of-cursor-location"></a>Die Bedeutung der Cursorposition
Jeder Cursor verwendet temporäre Ressourcen zum Speichern der Daten. Diese Ressourcen können Speicher, eine Auslagerungsdatei des Datenträgers, temporäre Datenträgerdateien oder sogar temporären Speicherplatz in der Datenbank sein. Der Cursor wird aufgerufen, eine *clientseitige* Cursor, wenn diese Ressourcen auf dem Clientcomputer gespeichert werden. Der Cursor wird aufgerufen, eine *serverseitige* Cursor, wenn diese Ressourcen auf dem Server gespeichert sind.  
  
## <a name="client-side-cursors"></a>Die clientseitige Cursor  
 Rufen Sie in ADO für einen clientseitigen Cursor durch Verwenden der **AdUseClient CursorLocationEnum.** Mit einer nicht-Client-Side Keysetcursor sendet der Server das gesamte Resultset an den Clientcomputer im Netzwerk. Der Clientcomputer enthält und über den Cursor und Ergebnis Satz benötigten temporären Ressourcen verwaltet. Die clientseitige Anwendung kann das gesamte Resultset, um zu bestimmen, welche Zeilen dafür durchsuchen.  
  
 Statische und keysetgesteuerte clientseitige Cursor können eine deutliche Auslastung auf der Arbeitsstation platzieren, wenn sie zu viele Zeilen enthalten. Während aller Cursorbibliotheken zum Erstellen von Cursorn mit Tausenden von Zeilen sind, können Anwendungen entwickelt, um solche umfangreiche Rowsets fetch unbefriedigend. Es gibt natürlich Ausnahmen. Bei einigen Anwendungen ist möglicherweise für ein großer clientseitigen Cursor perfekt geeignet und Leistung möglicherweise ein Problem nicht.  
  
 Ein Hauptvorteil des clientseitigen Cursors ist die schnelle Reaktion. Nachdem das Resultset auf den Clientcomputer heruntergeladen wurde, ist das Durchsuchen, mit die Zeilen sehr schnell. Ihre Anwendung ist im Allgemeinen stärker skalierbare mit clientseitigen Cursorn, da ressourcenanforderungen den Cursor auf jedem Client separate und nicht auf dem Server platziert werden.  
  
## <a name="server-side-cursors"></a>Serverseitiger Cursor  
 Rufen Sie in ADO für einen serverseitigen Cursor durch Verwenden der **AdUseServer CursorLocationEnum.** Mit einem serverseitigen Cursor verwaltet der Server das Resultset mit Ressourcen, die vom Server-Computer bereitgestellt. Der serverseitige Cursor gibt nur die angeforderten Daten zurück, über das Netzwerk. Diese Art von Cursor bieten manchmal eine bessere Leistung als die clientseitigen Cursor verwenden, besonders in Situationen, in denen zu übermäßigem Netzwerkverkehr ein Problem darstellt.  
  
 Allerdings ist es wichtig, die darauf hinweisen, dass ein serverseitiger Cursor ist, zumindest vorübergehend – für jeden aktiven Client wertvolle Serverressourcen belegt. Sie müssen entsprechend planen, um sicherzustellen, dass Ihre Serverhardware Verwalten aller die serverseitige Cursor von aktiven Clients angefordert wird. Darüber hinaus ein serverseitigen Cursor kann langsam sein, da sie nur Zugriff auf einzelne Zeilen enthält – kein Batch-Cursor vorhanden ist.  
  
 Serverseitige Cursor sind hilfreich, wenn einfügen, aktualisieren oder Löschen von Datensätzen. Mit serverseitiger Cursor haben Sie mehrere aktive Anweisungen über die gleiche Verbindung.
