---
title: NULL-SET-Befehls | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1050db2b6a50fc794626b6017bd26af05f458a8a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="set-null-command"></a>SET NULL-Befehl
Bestimmt, wie null-Werte, durch die ALTER TABLE - SQL, CREATE TABLE - SQL und INSERT unterstützt werden - SQL-Befehle.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>Argumente  
 ON  
 (Standard für den Treiber; der Standardwert für Visual FoxPro ist OFF). Gibt an, dass alle Spalten in einer Tabelle mit ALTER TABLE und CREATE TABLE erstellt null-Werte zulässt. Sie können null-Wert-Unterstützung für Spalten in der Tabelle überschreiben, indem Sie z. B. die NOT NULL-Klausel in den Definitionen der Spalten.  
  
 Gibt auch an, dass INSERT - SQL null-Werte in Spalten nicht in der INSERT - Wert für das SQL-Klausel enthalten eingefügt wird. INSERT - wird SQL null-Werte nur in Spalten einzufügen, die null-Werte zulassen.  
  
 OFF  
 Gibt an, dass alle Spalten in einer Tabelle mit ALTER TABLE und CREATE TABLE erstellt keine null-Werte zulassen. Legen Sie null-Wert-Unterstützung für Spalten in der ALTER TABLE und CREATE TABLE, indem Sie z. B. die NULL-Klausel in den Definitionen der Spalten.  
  
 Gibt auch an, dass INSERT - SQL leere Werten in Spalten nicht in der INSERT - Wert für das SQL-Klausel enthalten eingefügt wird.  
  
## <a name="remarks"></a>Hinweise  
 SET NULL beeinflusst nur wie null-Werte werden von ALTER TABLE, CREATE TABLE und INSERT - SQL unterstützt. Andere Befehle sind nicht betroffen von NULL festgelegt.  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE - SQL-Befehl](../../odbc/microsoft/alter-table-sql-command.md)   
 [Erstellen der Tabelle - SQL-Befehl](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT (SQL-Befehl)](../../odbc/microsoft/insert-sql-command.md)
