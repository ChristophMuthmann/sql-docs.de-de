---
title: "Anforderungen für die CLR User-Defined Aggregate | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- user-defined types [CLR integration], user-defined aggregates
- CREATE AGGREGATE statement
- SqlUserDefinedAggregate attribute
- aggregate methods [CLR integration]
- assemblies [CLR integration], user-defined aggregate functions
- custom aggregates [CLR integration]
- user-defined functions [CLR integration]
- UDTs [CLR integration], user-defined aggregates
ms.assetid: dbf9eb5a-bd99-42f7-b275-556d0def045d
caps.latest.revision: "56"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 158b2aaa95f289a558f0d186e359903252f6d90e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="clr-user-defined-aggregates---requirements"></a>CLR User-Defined Aggregate - Anforderungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Ein Typ in einer Assembly der common Language Runtime (CLR) kann als eine benutzerdefinierte Aggregatfunktion registriert werden, solange den erforderliche Aggregationsvertrag implementiert. Dieser Vertrag besteht aus den **SqlUserDefinedAggregate** Attribut und der Aggregation Vertrag Methoden. Der Aggregationsvertrag beinhaltet den Mechanismus zum Speichern des Zwischenstatus der Aggregation und der Mechanismus zum Sammeln neuer Werte, besteht aus vier Methoden: **Init**, **Accumulate**,  **Merge**, und **beenden**. Wenn Sie diese Anforderungen erfüllt haben, werden benutzerdefinierte Aggregate in voll nutzen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die folgenden Abschnitte zu diesem Thema enthalten zusätzliche Details zum Erstellen von benutzerdefinierten Aggregaten und ihrer Verwendungsweise. Ein Beispiel finden Sie unter [Invoking CLR User-Defined Aggregatfunktionen](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md).  
  
## <a name="sqluserdefinedaggregate"></a>SqlUserDefinedAggregate  
 Weitere Informationen finden Sie unter [SqlUserDefinedAggregateAttribute](http://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="aggregation-methods"></a>Aggregationsmethoden  
 Die als benutzerdefiniertes Aggregat registrierte Klasse muss die folgenden Instanzmethoden unterstützen. Diese Methoden werden vom Abfrageprozessor verwendet, um die Aggregation zu berechnen:  
  
|Methode|Syntax|Description|  
|------------|------------|-----------------|  
|**Init**|`public void Init();`|Der Abfrageprozessor verwendet diese Methode, um die Berechnung der Aggregation zu initialisieren. Diese Methode wird einmal für jede Gruppe aufgerufen, die der Abfrageprozessor aggregiert. Der Abfrageprozessor verwendet möglicherweise dieselbe Instanz der Aggregatklasse mehrfach, um Aggregate für mehrere Gruppen zu berechnen. Die **Init** Methode führen Sie nach der vorherigen Verwendung dieser Instanz Bereinigung nach Bedarf, und aktivieren Sie ihn eine weiteren aggregatberechnung neu zu starten.|  
|**Sammeln**|`public void Accumulate ( input-type value[, input-type value, ...]);`|Ein oder mehrere Parameter, die die Parameter der Funktion darstellen. *INPUT_TYPE* muss die verwaltete [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und dem systemeigenen Datentyp [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angegebenen Datentyp *Input_sqltype* in der **CREATE AGGREGATE** Anweisung . Weitere Informationen finden Sie unter [Zuordnen von CLR-Parameterdaten](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).<br /><br /> Für benutzerdefinierte Typen (User-Defined Types, UDTs) entspricht der Eingabetyp dem UDT-Typ. Der Abfrageprozessor verwendet diese Methode, um die Aggregatwerte zu sammeln. Sie wird einmal für jeden Wert in der zu aggregierenden Gruppe aufgerufen. Der Abfrageprozessor ruft diese immer nur nach dem Aufruf der **Init** Methode für die jeweilige Instanz der Aggregatklasse. Durch die Implementierung dieser Methode wird der Instanzstatus auf den momentanen Stand der übergebenen Argumentwertansammlung aktualisiert.|  
|**Merge**|`public void Merge( udagg_class value);`|Diese Methode kann verwendet werden, um eine andere Instanz dieser Aggregatklasse mit der aktuellen Instanz zusammenzuführen. Der Abfrageprozessor verwendet diese Methode, um mehrere Teilberechnungen einer Aggregation zusammenzuführen.|  
|**Beenden**|`public return_type Terminate();`|Diese Methode schließt die Aggregatberechnung ab und gibt das Ergebnis der Aggregation zurück. Die *Return_type* muss ein verwaltetes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp, der verwaltete Entsprechung *Return_sqltype* angegebenen, in der **CREATE AGGREGATE** Anweisung. Die *Return_type* kann auch ein benutzerdefinierten Typ sein.|  
  
### <a name="table-valued-parameters"></a>Tabellenwertparameter  
 Tabellenwertparameter (Table Valued Parameters, TVPs), benutzerdefinierte Tabellentypen, die an eine Prozedur oder Funktion übergeben werden, bieten eine effiziente Methode zum Übergeben mehrerer Datenzeilen an den Server. TVPs verfügen über eine ähnliche Funktionalität wie Parameterarrays, bieten aber größere Flexibilität und engere Integration mit [!INCLUDE[tsql](../../includes/tsql-md.md)]. Außerdem verfügen sie auch über ein besseres Leistungspotenzial. TVPs helfen auch, die Anzahl von Roundtrips zum Server zu reduzieren. Anstatt mehrere Anforderungen an den Server zu senden, z. B. mit einer Liste von skalaren Parametern, können Daten als TVP an den Server gesendet werden. Ein benutzerdefinierter Tabellentyp kann nicht als Tabellenwertparameter an eine verwaltete gespeicherte Prozedur oder Funktion übergeben werden, die im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozess ausgeführt wird, oder von einer solchen Prozedur oder Funktion zurückgegeben werden. Auch können TVPs nicht innerhalb des Bereichs einer Kontextverbindung verwendet werden. Allerdings kann ein TVP, sofern er nicht als Kontextverbindung verwendet wird, mit SqlClient in verwalteten gespeicherten Prozeduren oder Funktionen verwendet werden, die im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozess ausgeführt werden. Die Verbindung kann zum gleichen Server erfolgen, der die verwaltete Prozedur oder Funktion ausführt. Weitere Informationen zu TVPs finden Sie unter [Tabellenwertparametern &#40; Datenbankmodul &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="change-history"></a>Änderungsverlauf  
  
|Aktualisierter Inhalt|  
|---------------------|  
|Aktualisiert die Beschreibung des der **Accumulate** Methode; sie jetzt mehrere Parameter akzeptiert.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Benutzerdefinierte CLR-Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Aufrufen von CLR-benutzerdefinierten Aggregatfunktionen](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
  
  
