---
title: Verwalten von Transaktionen (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d34410453fea22927b36ed7791830f170a0a3a09
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="managing-transactions-xmla"></a>Verwalten von Transaktionen (XMLA)
  Jeder Befehl XML for Analysis (XMLA) gesendet, um eine Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] im Kontext einer Transaktion auf der aktuellen impliziten oder expliziten Sitzung ausgeführt wird. Um alle diese Transaktionen zu verwalten, verwenden Sie die [BeginTransaction](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [CommitTransaction](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), und [RollbackTransaction](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md) Befehle. Durch die Verwendung dieser Befehle können Sie implizite oder explizite Transaktionen erstellen, den Verweiszähler der Transaktion ändern, Transaktionen starten sowie einen Commit oder ein Rollback für diese Transaktionen ausführen.  
  
## <a name="implicit-and-explicit-transactions"></a>Implizite und explizite Transaktionen  
 Eine Transaktion ist entweder implizit oder explizit:  
  
 **Implizite Transaktion**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erstellt ein *implizite* Transaktion für einen XMLA-Befehl, falls die **BeginTransaction** Befehl gibt den Beginn einer Transaktion. Wenn der Befehl erfolgreich ist, führt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] immer einen Commit für die implizite Transaktionen aus, und wenn der Befehl einen Fehler generiert, wird ein Rollback für die implizite Transaktion ausgeführt.  
  
 **Explizite Transaktion**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erstellt ein *explizite* Transaktion Wenn die **BeginTransaction** Befehl startet eine Transaktion. Allerdings [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] führt nur eine explizite Transaktion aus, wenn eine **CommitTransaction** Befehl gesendet wird und ein Rollback für eine explizite Transaktion aus, wenn eine **RollbackTransaction** -Befehl gesendet wird.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] führt zudem ein Rollback sowohl für implizite als auch für explizite Transaktionen aus, wenn die aktuelle Sitzung beendet wird, bevor die aktive Transaktion fertiggestellt wird.  
  
## <a name="transactions-and-reference-counts"></a>Transaktionen und Verweiszähler  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwaltet einen Transaktionsverweiszähler für jede Sitzung. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] unterstützt jedoch keine geschachtelten Transaktionen, da nur eine aktive Transaktion pro Sitzung verwaltet wird. Wenn die aktuelle Sitzung keine aktive Transaktion besitzt, wird der Transaktionsverweiszähler auf null festgelegt.  
  
 Das heißt, jede **BeginTransaction** Befehl inkrementiert den Verweiszähler um eins, während jeder **CommitTransaction** Befehl dekrementiert den Verweiszähler um eins. Wenn eine **CommitTransaction** Befehl wird die Transaktionsanzahl auf 0 (null), [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] führt einen Commit der Transaktion.  
  
 Allerdings die **RollbackTransaction** Befehl setzt die aktive Transaktion unabhängig von den aktuellen Wert der Verweiszähler der Transaktion zurück. Das heißt, eine einzelne **RollbackTransaction** Befehl Rollback für die aktive Transaktion, unabhängig davon, wie viele **BeginTransaction** Befehle oder **CommitTransaction** Befehle gesendet wurden, und legt den transaktionsverweiszähler auf NULL fest.  
  
## <a name="beginning-a-transaction"></a>Beginnen einer Transaktion  
 Die **BeginTransaction** Befehl beginnt eine explizite Transaktion für die aktuelle Sitzung und erhöht den transaktionsverweiszähler für die aktuelle Sitzung um eins. Alle nachfolgenden Befehle gelten als innerhalb der aktiven Transaktion, bis entweder genug **CommitTransaction** Befehle werden an die aktive Transaktion oder einer einzelnen commit geschickt **RollbackTransaction**Befehl wird die aktive Transaktion ein Rollback gesendet.  
  
## <a name="committing-a-transaction"></a>Commitausführung für eine Transaktion  
 Die **CommitTransaction** Befehl führt einen Commit für die Ergebnisse von Befehlen, die ausgeführt werden, nachdem die **BeginTransaction** -Befehl für die aktuelle Sitzung ausgeführt wurde. Jede **CommitTransaction** -Befehl verringert den Verweiszähler für aktive Transaktionen auf eine Sitzung. Wenn eine **CommitTransaction** Befehl wird den Verweiszähler auf 0 (null), [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] führt einen Commit für die aktive Transaktion. Wenn keine aktive Transaktion vorhanden ist (also der transaktionsverweiszähler für die aktuelle Sitzung bereits festgelegt ist, 0 (null)), eine **CommitTransaction** Befehl führt zu einem Fehler.  
  
## <a name="rolling-back-a-transaction"></a>Ausführen von Rollbacks für eine Transaktion  
 Die **RollbackTransaction** Befehl Rollback für die Ergebnisse von Befehlen, die ausgeführt werden, nachdem die **BeginTransaction** -Befehl für die aktuelle Sitzung ausgeführt wurde. Die **RollbackTransaction** Befehl die aktive Transaktion, unabhängig von der aktuellen transaktionsverweiszähler ein Rollback und legt den transaktionsverweiszähler auf NULL fest. Wenn keine aktive Transaktion vorhanden ist (also der transaktionsverweiszähler für die aktuelle Sitzung bereits festgelegt ist, 0 (null)), eine **RollbackTransaction** Befehl führt zu einem Fehler.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
