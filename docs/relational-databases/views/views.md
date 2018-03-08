---
title: Sichten | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: views
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-views
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- views [SQL Server], about views
ms.assetid: ada83c28-e8b7-45d9-b53c-b3d67c8820c8
caps.latest.revision: 
author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7ba650c638d855556ec2afe992f26ff3f6ad2460
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="views"></a>Sichten
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]
Eine Sicht ist eine virtuelle Tabelle, deren Inhalt durch eine Abfrage definiert wird. Wie bei einer Tabelle besteht auch eine Sicht aus einem Satz benannter Spalten und Zeilen mit Daten. Wenn sie nicht indiziert ist, liegt eine Sicht jedoch nicht als gespeicherter Satz von Datenwerten in einer Datenbank vor. Die Zeilen und Spalten mit Daten stammen aus Tabellen, auf die in der die Sicht definierenden Abfrage verwiesen wird. Diese Datenzeilen und -spalten werden dynamisch erstellt, wenn auf die Sicht verwiesen wird.  
  
 Eine Sicht dient als Filter für die zugrunde liegenden Tabellen, auf die in der Sicht verwiesen wird. Die Abfrage, die die Sicht definiert, kann Daten aus einer oder mehreren Tabellen oder aus anderen Sichten in der aktuellen Datenbank oder anderen Datenbanken verwenden. Sie können darüber hinaus verteilte Abfragen verwenden, um Sichten zu definieren, die Daten aus mehreren heterogenen Quellen verwenden. Dies kann z. B. dann hilfreich sein, wenn Sie Daten mit gleicher Struktur kombinieren möchten, die sich jedoch auf unterschiedlichen Servern befinden, wobei auf jedem Server die Daten für einen anderen Bereich Ihrer Organisation gespeichert sind.  
  
 Im Allgemeinen werden Sichten verwendet, um die Darstellung einer Datenbank für die einzelnen Benutzer einzuschränken, zu vereinfachen und anzupassen. Sichten können als Sicherheitsmechanismen verwendet werden, da Benutzern der Zugriff auf Daten über Sichten ermöglicht werden kann, ohne diesen Benutzern jedoch die Berechtigungen für den direkten Zugriff auf die der Sicht zugrunde liegenden Basistabellen zu gewähren. Sichten können verwendet werden, um eine abwärtskompatible Schnittstelle zum Emulieren einer Tabelle bereitzustellen, die zuvor vorhanden war, aber deren Schema geändert wurde. Sichten können auch beim Kopieren von Daten nach und von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden, um die Leistung zu verbessern oder Daten zu partitionieren.  
  
## <a name="types-of-views"></a>Sichttypen  
 Neben der Standardrolle der grundlegenden benutzerdefinierten Sichten bietet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die folgenden Typen von Sichten, die innerhalb einer Datenbank speziellen Zwecken dienen:  
  
 Indizierte Sichten  
 Eine indizierte Sicht ist eine Sicht, die materialisiert wurde. Dies bedeutet, dass die Sichtdefinition berechnet und die resultierenden Daten so wie eine Tabelle gespeichert wurden. Sie indizieren eine Sicht, indem Sie einen eindeutigen gruppierten Index für sie erstellen. Indizierte Sichten können die Leistung einiger Abfragetypen deutlich verbessern. Indizierte Sichten funktionieren am besten für Abfragen, die viele Zeilen aggregieren. Sie eignen sich nicht gut für zugrunde liegende Datasets, die häufig aktualisiert werden.  
  
 Partitionierte Sichten  
 Mithilfe einer partitionierte Sicht werden partitionierte Daten aus einem Satz von Elementtabellen über einen oder mehrere Server hinweg horizontal verknüpft. Die Daten werden so dargestellt, als würden sie aus einer Tabelle stammen. Eine Sicht, die Elementtabellen für die gleiche Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verknüpft, ist eine lokale partitionierte Sicht.  
  
 Systemsichten  
 Systemsichten machen Katalogmetadaten verfügbar. Mithilfe von Systemsichten können Sie Informationen zu der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder den Objekten zurückgeben, die in der Instanz definiert wurden. Sie können z.B. die sys.databases-Katalogsicht abfragen, um Informationen zu den benutzerdefinierten Datenbanken zurückzugeben, die in der Instanz verfügbar sind. Weitere Informationen finden Sie unter [Systemsichten &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90).  
  
## <a name="common-view-tasks"></a>Allgemeine Sichttasks  
 Die folgende Tabelle enthält Links zu häufigen Tasks im Zusammenhang mit der Erstellung und Änderung von Sichten.  
  
|Anzeigen von Tasks|Thema|  
|----------------|-----------|  
|Beschreibt, wie eine Sicht erstellt wird.|[Erstellen von Sichten](../../relational-databases/views/create-views.md)|  
|Beschreibt, wie eine indizierte Sicht erstellt wird.|[Erstellen von indizierten Sichten](../../relational-databases/views/create-indexed-views.md)|  
|Beschreibt, wie die Sichtdefinition geändert wird.|[Ändern von Sichten](../../relational-databases/views/modify-views.md)|  
|Beschreibt, wie Daten durch eine Sicht geändert werden.|[Ändern von Daten über eine Sicht](../../relational-databases/views/modify-data-through-a-view.md)|  
|Beschreibt, wie eine Sicht gelöscht wird.|[Löschen von Sichten](../../relational-databases/views/delete-views.md)|  
|Beschreibt, wie Informationen zu einer Sicht, z. B. die Sichtdefinition, zurückgegeben werden.|[Abrufen von Informationen zu einer Sicht](../../relational-databases/views/get-information-about-a-view.md)|  
|Beschreibt, wie eine Sicht umbenannt wird.|[Umbenennen von Sichten](../../relational-databases/views/rename-views.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen von Sichten über XML-Spalten](../../relational-databases/xml/create-views-over-xml-columns.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)  
  
  
