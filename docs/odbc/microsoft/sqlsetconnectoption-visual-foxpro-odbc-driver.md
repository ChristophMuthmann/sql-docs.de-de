---
title: SQLSetConnectOption (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
- SQLSetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5a35449e-4694-4ee5-9fa1-45d5a8fe7823
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf786b51ad01bd3f61bdfcbafda23347db4c3aba
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: Partial  
  
 ODBC-API-Konformität: Ebene 1  
  
 Legt Optionen fest, die Aspekte der Verbindungen zu steuern. Diese Funktion wird teilweise unterstützt: der Treiber unterstützt alle Werte für die *fOption* Argument, aber einige der nicht unterstützt *vParam* Werte für die *fOption* Argument SQL_TXN_ISOLATION.  
  
 Die folgende Tabelle beschreibt nur die Argumente mit der Visual FoxPro-ODBC-Treiber-Implementierung von Verhalten **SQLSetConnectOption**.  
  
|*fOption*|Hinweise|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Bei Auswahl von SQL_AUTOCOMMIT_OFF festlegen, die Anwendung muss explizit einen commit oder Rollback Transaktionen mit [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); der Visual FoxPro-ODBC-Treiber nicht automatisch nach dem Abschluss eine transaktionsfähige-Anweisung fest. Der Treiber beginnt eine Transaktion aus, wenn die Anweisung transaktionsfähige ist.|  
|SQL_CURRENT_QUALIFIER|Kann entweder eine vollständig qualifiziert [Datenbank](../../odbc/microsoft/visual-foxpro-terminology.md) Namen oder den vollqualifizierten Pfad zu einem Verzeichnis mit NULL oder mehr [frei Tabellen](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SQL_LOGINTIMEOUT|Gibt "Treiber nicht unterstützt"-Fehler zurück.|  
|SQL_CURSORS|Gibt "Treiber nicht unterstützt"-Fehler zurück.|  
|SQL_PACKET_SIZE|Gibt "Treiber nicht unterstützt"-Fehler zurück.|  
|SQL_TXN_ISOLATION|Der Treiber kann nur SQL_TXN_READ_COMMITTED.<br /><br /> Die folgenden *vParam*s werden nicht unterstützt:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE FESTGELEGT SIND|  
  
 Weitere Informationen finden Sie unter [SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md) in der *ODBC Programmer's Reference*.
