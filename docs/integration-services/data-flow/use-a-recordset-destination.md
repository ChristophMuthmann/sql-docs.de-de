---
title: Verwenden eines Recordsetziels | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Recordset destination
ms.assetid: a7b143dc-8008-404f-83b0-b45ffbca6029
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d081c9a89e8a72dea2b09771b7ab548f032a25b4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="use-a-recordset-destination"></a>Verwenden eines Recordsetziels
  Das Recordsetziel speichert keine Daten in einer externen Datenquelle. Stattdessen speichert das Recordsetziel Daten im Speicher eines Recordsets, das in einer [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketvariablen des Datentyps **Object** gespeichert ist. Nachdem die Daten vom Recordsetziel gespeichert wurden, verwenden Sie typischerweise einen Foreach-Schleifencontainer mit dem Foreach-ADO-Enumerator zum Verarbeiten jeweils einer Zeile des Recordsets. Der Foreach-ADO-Enumerator speichert den Wert jeder einzelnen Spalte für die aktuelle Zeile in einer separaten Paketvariablen. Anschließend lesen die im Foreach-Schleifencontainer konfigurierten Tasks diese Werte in den Variablen und führen für diese Aktionen aus.  
  
 Sie können das Recordsetziel in vielen verschiedenen Szenarios verwenden. Im Folgenden finden Sie einige Beispiele:  
  
-   Mit einem Task „Mail senden“ und der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Ausdruckssprache können Sie für jede Zeile im Recordset eine benutzerdefinierte E-Mail-Nachricht senden.  
  
-   Mit einer in einem Datenflusstask als Quelle konfigurierten Skriptkomponente können Sie die Spaltenwerte in die Spalten des Datenflusses einlesen. Dann können Sie Transformationen und Ziele verwenden, um die Zeile zu transformieren und zu speichern. In diesem Beispiel wird der Datenflusstask für jede Zeile einmal ausgeführt.  
  
 In den folgenden Abschnitten wird zuerst der allgemeine Vorgang bei der Verwendung des Recordsetziels beschrieben, anschließend wird ein spezielles Beispiel für die Verwendung des Ziels gezeigt.  
  
## <a name="general-steps-to-using-a-recordset-destination"></a>Allgemeine Schritte bei der Verwendung eines Recordsetziels  
 Im folgenden Verfahren sind die zum Speichern von Daten in einem Recordsetziel und anschließenden Verarbeiten der einzelnen Zeilen mit dem Foreach-Schleifencontainer erforderlichen Schritte zusammengefasst.  
  
#### <a name="to-save-data-to-a-recordset-destination-and-process-each-row-by-using-the-foreach-loop-container"></a>So speichern Sie Daten in einem Recordsetziel und verarbeiten jede einzelne Zeile mit dem Foreach-Schleifencontainer  
  
1.  Erstellen oder öffnen Sie ein [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]-Paket in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  Erstellen Sie eine Variable für das vom Recordsetziel im Speicher gespeicherte Recordset, und legen Sie den Variablentyp auf **Object**fest.  
  
3.  Erstellen Sie zusätzliche Variablen der entsprechenden Typen für die Werte der einzelnen Spalten im zu verwendenden Recordset.  
  
4.  Fügen Sie den Verbindungs-Manager hinzu, der für die Datenquelle für den Datenfluss erforderlich ist, und konfigurieren Sie diesen.  
  
5.  Fügen Sie dem Paket einen Datenflusstask hinzu, und konfigurieren Sie auf der Registerkarte Datenfluss des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers Quellen und Transformationen zum Laden und Transformieren der Daten.  
  
6.  Fügen Sie dem Datenfluss ein Recordsetziel hinzu, und stellen Sie eine Verbindung mit den Transformationen her. Geben Sie für die **VariableName** -Eigenschaft des Recordsetziels den Namen der Variablen ein, die das Recordset aufnehmen soll.  
  
7.  Fügen Sie auf der Registerkarte „Ablaufsteuerung“ des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers einen Foreach-Schleifencontainer hinzu, und verbinden Sie diesen Container nach dem Datenflusstask. Öffnen Sie dann den **Foreach-Schleifen-Editor** , um den Container mit den folgenden Einstellungen zu konfigurieren:  
  
    1.  Wählen Sie auf der Seite **Sammlung** den Foreach-ADO-Enumerator aus. Wählen Sie dann unter **ADO-Objektquellvariable**die Variable aus, die das Recordset enthält.  
  
    2.  Ordnen Sie auf der Seite **Variablenzuordnungen** den nullbasierten Index der einzelnen zu verwendenden Spalten der entsprechenden Variablen zu.  
  
         Bei jeder Iteration der Schleife füllt der Enumerator diese Variablen mit den Spaltenwerten aus der aktuellen Zeile auf.  
  
8.  Fügen Sie im Foreach-Schleifencontainer Tasks zum Verarbeiten jeweils einer Zeile des Recordsets durch Lesen der Variablenwerte hinzu, und konfigurieren Sie diese.  
  
## <a name="example-of-using-the-recordset-destination"></a>Beispiel für die Verwendung des Recordsetziels  
 Im folgenden Beispiel lädt der Datenflusstask Informationen zu [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Mitarbeitern aus der Sales.SalesPerson-Tabelle in ein Recordsetziel. Anschließend liest ein Foreach-Schleifencontainer jeweils eine Datenzeile und ruft einen Task "Mail senden" auf. Der Task "Mail senden" verwendet Ausdrücke zum Senden benutzerdefinierter E-Mail-Nachrichten an die einzelnen Vertriebsmitarbeiter, in der deren Bonussummen angegeben sind.  
  
#### <a name="to-create-the-project-and-configure-the-variables"></a>So erstellen Sie das Projekt und konfigurieren die Variablen  
  
1.  Erstellen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]ein neues [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt.  
  
2.  Wählen Sie im Menü **SSIS** den Befehl **Variablen**aus.  
  
3.  Erstellen Sie im Fenster **Variablen** die Variablen für das Recordset sowie die Spaltenwerte in der aktuellen Zeile:  
  
    1.  Erstellen Sie die Variable **BonusRecordset**, und legen Sie deren Typ auf **Object**fest.  
  
         Die Variable **BonusRecordset** enthält das Recordset.  
  
    2.  Erstellen Sie die Variable **EmailAddress**, und legen Sie deren Typ auf **String**fest.  
  
         Die Variable **EmailAddress** enthält die E-Mail-Adresse der Vertriebsperson.  
  
    3.  Erstellen Sie die Variable **FirstName**, und legen Sie deren Typ auf **String**fest.  
  
         Die Variable **FirstName** enthält den Vornamen der Vertriebsperson.  
  
    4.  Erstellen Sie die Variable **Bonus**, und legen Sie deren Typ auf **Double**fest.  
  
         Die Variable **Bonus** enthält den Betrag für den Bonus der Vertriebsperson.  
  
#### <a name="to-configure-the-connection-managers"></a>So konfigurieren Sie die Verbindungs-Manager  
  
1.  Fügen Sie im Bereich Verbindungs-Manager des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers einen neuen OLE DB-Verbindungs-Manager hinzu, mit dem eine Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Beispieldatenbank hergestellt wird, und konfigurieren Sie diesen.  
  
     Die OLE DB-Quelle im Datenflusstask verwendet diesen Verbindungs-Manager zum Abrufen von Daten.  
  
2.  Fügen Sie im Bereich Verbindungs-Manager einen neuen SMTP-Verbindungs-Manager hinzu, mit dem eine Verbindung mit einem verfügbaren SMTP-Server hergestellt wird, und konfigurieren Sie diesen.  
  
     Der Task "Mail senden" im Foreach-Schleifencontainer verwendet diesen Verbindungs-Manager zum Senden von E-Mail-Nachrichten.  
  
#### <a name="to-configure-the-data-flow-and-the-recordset-destination"></a>So konfigurieren Sie den Datenfluss und das Recordsetziel  
  
1.  Fügen Sie auf der Registerkarte **Ablaufsteuerung** des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers der Entwurfsoberfläche einen Datenflusstask hinzu.  
  
2.  Fügen Sie dem Datenflusstask auf der Registerkarte **Datenfluss** tab, add an OLE DB source to the Datenfluss task, and then open the **Quellen-Editor für OLE DB**.  
  
3.  Konfigurieren Sie auf der Seite **Verbindungs-Manager** des Editors die Quelle mit den folgenden Einstellungen:  
  
    1.  Wählen Sie unter **OLE DB-Verbindungs-Manager**den zuvor erstellten OLE DB-Verbindungs-Manager aus.  
  
    2.  Wählen Sie unter **Datenzugriffsmodus**die Option **SQL-Befehl**aus.  
  
    3.  Geben Sie unter **SQL-Befehlstext**die folgende Abfrage ein:  
  
        ```sql 
        SELECT     Person.Contact.EmailAddress, Person.Contact.FirstName, CONVERT(float, Sales.SalesPerson.Bonus) AS Bonus  
        FROM         Sales.SalesPerson INNER JOIN  
                              Person.Contact ON Sales.SalesPerson.SalesPersonID = Person.Contact.ContactID  
        ```  
  
        > [!NOTE]  
        >  Sie müssen den **currency** -Wert in der Bonus-Spalte in den Datentyp **float** konvertieren, bevor Sie diesen in eine Paketvariable vom Typ **Double**laden können.  
  
4.  Fügen Sie auf der Registerkarte **Datenfluss** ein Recordsetziel hinzu, und stellen Sie eine Verbindung mit dem Ziel nach der der OLE DB-Quelle her.  
  
5.  Öffnen Sie den **Recordsetziel-Editor**, und konfigurieren Sie das Ziel mit den folgenden Einstellungen:  
  
    1.  Wählen Sie auf der Registerkarte **Komponenteneigenschaften** für die **VariableName** -Eigenschaft **User::BonusRecordset**aus.  
  
    2.  Wählen Sie auf der Registerkarte **Eingabespalten** alle drei verfügbaren Spalten aus.  
  
#### <a name="to-configure-the-foreach-loop-container-and-run-the-package"></a>So konfigurieren Sie den Foreach-Schleifencontainer und führen das Paket aus  
  
1.  Fügen Sie auf der Registerkarte **Ablaufsteuerung** des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers einen Foreach-Schleifencontainer hinzu, und verbinden Sie den Container nach dem Datenflusstask.  
  
2.  Öffnen Sie den **Foreach-Schleifen-Editor**, und konfigurieren Sie den Container mit den folgenden Einstellungen:  
  
    1.  Wählen Sie auf der Seite **Sammlung** unter **Enumerator**die Option **Foreach-ADO-Enumerator**und unter **ADO-Objektquellvariable**die Option **User::BonusRecordset**aus.  
  
    2.  Ordnen Sie auf der Seite **Variablenzuordnungen** **User::EmailAddress** Index 0, **User::FirstName** Index 1 und **User::Bonus** Index 2 zu.  
  
3.  Fügen Sie auf der Registerkarte **Ablaufsteuerung** im Foreach-Schleifencontainer einen Task „Mail senden“ hinzu.  
  
4.  Öffnen Sie den **Editor für den Task „Mail senden“**, und konfigurieren Sie auf der Seite **E-Mail** den Task mit den folgenden Einstellungen:  
  
    1.  Wählen Sie für **SmtpConnection**den SMTP-Verbindungs-Manager aus, der zuvor konfiguriert wurde.  
  
    2.  Geben Sie unter **From**eine geeignete E-Mail-Adresse ein.  
  
         Wenn Sie Ihre eigene E-Mail-Adresse verwenden, können Sie überprüfen, ob das Paket erfolgreich ausgeführt wird. Für Nachrichten, die vom Task „Mail senden“ an die fiktiven Vertriebspersonen von [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]gesendet wurden, erhalten Sie Unzustellbarkeitsmeldungen.  
  
    3.  Geben Sie unter **To**eine Standard-E-Mail-Adresse ein.  
  
         Dieser Wert wird nicht verwendet, sondern zur Laufzeit durch die E-Mail-Adresse der betreffenden Vertriebsperson ersetzt.  
  
    4.  Geben Sie unter **Subject**„Ihr Jahresbonus“ ein.  
  
    5.  Wählen Sie für **MessageSourceType**die Option **Direkteingabe**aus.  
  
5.  Klicken Sie auf der Seite **Ausdrücke** des **Editors für den Task „Mail senden“**auf die Schaltfläche mit den drei Punkten (**...**), um den **Eigenschaftsausdrucks-Editor**zu öffnen.  
  
6.  Geben Sie im **Eigenschaftsausdrucks-Editor**die folgenden Informationen ein:  
  
    1.  Fügen Sie unter **ToLine**den folgenden Ausdruck hinzu:  
  
        ```  
        @[User::EmailAddress]  
        ```  
  
    2.  Fügen Sie für die **MessageSource** -Eigenschaft den folgenden Ausdruck hinzu:  
  
        ```  
        "Dear " +  @[User::FirstName] + ": The amount of your bonus for this year is $" +  (DT_WSTR, 12) @[User::Bonus] + ". Thank you!"  
        ```  
  
7.  Führen Sie das Paket aus.  
  
     Wenn Sie einen gültigen SMTP-Server und Ihre eigene E-Mail-Adresse angegeben haben, erhalten Sie für die Nachrichten, die vom Task "Mail senden" an die fiktiven Vertriebspersonen von [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]gesendet wurden, Unzustellbarkeitsmeldungen.  
  
  
