---
title: Abfragen und Aktualisieren von Visual FoxPro-Daten aus Microsoft Access | Microsoft Docs
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
- querying Visual FoxPro data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], querying and updating
- updating Visual FoxPro data [ODBC]
ms.assetid: 2d314e78-9edf-44b2-bd8b-96784236bcbe
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6eefdf130a261945a17c9ec557235b65ab7133fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>Abfragen und Aktualisieren von Visual FoxPro-Daten aus Microsoft Access
Sie können Abfragen und Aktualisieren von Daten in einer Visual FoxPro-Datenbank aus einer Microsoft Access-Datenbank gespeichert werden, mithilfe der Option Tabelle verknüpfen.  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>So verknüpfen Sie eine Visual FoxPro-Datenbank mit einer Microsoft Access-Datenbank  
  
1.  Öffnen Sie eine Microsoft Access-Datenbank.  
  
2.  Klicken Sie auf "Neu", auf der Registerkarte "Tabellen".  
  
3.  Klicken Sie im Dialogfeld neue Tabelle wählen Sie Tabelle verknüpfen, und klicken Sie auf OK.  
  
4.  Wählen Sie im Dialogfeld Link ODBC-Datenbank in der Liste aus.  
  
5.  Wählen Sie im Dialogfeld SQL-Datenquellen die Datenquelle, die Verbindung mit der Visual FoxPro-Daten, die Sie verwenden möchten, Fragen, und klicken Sie auf OK.  
  
6.  Wählen Sie im Dialogfeld Verknüpfungstabellen die Tabellen, die Sie verwenden möchten, Abfragen und aktualisieren, und klicken Sie auf OK. Die verknüpften Visual FoxPro-Tabellen werden in der Registerkarte "Tabellen" der Microsoft Access-Datenbank angezeigt.  
  
 Sie können jetzt Microsoft Access verwenden, Abfragen und Aktualisieren von Daten in den verknüpften Visual FoxPro-Tabellen. Vorgenommenen Änderungen an verknüpften Daten werden in der Visual FoxPro-Datenquelle gesendet.  
  
 Wenn Sie nicht, dass Änderungen möchten, stellen Sie in Microsoft Access Einfluss auf die Daten in der Visual FoxPro-Datenquelle, finden Sie unter [importieren Visual FoxPro-Daten in Microsoft Access](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md).
