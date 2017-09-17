---
title: Format der Verbindungszeichenfolge und Attribute | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection strings [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connection strings
ms.assetid: 0c360112-8720-4e54-a1a6-b9b18d943557
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 79d5cabb884262b052429da53cf19c360048dd21
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="connection-string-format-and-attributes"></a>Format der Verbindungszeichenfolge und Attribute
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Anstatt ein Dialogfeld zu verwenden, erfordern einige Anwendungen möglicherweise eine Verbindungszeichenfolge, die Datenquellen-Verbindungsinformationen angibt. Die Verbindungszeichenfolge besteht aus einer Anzahl von Attributen, die angeben, wie ein Treiber eine Verbindung mit einer Datenquelle herstellt. Ein Attribut identifiziert eine bestimmte Information, die der Treiber muss wissen, kann er die entsprechenden datenquellenverbindung treffen. Jeder Treiber möglicherweise einen anderen Satz von Attributen, aber das Verbindungszeichenfolgenformat ist immer gleich. Eine Verbindungszeichenfolge weist das folgende Format:  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Der Microsoft ODBC-Treiber für Oracle unterstützt das Verbindungszeichenfolgenformat der ersten Version des Treibers, der verwendet `CONNECTSTRING`anstelle von = `SERVER=`.  
  
 Wenn Sie ein Datenquellenanbieter, die Windows-Authentifizierung unterstützt Verbindung, müssen Sie angeben `Trusted_Connection=yes` anstelle von Benutzerinformationen-ID und Kennwort in der Verbindungszeichenfolge angegeben.  
  
 Sie müssen die Datenquelle angeben name, sofern Sie nicht die UID, PWD, SERVER (oder CONNECTSTRING) angeben und Treiber-Attribute. Alle anderen Attribute sind jedoch optional. Wenn Sie ein Attribut nicht angeben, dieses Attribut standardmäßig in der entsprechenden DSN-Registerkarte des angegebenen der **ODBC-Datenquellenadministrator** (Dialogfeld). Der Attributwert kann Groß-/Kleinschreibung beachtet werden.  
  
 Die Attribute für die Verbindungszeichenfolge sind wie folgt aus:  
  
|Attribut|Description|Standardwert|  
|---------------|-----------------|-------------------|  
|DSN|Der Name der Datenquelle aufgeführt, in der Registerkarte "Treiber" der **ODBC-Datenquellenadministrator** (Dialogfeld).|""|  
|PWD|Das Kennwort für den Oracle-Server, die Sie zugreifen möchten. Dieser Treiber unterstützt die Einschränkungen, die Oracle auf Kennwörter ablegt.|""|  
|SERVER|Die Verbindungszeichenfolge für den Oracle-Server, die Sie zugreifen möchten.|""|  
|UID|Der Name des Oracle-Server. Je nach System, dieses Attribut kann nicht ausgelassen werden – d. h. bestimmte Datenbanken und Tabellen möglicherweise dieses Attribut aus Sicherheitsgründen.<br /><br /> Verwenden Sie "/" Oracle Verwendung des System-Authentifizierung funktioniert.|""|  
|BUFFERSIZE|Die optimale Puffergröße verwendet, wenn die Spalten abrufen.<br /><br /> Der Treiber wird optimiert, abrufen, sodass ein Abrufen von Daten aus dem Oracle-Server genügend Zeilen aus, um einen Puffer dieser Größe füllen zurückgegeben. Größere Werte tendenziell Leistung zu steigern, wenn Sie eine große Datenmenge abrufen.|65535|  
|SYNONYMCOLUMNS|Wenn dieser Wert ist "true" (1), ein SQLSpalten-()-API-Aufruf gibt Spalteninformationen zurück. Andernfalls wird SQLSpalten-() nur die Spalten für Tabellen und Sichten zurückgegeben. Der ODBC-Treiber für Oracle bietet schnelleren Zugriff auf, wenn dieser Wert nicht festgelegt ist.|1|  
|REMARKS|Wenn dieser Wert ist "true" (1), gibt der Treiber "Hinweise" Spalten für die [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) Resultset. Der ODBC-Treiber für Oracle bietet schnelleren Zugriff auf, wenn dieser Wert nicht festgelegt ist.|0|  
|StdDayOfWeek|Erzwingt die ODBC-Standard für die DAYOFWEEK skalare an. Dies ist standardmäßig auf, aber Benutzer, die lokalisierte Version benötigen, können das Verhalten Verwendung Rückgabeergebnis Oracle ändern.|1|  
|GuessTheColDef|Gibt an, und zwar unabhängig davon, ob der Treiber einen Wert ungleich NULL für zurückgeben soll die *CbColDef* Argument **SQLDescribeCol**. Gilt nur für Spalten, in denen es keine Skalierung Oracle definiert ist z. B. berechnete numerische, Spalten und Spalten als Zahl ohne eine Genauigkeit oder Dezimalstellenanzahl. Ein **SQLDescribeCol** gibt 130 für die Genauigkeit aufgerufen wird, wenn Oracle diese Informationen nicht bereitstellt.|0|  
  
 Beispielsweise würde eine Verbindungszeichenfolge, die mit den mit dem MyOracleServerOracle-Server und Oracle-Benutzer-MyUserID MyDataSource-Datenquelle verbunden werden:  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 Eine Verbindungszeichenfolge, die mit der MyOtherDataSource-Datenquelle, die mithilfe von Betriebssystem-Authentifizierung und die MyOtherOracleServerOracle Server verbindet würde folgendermaßen lauten:  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
