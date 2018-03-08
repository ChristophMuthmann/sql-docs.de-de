---
title: "Analysis Services Tutorial ergänzenden Lektion: dynamische Sicherheit | Microsoft Docs"
description: Beschreibt, wie dynamischen Sicherheit zu verwenden, indem Sie mithilfe von Zeilenfiltern in Analysis Services-Lernprogramm.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: 4f304535ab43563b64757ccfc812498df4467762
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="supplemental-lesson---dynamic-security"></a>Ergänzende Lektion - dynamische Sicherheit

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In dieser ergänzenden Lektion erstellen Sie eine zusätzliche Rolle, die dynamischen Sicherheit implementiert. Dynamische Sicherheit bietet Sicherheit auf Zeilenebene basierend auf dem Benutzernamen oder der Anmelde-ID des angemeldeten Benutzers. 
  
Um dynamische Sicherheit zu implementieren, fügen Sie eine Tabelle mit dem Modell mit den Benutzernamen von Benutzern, die eine Verbindung mit dem Modell herstellen und Modellobjekte und Daten durchsuchen können. Die diesem Lernprogramm erstellte Modell wird im Kontext der Adventure Works; Um diese Lektion abzuschließen, müssen Sie jedoch eine Tabelle mit Benutzern aus Ihrer eigenen Domäne hinzufügen. Sie benötigen keine Kennwörter für den Benutzernamen, die hinzugefügt werden. Um eine Tabelle EmployeeSecurity mit einem kleinen Teil der Benutzer in Ihrer eigenen Domäne zu erstellen, verwenden Sie die Funktion zum Einfügen, Mitarbeiterdaten aus einem Excel-Arbeitsblatt. In einem realen Szenario wäre die Tabelle mit den Benutzernamen in der Regel eine Tabelle aus einer tatsächlichen Datenbank als Datenquelle; Angenommen, eine echte DimEmployee-Tabelle.  
  
Um dynamische Sicherheit zu implementieren, verwenden Sie zwei DAX-Funktionen: [USERNAME-Funktion (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) und [LOOKUPVALUE-Funktion (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab). Diese Funktionen, die in einer Zeilenfilterformel angewendet werden, werden in einer neuen Rolle definiert. Mithilfe der LOOKUPVALUE-Funktion gibt die Formel einen Wert aus der EmployeeSecurity-Tabelle. Die Formel übergibt Sie an, dass der Wert der USERNAME-Funktion, die den Benutzernamen des angemeldeten Benutzers angibt, die dieser Rolle gehört. Der Benutzer kann dann nur die von den Zeilenfiltern der Rolle festgelegten Daten durchsuchen. In diesem Fall geben Sie an, dass Verkaufsmitarbeiter nur internetumsatzdaten für die Vertriebsgebiete durchsuchen können, in denen sie Mitglied sind.  
  
Aufgaben, die nur für dieses Adventure Works-Szenario für die Tabellenmodellierung relevant sind und nicht unbedingt in der realen Welt anwendbar sind, werden als solche identifiziert. Jede Aufgabe umfasst weitere Informationen, die den Zweck der Aufgabe beschreiben.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **30 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  

In diesem Artikel ergänzende Lektion ist Teil eines Lernprogramms zur tabellenmodellierung, das in Reihenfolge absolviert werden sollte. Sie sollten vor dem Ausführen der Aufgaben in dieser ergänzenden Lektion alle vorherigen Lektionen abgeschlossen haben.  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>Hinzufügen der dimSalesTerritory-Tabelle zum Projekt 'AW Internet Sales Tabular Model'  

Um dynamische Sicherheit für dieses Adventure Works-Szenario zu implementieren, müssen Sie zwei weitere Tabellen mit dem Modell hinzufügen. Die erste Tabelle, die Sie hinzufügen, ist die dimsalesterritory-Tabelle (als Vertriebsgebiet) aus der gleichen AdventureWorksDW-Datenbank. Sie gelten später einen Zeilenfilter für die Tabelle "salesterritory", die die betreffenden Daten definiert, die der angemeldete Benutzer navigieren kann.  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>So fügen Sie die Tabelle dimSalesTerritory hinzu  
  
1.  Im tabellarischen Modell-Explorer > **Datenquellen**mit der rechten Maustaste auf die Verbindung, und klicken Sie dann auf **neue Importtabellen**.  

    Wenn das Dialogfeld Identitätswechselinformationen angezeigt wird, geben Sie die Identitätswechsel-Anmeldeinformationen ein, die Sie in Lektion 2, "Hinzufügen von Daten", verwendet haben.
  
2.  Wählen Sie im Navigator der **DimSalesTerritory** Tabelle, und klicken Sie dann auf **OK**.    
  
3.  Klicken Sie im Abfrage-Editor auf die **DimSalesTerritory** abgefragt, und entfernen Sie **SalesTerritoryAlternateKey** Spalte.  
  
7.  Klicken Sie auf **Importieren**.  
  
    Die neue Tabelle wird im Arbeitsbereich "Modell" hinzugefügt. Objekte und Daten aus der Quelltabelle DimSalesTerritory werden dann in Ihre AW Internet Sales Tabular Model importiert.  
  
9. Nachdem die Tabelle wurde erfolgreich importiert wurde, klicken Sie auf **schließen**.  

## <a name="add-a-table-with-user-name-data"></a>Hinzufügen einer Tabelle mit Benutzernamendaten  

Die Tabelle dimemployee in der AdventureWorksDW-Beispieldatenbank werden Benutzer in der AdventureWorks-Domäne enthält. Diese Benutzernamen sind nicht in Ihrer Umgebung vorhanden. Sie müssen eine Tabelle im Modell erstellen, die einen kleinen Teil (mindestens drei) der tatsächlichen Benutzer in Ihrer Organisation enthält. Anschließend fügen Sie diese Benutzer als Mitglieder der neuen Rolle. Benötigen Sie keine Kennwörter für die beispielbenutzernamen, aber das aktuelle Windows-Benutzernamen Ihrer Domäne.  
  
#### <a name="to-add-an-employeesecurity-table"></a>Hinzufügen eine Tabelle EmployeeSecurity  
  
1.  Öffnen Sie Microsoft Excel, erstellen ein Arbeitsblatt ein.  
  
2.  Kopieren Sie die folgende Tabelle, einschließlich der Kopfzeile, und fügen Sie sie dann in das Arbeitsblatt ein.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Ersetzen Sie den Vornamen, Nachnamen und "Domäne\Benutzername" mit dem Namen und Anmelde-Ids von drei Benutzern in Ihrer Organisation ein. Platzieren Sie denselben Benutzer auf die ersten beiden Zeilen bei EmployeeId 1 wird angezeigt, dass dieser Benutzer mehr als eine Vertriebsregion gehört. Lassen Sie die Felder EmployeeId und SalesTerritoryId, wie sie sind.  
  
4.  Speichern Sie das Arbeitsblatt als **SampleEmployee**.  
  
5.  Wählen Sie im Arbeitsblatt alle Zellen mit Mitarbeiterdaten, einschließlich der Header, und klicken Sie dann mit der rechten Maustaste der ausgewählten Daten und klicken Sie dann auf **Kopie**.  
  
6.  Klicken Sie in SSDT, auf die **bearbeiten** Menü, und klicken Sie dann auf **einfügen**.  
  
    Wenn einfügen abgeblendet ist, klicken Sie auf eine beliebige Spalte in einer Tabelle im Modell-Designer-Fenster, und versuchen Sie es erneut.  
  
7.  In der **Vorschau einfügen** Dialogfeld **Tabellenname**, Typ **EmployeeSecurity**.  
  
8.  In **einzufügende Daten**, ob die Daten alle Benutzerdaten und Kopfzeilen aus dem Arbeitsblatt SampleEmployee.  
  
9. Überprüfen Sie, ob **Erste Zeile als Spaltenüberschriften verwenden** aktiviert ist, und klicken Sie anschließend auf **OK**.  
  
    Eine neue Tabelle namens EmployeeSecurity mit Mitarbeiterdaten aus dem Arbeitsblatt SampleEmployee wird erstellt.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>Erstellen von Beziehungen zwischen der FactInternetSales DimGeography und DimSalesTerritory-Tabelle  

Die Tabelle FactInternetSales DimGeography und dimsalesterritory-Tabelle enthalten jeweils die Spalte SalesTerritoryId. Die SalesTerritoryId-Spalte in der DimSalesTerritory-Tabelle enthält die Werte mit einer anderen Id für jedes Vertriebsgebiet.  
  
#### <a name="to-create-relationships-between-the-factinternetsales-dimgeography-and-the-dimsalesterritory-table"></a>So erstellen Sie Beziehungen zwischen der FactInternetSales, DimGeography und die DimSalesTerritory-Tabelle  
  
1.  In der Diagrammsicht in der **DimGeography** Tabelle auf, und warten Sie, die **SalesTerritoryId** Spalte ziehen Sie dann den Cursor an die **SalesTerritoryId** Spalte in der **DimSalesTerritory** Tabelle, und lassen Sie anschließend.  
  
2.  In der **FactInternetSales** Tabelle auf, und warten Sie, die **SalesTerritoryId** Spalte ziehen Sie dann den Cursor an die **SalesTerritoryId** Spalte in der **DimSalesTerritory** Tabelle, und lassen Sie anschließend.  
  
    Beachten Sie, dass die Eigenschaft aktiv für diese Beziehung ist "false", was bedeutet, dass er nicht aktiv ist. Die FactInternetSales-Tabelle ist bereits eine andere aktive Beziehung.  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a>Ausblenden der EmployeeSecurity-Tabelle in Clientanwendungen  

In dieser Aufgabe blenden Sie die EmployeeSecurity-Tabelle, da diese in der Feldliste einer Clientanwendung angezeigt werden. Bedenken Sie, die eine Tabelle durch Ausblenden nicht gesichert wird. Benutzer können weiterhin die EmployeeSecurity Tabellendaten Abfragen, wenn sie wissen, wie. Zum Sichern der EmployeeSecurity Tabellendaten, die verhindern, dass Benutzer kann seine Daten Abfragen wenden Sie einen Filter in einer späteren Aufgabe.  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a>So blenden Sie die EmployeeSecurity-Tabelle in Clientanwendungen aus  
  
-   Klicken Sie im Modell-Designer in der Diagrammsicht mit der rechten Maustaste auf die Tabellenkopfzeile **Employee** (Angestellter), und klicken Sie anschließend auf **Aus Clienttools ausblenden**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Erstellen der Benutzerrolle 'Sales Employees by Territory'  

In dieser Aufgabe erstellen Sie eine Benutzerrolle an. Diese Rolle umfasst einen Zeilenfilter definieren, welche Zeilen der Tabelle DimSalesTerritory für Benutzer sichtbar sind. Der Filter wird dann in die Richtung der 1: n-Beziehung zu anderen Tabellen, die im Zusammenhang mit der dimsalesterritory-Tabelle angewendet. Sie gelten auch einen Filter, der sichert die gesamte EmployeeSecurity-Tabelle, damit jeder Benutzer, der Mitglied der Rolle ist.  
  
> [!NOTE]  
> Die Rolle Sales Employees by Territory, die Sie in dieser Lektion erstellen, schränkt Mitglieder ein, sodass sie nur Umsatzdaten für das Vertriebsgebiet suchen (oder abfragen) können, zu dem sie gehören. Wenn Sie einen Benutzer als Mitglied der Sales Employees Territory-Rolle, die auch vorhanden ist hinzugefügt, wie ein Element in einer Rolle in erstellt [Lektion 11: Erstellen von Rollen](../tutorial-tabular-1400/as-lesson-11-create-roles.md), erhalten Sie eine Kombination von Berechtigungen. Wenn ein Benutzer Mitglied mehrerer Rollen ist, sind die für jede Rolle definierten Berechtigungen und Zeilenfilter kumulativ. D. h., hat der Benutzer mehr Berechtigungen, die durch die Kombination aus Rollen bestimmt.  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>So erstellen Sie die Benutzerrolle 'Sales Employees by Territory'  
  
1.  Klicken Sie in SSDT, auf die **Modell** Menü, und klicken Sie dann auf **Rollen**.  
  
2.  In **Rollen-Manager**, klicken Sie auf **neu**.  
  
    Der Liste wird eine neue Rolle mit der Berechtigung Keine hinzugefügt.  
  
3.  Klicken Sie auf die neue Rolle, und klicken Sie dann in der **Name** Spalte benennen Sie die Rolle auf **Sales Employees by Territory**.  
  
4.  Klicken Sie in der Spalte **Berechtigungen** auf die Dropdownliste, und wählen Sie anschließend die Berechtigung **Lesen** aus.  
  
5.  Klicken Sie auf die **Elemente** Registerkarte, und klicken Sie dann auf **hinzufügen**.  
  
6.  In der **Benutzer oder Gruppe auswählen** Dialogfeld **Geben Sie die zu verwendenden Objektnamen wählen**, geben Sie das erste Beispiel Benutzernamen ein, die Sie beim Erstellen der Tabelle EmployeeSecurity verwendet. Klicken Sie auf **Namen überprüfen** , um die Gültigkeit des Benutzernamens zu überprüfen, und klicken Sie anschließend auf **OK**.  
  
    Wiederholen Sie diesen Schritt, Hinzufügen von den anderen beispielbenutzernamen, die Sie beim Erstellen der Tabelle EmployeeSecurity verwendet werden soll.  
  
7.  Klicken Sie auf die **Zeilenfilter** Registerkarte.  
  
8.  Für die **EmployeeSecurity** -Tabelle in der **DAX-Filter** Spalte Geben Sie die folgende Formel:  
  
    ```
      =FALSE()  
    ```
  
    Diese Formel gibt an, dass alle Spalten in der falschen booleschen Bedingung aufgelöst. Keine Spalten für die Tabelle EmployeeSecurity können von einem Mitglied der Sales Employees von Benutzerrolle Territory abgefragt werden.  
  
9. Für die **DimSalesTerritory** Tabelle, und geben Sie die folgende Formel:  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    In dieser Formel gibt die LOOKUPVALUE-Funktion alle Werte für die DimEmployeeSecurity [SalesTerritoryId]-Spalte, in denen die EmployeeSecurity [LoginId] ist identisch mit dem aktuell angemeldeten Windows-Benutzernamen und EmployeeSecurity [SalesTerritoryId] ist die dimsalesterritory-Tabelle [SalesTerritoryId] identisch.  
  
    Der Satz von IDs von LOOKUPVALUE zurückgegebenen Vertriebsgebiet wird dann zum Einschränken der Zeilen in der DimSalesTerritory-Tabelle dargestellt. Nur Zeilen, in denen die SalesTerritoryID für die Zeile im Satz von IDs, die von der LOOKUPVALUE-Funktion zurückgegeben wird, werden angezeigt.  
  
10. Klicken Sie im Rollen-Manager auf **Ok**.  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a>Testen der Benutzerrolle 'Sales Employees by Territory'  

In dieser Aufgabe verwenden Sie analysieren Funktion in Excel in SSDT, um die Wirksamkeit von Sales Employees Benutzerrolle Territory zu testen. Sie geben einen Benutzernamen, die Sie der Tabelle EmployeeSecurity und als Mitglied der Rolle hinzugefügt. Dieser Benutzername wird dann als der effektive Benutzername in der Verbindung zwischen Excel und das Modell erstellt, verwendet.  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>So testen Sie die Benutzerrolle 'Sales Employees by Territory'  
  
1.  Klicken Sie in SSDT, auf die **Modell** Menü, und klicken Sie dann auf **in Excel analysieren**.  
  
2.  Wählen Sie im Dialogfeld **In Excel analysieren** in **Geben Sie den Benutzernamen oder die Rolle für die Verbindung mit dem Modell an**die Option **Anderer Windows-Benutzer**aus, und klicken Sie anschließend auf **Durchsuchen**.  
  
3.  In der **Benutzer oder Gruppe auswählen** Dialogfeld **Geben Sie die zu verwendenden Objektnamen**, geben Sie einen Benutzernamen ein, die Sie in der Tabelle EmployeeSecurity enthalten, und klicken Sie dann auf **Namen überprüfen**.  
  
4.  Klicken Sie auf **OK** , um das Dialogfeld **Benutzer oder Gruppe auswählen** zu schließen. Klicken Sie anschließend auf **OK** , um das Dialogfenster **In Excel analysieren** zu schließen.  
  
    Excel wird mit einer neuen Arbeitsmappe geöffnet. Automatisch wird eine PivotTable erstellt. Die PivotTable-Fields-Liste enthält die meisten Datenfelder im neuen Modell verfügbar sind.  
  
    Beachten Sie, dass die EmployeeSecurity-Tabelle nicht in der PivotTable-Fields-Liste angezeigt wird. Sie ausgeblendet haben diese Tabelle aus den Clienttools in der vorherigen Aufgabe.  
  
5.  In der **Felder** Liste **∑ Internet Sales** (Measures), wählen Sie die **InternetTotalSales** Measure. Das Measure in eingegeben wird die **Werte** Felder.  
  
6.  Wählen Sie die **SalesTerritoryId** Spalte aus der **DimSalesTerritory** Tabelle. Die Spalte eingegeben wird, in der **Zeilenbezeichnungen** Felder.  
  
    Die Internetumsatzzahlen werden nur für den einen Bereich angezeigt, dem der gültige Benutzername, den Sie verwendet haben, zugeordnet haben. Bei Auswahl einer anderen Spalte, z. B. City, aus der Tabelle DimGeography als Feld Zeilenbezeichnungen, werden nur Orte im Vertriebsgebiet, zu dem der gültige Benutzer gehört, angezeigt.  
    Dieser Benutzer kann nicht durchsuchen oder Abfragen internetumsatzdaten für Gebiete als der, der sie angehören. Diese Einschränkung ist, da der Zeilenfilter definiert, für die DimSalesTerritory-Tabelle, in der Sales Employees by Territory-Benutzerrolle ", Daten in Bezug auf andere Vertriebsgebiete sichert.  
  
## <a name="see-also"></a>Siehe auch  

[USERNAME-Funktion (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[LOOKUPVALUE-Funktion (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[CUSTOMDATA-Funktion (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  