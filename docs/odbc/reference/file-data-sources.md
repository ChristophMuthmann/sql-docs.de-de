---
title: Datei-Datenquellen | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 254e859c8533625cb34f7d867c62f26bea5cd04d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="file-data-sources"></a>Dateidatenquellen
*Datei-Datenquellen* werden in einer Datei gespeichert und ermöglichen Sie Verbindungsinformationen wiederholt durch einen einzelnen Benutzer verwendet oder von mehreren Benutzern gemeinsam genutzt werden. Wenn eine Datei als Datenquelle verwendet wird, stellt der Treiber-Manager die Verbindung mit der Datenquelle anhand der Informationen in einem DSN-Datei her. Diese Datei kann wie jede andere Datei bearbeitet werden. Eine Datei als Datenquelle einen Datenquellennamen keinen ist eine Datenquelle für den Computer, und nicht auf einen Benutzer oder Computer registriert ist.  
  
 Eine Dateidatenquelle den Verbindungsprozess optimiert, da die DSN-Datei die Verbindungszeichenfolge enthält, die sonst für einen Aufruf erstellt werden sollen die **SQLDriverConnect** Funktion. Ein weiterer Vorteil von DSN-Datei ist, dass es auf jedem Computer kopiert werden kann, damit identische Datenquellen an, die von vielen Computern verwendet werden können, solange sie den entsprechenden Treiber installiert haben. Eine Dateidatenquelle kann auch von Anwendungen gemeinsam genutzt werden. Eine freigegebenes Dateidatenquelle kann in einem Netzwerk platziert und gleichzeitig von mehreren Anwendungen verwendet werden.  
  
 DSN-Datei kann auch Dateidatenquelle sein. Eine Dateidatenquelle DSN-Datei befindet sich auf einem einzelnen Computer und verweist auf eine Computer-Datenquelle. Dateidatenquelle vorhanden hauptsächlich, dass die einfache Konvertierung von Datenquellen für Computer in Dateidatenquellen zulassen, damit eine Anwendung ausschließlich mit Dateidatenquellen entworfen werden kann. Wenn der Treiber-Manager die Informationen in eine Dateidatenquelle gesendet wird, wird eine Verbindung nach Bedarf, um die Computer-Datenquelle, der auf die DSN-Datei verweist.  
  
 Weitere Informationen zu Datenquellen finden Sie unter [Herstellen einer Verbindung mithilfe von Dateidatenquellen](../../odbc/reference/develop-app/connecting-using-file-data-sources.md), oder die [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) funktionsbeschreibung.
