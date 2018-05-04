---
title: Inkompatible Zugriffsfeatures (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access databases
- Access databases, features incompatible with SQL Azure
- Access databases, features incompatible with SQL Server
- dates
- default expressions
- foreign keys
- hyperlink columns
- incompatible Access features
- indexes
- indexes, length of
- keywords
- primary keys
- reference, incompatible features
- replication columns
- special characters
- unique indexes
- validation rules
ms.assetid: 99d45b9c-e3b9-4d56-8c25-b594b887ace1
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e744ba8e8ae8927fc17c8e8c43cd288d02e82ca9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="incompatible-access-features-accesstosql"></a>Inkompatible Zugriffsfeatures (AccessToSQL)
Nicht alle Funktionen von Access-Datenbank sind kompatibel mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Beispielsweise [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und Zugriff weisen verschiedene Sätze von reservierten Schlüsselwörtern. Probleme, z. B., wenn diese auf eine erfolgreiche Migration verhindern könnten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Verwenden Sie in der folgenden Tabelle, um weitere Informationen zu möglichen Migrationsprobleme und Verwendungsmöglichkeiten Informationen finden sie.  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>Datenbankeinstellungen oder Funktionen, die Migration beeinflussen können  
  
|Zugriff auf Datenbankeinstellung oder Funktion|Migrationsproblem|  
|--------------------------------------|-------------------|  
|Eindeutige Indizes keine für den Zugriff auf Tabellen.|Wenn eine Tabelle, die einen eindeutigen Index nicht migriert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], die Tabelle kann nicht geändert werden, nach der Migration. Dies kann auf Probleme mit der Anwendungskompatibilität führen.<br /><br />Wenn Sie den Zugriff auf Datenbankobjekte konvertieren, wird das Fenster "Ausgabe" Access-Tabellen aufgelistet, die nicht eindeutige Indizes verfügen.<br /><br />Sie können Zugriff konfigurieren, um einen Primärschlüssel hinzugefügt werden, auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Tabelle während der Konvertierung. Weitere Informationen finden Sie unter [Projekteinstellungen (Konvertierung)](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388).|  
|Den Zugriff auf Tabellen haben Replikation-Spalten.|Migration von eine Access-Tabelle, die Replikationssystemspalten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Jet-Replikationsfunktionalität wird nach der Migration unterbrochen werden.<br /><br />Nach der Migration in Erwägung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Replikation synchronisierten Kopien Ihrer Datenbanken verwalten.|  
|Den Zugriff auf Tabellen, deren eindeutige Indizes werden mehrere null-Werte enthalten.|Access-Tabellen, eindeutige Indizes mit mehrere null-Werte aufweisen, können nicht übertragen werden, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], da in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], eindeutige Indizes nicht mehrere NULL-Werte zulassen. Die Migration wird für diese Tabellen fehlschlagen.<br /><br />SSMA wird dieses Problem in der Bewertungsberichte kennzeichnen. Um eine Bewertungsbericht erstellt haben, finden Sie unter [bewerten den Zugriff auf Datenbankobjekte für die Konvertierung](http://msdn.microsoft.com/en-us/8b9e23d6-da62-437a-8c05-8ad2628b9441).<br /><br />Wenn dieses Problem vorhanden ist, müssen Sie sicherstellen, dass der primäre Schlüssel keine doppelten null-Werte. Oder entfernen Sie die primary key- oder unique-Indizes, die mehrere null-Werte enthalten.|  
|Den Zugriff auf Tabellen enthalten die Date-Werten, die von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Bereich.|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **"DateTime"** Typ akzeptiert Datumsangaben im Bereich von 1 Jan. 1753 bis 31 Dez nur 9999. Access akzeptiert Datumsangaben im Bereich von 1 Jan-100 bis 31 Dezember 9999.<br /><br />SSMA wird dieses Problem in der Bewertungsberichte kennzeichnen. Um eine Bewertungsbericht erstellt haben, finden Sie unter [bewerten den Zugriff auf Datenbankobjekte für die Konvertierung](http://msdn.microsoft.com/en-us/8b9e23d6-da62-437a-8c05-8ad2628b9441).<br /><br />Sie können konfigurieren, wie Datumsangaben von SSMA aufgelöst wird, sind von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Bereich. Weitere Informationen finden Sie unter [Projekteinstellungen (Migration)](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d).|  
|Index-Länge in Access den Wert 900 Byte überschreitet.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Indizes weisen eine 900-Byte-Grenze für die Gesamtgröße der Indexschlüsselspalten vorhanden sind. Wenn die Access-Tabellen größere Indizes verwenden, werden SSMA eine Warnung angezeigt.<br /><br />Wenn Sie die Datenmigration fortsetzen, kann die Migration fehl.|  
|Access-Objektnamen werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Keywords-Eigenschaft, oder Sonderzeichen enthalten.|Zugriff und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] weisen verschiedene Sätze reservierte Schlüsselwörter und Sonderzeichen enthalten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objekte, die mit heißen akzeptiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schlüsselwörter oder, die Sonderzeichen enthalten, verwenden Sie Klammern oder Anführungszeichen Bezeichner, wie z. B. "Select" oder beim .p [auswählen]. Weitere Informationen finden Sie unter "Delimited Identifiers (Datenbankmodul)" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.<br /><br />**Hinweis:** zum Verwenden von Anführungszeichen zur Begrenzung von Bezeichnern muss SET QUOTED_IDENTIFIER ON.<br /><br />Beispielsweise `CREATE TABLE [schema](c1 [FOR])` ist eine gültige-Anweisung, obwohl **Schema** und **für** reservierte Schlüsselwörter sind. Darüber hinaus `CREATE TABLE [xxx*yyy](c1 x&y)` eine gültige Anweisung ist, obwohl die Namen von Tabellen- und Spaltennamen enthalten, die Sonderzeichen nicht **\&#42;** und **&amp;**.<br /><br />Alle Abfragen, die diese Objekte verweisen, müssen auch die Namen mit Klammern oder Anführungszeichen verwenden. Angenommen, die Abfrage `SELECT * FROM schema` schlägt fehl. Die richtige Abfrage ist: `SELECT * FROM [schema]`.<br /><br />Wenn Sie den Zugriff auf Datenbankobjekte konvertieren, wird im Ausgabebereich Access-Tabellen aufzulisten, die Schlüsselwörter oder Sonderzeichen zu verwenden. Sie können die Tabellen in Access ändern und dann entfernen und fügen Sie die Datenbank erneut; oder Sie können ändern, Abfragen, die diese Objekte verweisen, sodass die Abfragen Klammern oder Anführungszeichen zur Begrenzung von Bezeichnern verwenden. Wenn Sie Ihre Abfragen nicht ändern, die Access-Anwendungen möglicherweise Fehler zurück oder andere Probleme.|  
|Feldgrößen unterscheiden sich hinsichtlich der Primär-/Fremdschlüssel-Beziehungen.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] die Jet-Funktionalität, verknüpfen Sie Spalten mit unterschiedlichen Datentypen oder Größen mit foreign Key-Einschränkungen unterstützt nicht.<br /><br />Wenn Sie den Zugriff auf Datenbankobjekte konvertieren, listet das Fenster "Ausgabe" alle primären Schlüssel/Fremdschlüssel-Einschränkungen, die nicht in konvertiert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie können Datentypen und-Größen auf Spalten ändern, damit sie übereinstimmen, und klicken Sie dann zu entfernen und erneut, die Access-Datenbank hinzufügen. Oder Sie können die Daten migrieren, obwohl diese Einschränkungen nicht in erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|Auf die verwiesen wird Tabellen in Access Beziehungen verfügen weder einen Primärschlüssel als auch einen eindeutigen Index.|Zugriff akzeptiert die Beziehung zwischen Tabellen, bei denen die referenzierte Tabelle keinen Primärschlüssel oder einen eindeutigen Index verfügt. Dies wird jedoch nicht unterstützt von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br />Beim Konvertieren von den Zugriff auf Datenbankobjekte werden im Fenster "Ausgabe" alle Tabellen aufgelistet, die Beziehungen jedoch ohne Primärschlüssel oder eindeutigen Index verfügen. Sie können die Tabellen, um den Primärschlüssel oder eindeutige Indizes hinzufügen und entfernen und erneut hinzufügen, die Access-Datenbank ändern. Alternativ können Sie Daten migrieren, obwohl die Beziehung zwischen den Tabellen unterbrochen werden.|  
|Den Zugriff auf Tabellen haben Hyperlinkspalten.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] unterstützt keine **Hyperlink** Spalten. Stattdessen werden die Spalten wie Access Memospalten behandelt. Standardmäßig werden diese Spalten in konvertiert **nvarchar(max)** Spalten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie können die Zuordnung anpassen. Weitere Informationen finden Sie unter [Zuordnen von Quelle und Ziel-Datentypen](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9).|  
|Standardinstanz oder Überprüfung regelausdrücke enthalten Access-Funktionen, die konvertiert werden können [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.|Standardausdrücke Zugriff oder Validierungsregeln können Zugriff Systemfunktionen oder benutzerdefinierte Funktionen, die nicht zugeordnet werden können umfassen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Verwenden von Funktionen, die nicht zugeordnet werden können [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure ist es nicht vor dem Laden der Default-Ausdrücken oder Validierungsregeln in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.|  
  
## <a name="see-also"></a>Siehe auch  
[Access-Datenbanken vorbereitet für die Migration.](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
