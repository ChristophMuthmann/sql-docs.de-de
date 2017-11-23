---
title: Anweisungen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: d8d6f62a-e815-425c-a80e-a63fd34ec275
caps.latest.revision: "7"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: e6e36b056aaca063970c81d2932ec47ee7cef29e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="transact-sql-statements"></a>Transact-SQL-Anweisungen
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

In diesem Referenzthema werden die Kategorien von Anweisungen für die Verwendung mit Transact-SQL (T-SQL) zusammengefasst. Sie finden alle Anweisungen im linken Navigationsbereich aufgeführt.

## <a name="backup-and-restore"></a>Sichern und Wiederherstellen
Die Backup- und Restore-Anweisungen bieten Möglichkeiten zum Erstellen von Sicherungen und Wiederherstellen von Sicherungen.  Weitere Informationen finden Sie unter der [Übersicht über die Sicherung und Wiederherstellung](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).

## <a name="data-definition-language"></a>Datendefinitionssprache
Anweisungen von Data Definition Language (DDL) werden Datenstrukturen definiert. Verwenden Sie die Anweisungen zum Erstellen, ändern oder Löschen von Datenstrukturen in einer Datenbank.
- ALTER
- Sortierungen
- CREATE
- DROP
- TRIGGER DEAKTIVIEREN
- ENABLE TRIGGER
- UMBENENNEN
- UPDATE STATISTICS

## <a name="data-manipulation-language"></a>Datenbearbeitungssprache
(Data Manipulation Language, DML) wirken sich auf die Informationen in der Datenbank gespeichert. Verwenden Sie diese Anweisungen, um Einfüge-, Update- und ändern Sie die Zeilen in der Datenbank.

- BULK INSERT
- DELETE
- INSERT
- MERGE
- TRUNCATE TABLE

## <a name="permissions-statements"></a>Berechtigungen-Anweisungen
Berechtigungen Anweisungen ermitteln, welche Benutzer und Anmeldenamen den Zugriff auf Daten und Vorgänge ausführen können. Weitere Informationen zur Authentifizierung und Zugriff finden Sie unter der [Sicherheitscenter](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## <a name="service-broker-statements"></a>Service Broker-Anweisungen
Service Broker ist ein Feature, die systemeigene Unterstützung für Messaging-und warteschlangenanwendungen bereitstellt. Weitere Informationen finden Sie unter [Service Broker](../../relational-databases/service-broker/event-notifications.md).

## <a name="session-settings"></a>Sitzungseinstellungen
SET-Anweisungen bestimmen, wie die aktuelle Sitzung Handles Uhrzeiteinstellungen ausgeführt. Eine Übersicht finden Sie unter [SET-Anweisungen](set-statements-transact-sql.md).
