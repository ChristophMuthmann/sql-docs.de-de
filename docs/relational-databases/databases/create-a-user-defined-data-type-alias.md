---
title: Erstellen eines benutzerdefinierten Datentypalias | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.userdefineddatatype.general.f1
- sql13.swb.new.datatype.properties.general.f1
helpviewer_keywords: alias data types [SQL Server], creating
ms.assetid: b1dd8413-0cd0-411b-a79b-1bb043ccc62d
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8b7281ad56ebbf4b63d03866888a91ccfc111985
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-a-user-defined-data-type-alias"></a>Erstellen eines benutzerdefinierten Datentypalias
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie ein neuer benutzerdefinierter Datentypalias in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] erstellt wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So erstellen Sie einen benutzerdefinierten Datentypalias mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Bei der Verwendung eines Namens für einen benutzerdefinierten Datentypalias müssen die Regeln für Bezeichner eingehalten werden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die CREATE TYPE-Berechtigung für die aktuelle Datenbank und die ALTER-Berechtigung für *schema_name*. Wenn *schema_name* nicht angegeben wird, gelten die Standardregeln für die Namensauflösung, um das Schema für den aktuellen Benutzer zu bestimmen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-create-a-user-defined-data-type"></a>So erstellen Sie einen benutzerdefinierten Datentyp  
  
1.  Erweitern Sie im Objekt-Explorer **Datenbanken**, erweitern Sie eine Datenbank, erweitern Sie **Programmierbarkeit**, erweitern Sie **Typen**, klicken Sie mit der rechten Maustaste auf **Benutzerdefinierte Datentypen**, und klicken Sie dann auf **Neuer benutzerdefinierter Datentyp**.  
  
     **NULL-Werte zulassen**  
     Geben Sie an, ob der benutzerdefinierte Datentyp NULL-Werte akzeptieren kann. Die NULL-Zulässigkeit eines vorhandenen benutzerdefinierten Datentyps ist nicht bearbeitbar.  
  
     **Datentyp**  
     Wählen Sie den Basisdatentyp aus dem Listenfeld aus. Im Listenfeld werden alle Datentypen mit Ausnahme der Datentypen **geography**, **geometry**, **hierarchyid**, **sysname**, **timestamp** und **xml** angezeigt. Der Datentyp eines vorhandenen benutzerdefinierten Datentyps ist nicht bearbeitbar.  
  
     **Default**  
     Wählen Sie optional einen Standardwert aus, um den benutzerdefinierten Datentypalias zu binden.  
  
     **Länge/Genauigkeit**  
     Zeigt jeweils die Länge bzw. Genauigkeit des Datentyps an. **Länge** gilt für zeichenbasierte benutzerdefinierte Datentypen, und **Genauigkeit** gilt nur für auf numerischen Werten basierende benutzerdefinierte Datentypen. Die Bezeichnung ändert sich je nach dem zuvor gewählten Datentyp. Dieses Feld ist bearbeitbar, wenn die Länge oder Genauigkeit des ausgewählten Datentyps fest ist.  
  
     Die Länge wird für **nvarchar(max)**-, **varchar(max)**- **oder varbinary(max)** -Datentypen nicht angezeigt.  
  
     **Name**  
     Wenn Sie einen neuen benutzerdefinierten Datentypalias erstellen, geben Sie einen eindeutigen Namen ein, der in der gesamten Datenbank verwendet werden soll, um den benutzerdefinierten Datentyp darzustellen. Die maximale Zeichenanzahl muss dem Systemdatentyp **sysname** entsprechen. Der Name eines vorhandenen benutzerdefinierten Datentypalias ist nicht bearbeitbar.  
  
     **Rule**  
     Wählen Sie optional eine Regel zum Binden an den benutzerdefinierten Datentypalias aus.  
  
     **Dezimalstellen**  
     Gibt an, wie viele Dezimalstellen (Ziffern nach dem Dezimalzeichen) maximal gespeichert werden können.  
  
     **Schema**  
     Wählen Sie ein Schema aus einer Liste mit allen für den aktuellen Benutzer verfügbaren Schemas aus. Die Standardauswahl ist das Standardschema für den aktuellen Benutzer.  
  
     **Speicherung**  
     Zeigt die maximale Speichergröße für den benutzerdefinierten Datentypalias an. Die maximalen Speicherplatzgrößen variieren in Abhängigkeit von der Genauigkeit.  
  
    |||  
    |-|-|  
    |1 – 9|5|  
    |10 – 19|9|  
    |20 – 28|13|  
    |29 – 38|17|  
  
     Bei den Datentypen **nchar** und **nvarchar** beträgt der Speicherwert immer das Zweifache des Werts in **Länge**.  
  
     Für **nvarchar(max)**-, **varchar(max)**- oder **varbinary(max)** -Datentypen wird der Speicher nicht angezeigt.  
  
2.  Geben Sie im Dialogfeld **Neuer benutzerdefinierter Datentyp** in das Feld **Schema** das Schema ein, das diesen Datentypalias besitzen soll, oder wählen Sie mit der Schaltfläche zum Durchsuchen das Schema aus.  
  
3.  Geben Sie in das Feld **Name** einen Namen für den neuen Datentypalias ein.  
  
4.  Wählen Sie im Feld **Datentyp** den Datentyp aus, auf dem der neue Datentypalias basieren soll.  
  
5.  Vervollständigen Sie, soweit für diesen Datentyp zutreffend, die Felder **Länge**, **Genauigkeit**und **Dezimalstellen** .  
  
6.  Aktivieren Sie **NULL-Werte zulassen** , damit der neue Datentypalias NULL-Werte zulässt.  
  
7.  Vervollständigen Sie im Bereich **Bindung** die Felder **Standard** oder **Regel** , falls Sie dem neuen Datentypalias einen Standardwert oder eine Regel zuordnen möchten. Standardwerte und Regeln können in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]nicht erstellt werden. Verwenden Sie [!INCLUDE[tsql](../../includes/tsql-md.md)]. Beispielcode zum Erstellen von Standardwerten und Regeln finden Sie im Vorlagen-Explorer.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-create-a-user-defined-data-type-alias"></a>So erstellen Sie einen benutzerdefinierten Datentypalias  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird ein Datentypalias erstellt, der auf dem vom System bereitgestellten Datentyp `varchar` basiert. Der Datentypalias `ssn` wird für Spalten mit elfstelligen Sozialversicherungsnummern verwendet (999-99-9999). Diese Spalte darf nicht den Wert NULL aufweisen.  
  
```tsql  
CREATE TYPE ssn  
FROM varchar(11) NOT NULL ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)  
  
  
