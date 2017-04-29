---
title: "Transaktionsprotokollspeicherplatz für Indexvorgänge | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index disk space [SQL Server]
- space [SQL Server], indexes
- transaction logs [SQL Server], disk space
- disk space [SQL Server], transaction logs
- space [SQL Server], transaction logs
ms.assetid: 4f8a4922-4507-4072-be67-c690528d5c3b
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a1d06fd19479d11e1705e6c21ed7e1698a89896a
ms.lasthandoff: 04/11/2017

---
# <a name="transaction-log-disk-space-for-index-operations"></a>Transaktionsprotokollspeicherplatz für Indexvorgänge
  Umfangreiche Indexvorgänge können riesige Datenmengen erzeugen, die zu einem schnellen Füllen des Transaktionsprotokolls führen können. Um sicherzustellen, dass ein Rollback des Indexvorgangs möglich ist, kann das Transaktionsprotokoll nicht abgeschnitten werden, bis der Indexvorgang abgeschlossen ist. Die Sicherung des Protokolls während des Indexvorgangs ist jedoch möglich. Deshalb muss das Transaktionsprotokoll über ausreichend Speicherplatz verfügen, um sowohl die Transaktionen des Indexvorgangs als auch alle gleichzeitigen Benutzertransaktionen für die Dauer des Indexvorgangs aufnehmen zu können. Das gilt sowohl für Offline- als auch für Onlineindexvorgänge. Da während eines Offlineindexvorgangs der Zugriff auf die zugrunde liegenden Tabellen nicht möglich ist, treten dabei evtl. nur wenige Benutzertransaktionen auf, und das Protokoll wächst nicht so schnell an. Bei Onlineindexvorgängen erfolgt jedoch keinerlei Einschränkung von gleichzeitigen Benutzeraktivitäten. Daher können umfangreiche Onlineindexvorgänge in Kombination mit zahlreichen gleichzeitigen Benutzertransaktionen zu einem kontinuierlichen Anwachsen des Transaktionsprotokolls führen, ohne dass es eine Möglichkeit zum Abschneiden des Protokolls gibt.  
  
## <a name="recommendations"></a>Empfehlungen  
 Beim Ausführen umfangreicher Indexvorgänge sollten Sie die folgenden Empfehlungen beachten:  
  
1.  Stellen Sie sicher, dass das Transaktionsprotokoll gesichert und abgeschnitten wurde, bevor Sie umfangreiche Onlineindexvorgänge ausführen. Außerdem muss das Protokoll über ausreichend Speicherplatz verfügen können, um den vorgesehenen Index und die Benutzertransaktionen speichern zu können.  
  
2.  Setzen Sie die Option SORT_IN_TEMPDB für den Indexvorgang eventuell auf ON. Damit werden die Indextransaktionen von den gleichzeitigen Benutzertransaktionen getrennt. Die Indextransaktionen werden dann im Transaktionsprotokoll **tempdb** gespeichert, während die gleichzeitigen Benutzertransaktionen im Protokoll der Benutzerdatenbank gespeichert werden. Damit kann das Transaktionsprotokoll der Benutzerdatenbank bei Bedarf während des Indexvorgangs abgeschnitten werden. Wenn Sich das Protokoll **tempdb** außerdem auf einem anderen Datenträger als das Datenbankprotokoll befindet, konkurrieren die beiden Protokolle nicht um Speicherplatz auf demselben Datenträger.  
  
    > [!NOTE]  
    >  Überprüfen Sie, dass die Datenbank **tempdb** und das Transaktionsprotokoll über ausreichend Speicherplatz zur Durchführung des Indexvorgangs verfügen. Das **tempdb** -Transaktionsprotokoll kann nicht abgeschnitten werden, so lange der Indexvorgang noch nicht abgeschlossen ist.  
  
3.  Verwenden Sie ein Datenbankwiederherstellungsmodell, das eine minimale Protokollierung des Indexvorgangs zulässt. Damit kann die Größe des Protokolls verringert und das vollständige Füllen des Speicherplatzes durch das Protokoll verhindert werden.  
  
4.  Führen Sie den Onlineindexvorgang nicht in einer expliziten Transaktion aus. Das Protokoll wird nicht abgeschnitten, bis die explizite Transaktion abgeschlossen ist.  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Speicherplatzanforderungen für Index-DDL-Vorgänge](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [Beispiel für den zum Speichern eines Indexes belegten Speicherplatz](../../relational-databases/indexes/index-disk-space-example.md)  
  
  
