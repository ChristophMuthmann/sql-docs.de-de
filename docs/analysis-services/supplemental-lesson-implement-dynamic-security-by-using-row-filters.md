---
title: Implementieren von dynamischer Sicherheit mithilfe von Zeilenfiltern | Microsoft Docs
ms.custom: 
ms.date: 04/10/2017
ms.prod: 
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: 
ms.assetid: 
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 14bc3755dcbb92af2f75ed47a4df6843fe4782b4
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="supplemental-lesson---implement-dynamic-security-by-using-row-filters"></a>Ergänzende Lektion - Implementieren von dynamischer Sicherheit mithilfe von Zeilenfiltern
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In dieser ergänzenden Lektion erstellen Sie eine zusätzliche Rolle, die dynamische Sicherheit implementiert. Dynamische Sicherheit bietet Sicherheit auf Zeilenebene basierend auf dem Benutzernamen oder der Anmelde-ID des angemeldeten Benutzers. Weitere Informationen finden Sie unter [Rollen](../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
Um dynamische Sicherheit zu implementieren, müssen Sie dem Modell eine Tabelle hinzufügen, die die Windows-Benutzernamen der Benutzer enthält, die eine Verbindung mit dem Modell als Datenquelle erstellen und Modellobjekte und Daten durchsuchen dürfen. In diesem Lernprogramm erstellen Sie ein Modell im Kontext der Adventure Works Corp. Sie müssen jedoch eine Tabelle mit Benutzern Ihrer Domäne hinzufügen, um diese Lektion abzuschließen. Die Kennwörter für die hinzuzufügenden Benutzernamen sind nicht erforderlich. Um eine Tabelle EmployeeSecurity mit einem kleinen Teil der Benutzer in Ihrer eigenen Domäne zu erstellen, verwenden Sie die Funktion zum Einfügen, Mitarbeiterdaten aus einem Excel-Arbeitsblatt. In der wirklichen Welt verwendet die Tabelle mit den Benutzernamen, die Sie einem Modell hinzugefügt haben, in der Regel eine Tabelle aus einer tatsächlichen Datenbank als Datenquelle, z. B. eine reale dimEmployee-Tabelle.  
  
Verwenden Sie die zwei neuen DAX-Funktionen ( [USERNAME-Funktion (DAX)](http://msdn.microsoft.com/en-us/22dddc4b-1648-4c89-8c93-f1151162b93f) und [LOOKUPVALUE-Funktion (DAX)](http://msdn.microsoft.com/en-us/73a51c4d-131c-4c33-a139-b1342d10caab)), um dynamische Sicherheit zu implementieren. Diese Funktionen, die in einer Zeilenfilterformel angewendet werden, werden in einer neuen Rolle definiert. Mit der LOOKUPVALUE-Funktion, die Formel gibt einen Wert aus der EmployeeSecurity-Tabelle und übergibt dann, dass der Wert der USERNAME-Funktion, die den Benutzernamen des angemeldeten Benutzers angibt, die dieser Rolle gehört. Der Benutzer kann dann nur die von den Zeilenfiltern der Rolle festgelegten Daten durchsuchen. In diesem Szenario legen Sie fest, dass Verkaufsmitarbeiter nur nach Internetumsatzdaten für die Vertriebsgebiete, denen sie angehören, suchen können.  
  
In dieser ergänzenden Lektion führen Sie eine Reihe von Aufgaben durch. Aufgaben, die nur für dieses Adventure Works-Szenario für die Tabellenmodellierung relevant sind und nicht unbedingt in der realen Welt anwendbar sind, werden als solche identifiziert. Jede Aufgabe umfasst weitere Informationen, die den Zweck der Aufgabe beschreiben.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **30 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Dieses ergänzende Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Sie sollten vor dem Ausführen der Aufgaben in dieser ergänzenden Lektion alle vorherigen Lektionen abgeschlossen haben.  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>Hinzufügen der dimSalesTerritory-Tabelle zum Projekt 'AW Internet Sales Tabular Model'  
Um dynamische Sicherheit für dieses Adventure Works-Szenario zu implementieren, müssen Sie dem Modell zwei weitere Tabellen hinzufügen. Die erste Tabelle, die Sie hinzufügen, ist die dimSalesTerritory-Tabelle (als Vertriebsgebiet) aus der gleichen AdventureWorksDW-Datenbank. Sie werden später einen Zeilenfilter auf die Tabelle "salesterritory" anwenden, die die betreffenden Daten definiert, die der angemeldete Benutzer navigieren kann.  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>So fügen Sie die Tabelle dimSalesTerritory hinzu  
  
1.  Klicken Sie in SSDT, auf die **Modell** Menü, und klicken Sie dann auf **vorhandene Verbindungen**.  
  
2.  Überprüfen Sie im Dialogfeld **Vorhandene Verbindungen** , ob die Datenquellenverbindung **Adventure Works DB from SQL** (Adventure Works-Datenbank aus SQL) ausgewählt ist, und klicken Sie anschließend auf **Öffnen**.  
  
    Wenn das Dialogfeld Identitätswechselinformationen angezeigt wird, geben Sie die Identitätswechsel-Anmeldeinformationen ein, die Sie in Lektion 2, "Hinzufügen von Daten", verwendet haben.  
  
3.  Behalten Sie auf der Seite **Auswählen, wie die Daten importiert werden sollen** die Auswahl der Option **Aus einer Liste von Tabellen und Sichten auswählen, um die zu importierenden Daten zu bestimmen** bei, und klicken Sie auf **Weiter**.  
  
4.  Wählen Sie auf der Seite **Tabellen und Sichten auswählen** die Tabelle **DimSalesTerritory** aus.  
  
5.  Klicken Sie auf **Preview and Filter**(Vorschau anzeigen und filtern).  
  
6.  Heben Sie die Auswahl der Spalte **SalesTerritoryAlternateKey** auf, und klicken Sie anschließend auf **OK**.  
  
7.  Klicken Sie auf der Seite **Tabellen und Sichten auswählen** auf **Fertig stellen**.  
  
    Die neue Tabelle wird am Ende des Modellarbeitsbereichs hinzugefügt. Objekte und Daten aus der Quelltabelle DimSalesTerritory werden dann in Ihre AW Internet Sales Tabular Model importiert.  
  
9. Nachdem die Tabelle importiert wurde, klicken Sie auf **Schließen**.  

## <a name="add-a-table-with-user-name-data"></a>Hinzufügen einer Tabelle mit Benutzernamendaten  
Da die Tabelle dimEmployee in der Beispieldatenbank AdventureWorksDW Benutzer in der AdventureWorks-Domäne enthält und diese Benutzernamen in Ihrer Umgebung nicht vorhanden sind, müssen Sie eine Tabelle im Modell erstellen, die einen kleinen Teil (drei) der tatsächlichen Benutzer in der Organisation enthält. Als Nächstes fügen Sie diese Benutzer als Mitglieder der neuen Rolle hinzu. Die Kennwörter für die Beispielbenutzernamen sind nicht erforderlich, aber Sie müssen tatsächliche Windows-Benutzernamen Ihrer Domäne verwenden.  
  
#### <a name="to-add-an-employeesecurity-table"></a>Hinzufügen eine Tabelle EmployeeSecurity  
  
1.  Öffnen Sie Microsoft Excel, und erstellen Sie ein neues Arbeitsblatt.  
  
2.  Kopieren Sie die folgende Tabelle, einschließlich der Kopfzeile, und fügen Sie sie dann in das Arbeitsblatt ein.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Ersetzen Sie den Vornamen, Nachnamen und "Domäne\Benutzername" mit dem Namen und Anmelde-Ids von drei Benutzern in Ihrer Organisation ein. Platzieren Sie denselben Benutzer auf die ersten beiden Zeilen für EmployeeId-1. Dadurch wird angezeigt, dass der Benutzer zu mehreren Vertriebsgebieten gehört. Lassen Sie die Felder EmployeeId und SalesTerritoryId, wie sie sind.  
  
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
  
1.  Im Modell-Designer in der Diagrammsicht in der **DimGeography** Tabelle, klicken Sie auf, und halten Sie die **SalesTerritoryId** Spalte ziehen Sie dann den Cursor an die **SalesTerritoryId** Spalte in der **DimSalesTerritory** Tabelle, und klicken Sie dann freigeben.  
  
2.  In der **FactInternetSales** Tabelle, klicken Sie auf, und warten Sie, den **SalesTerritoryId** Spalte ziehen Sie dann den Cursor an die **SalesTerritoryId** Spalte in der  **DimSalesTerritory** Tabelle, und klicken Sie dann freigeben.  
  
    Beachten Sie, dass die Eigenschaft aktiv für diese Beziehung ist "false", was bedeutet, dass er nicht aktiv ist. Dies ist die FactInternetSales-Tabelle wurde bereits eine andere aktive Beziehung, die in Measures verwendet wird.  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a>Ausblenden der EmployeeSecurity-Tabelle in Clientanwendungen  
In dieser Aufgabe werden die Tabelle EmployeeSecurity ausgeblendet werden, da diese nicht angezeigt wird, in der Feldliste einer Clientanwendung. Denken Sie daran, dass eine Tabelle durch Ausblenden nicht gesichert wird. Benutzer können weiterhin die EmployeeSecurity Tabellendaten Abfragen, wenn sie wissen, wie. Wenden Sie schützten EmployeeSecurity-Tabellendaten, Benutzer daran gehindert, wird keine der Daten, Abfragen eines Filters in einer späteren Aufgabe an.  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a>So blenden Sie die EmployeeSecurity-Tabelle in Clientanwendungen aus  
  
-   Klicken Sie im Modell-Designer in der Diagrammsicht mit der rechten Maustaste auf die Tabellenkopfzeile **Employee** (Angestellter), und klicken Sie anschließend auf **Aus Clienttools ausblenden**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Erstellen der Benutzerrolle 'Sales Employees by Territory'  
In dieser Aufgabe erstellen Sie eine neue Benutzerrolle. Diese Rolle umfasst einen Zeilenfilter definieren, welche Zeilen der Tabelle DimSalesTerritory für Benutzer sichtbar sind. Der Filter wird dann in die Richtung der 1: n-Beziehung zu anderen Tabellen, die im Zusammenhang mit der dimsalesterritory-Tabelle angewendet. Sie gelten auch einen einfachen Filter, der sichert die gesamte EmployeeSecurity-Tabelle, damit jeder Benutzer, der Mitglied der Rolle ist.  
  
> [!NOTE]  
> Die Rolle Sales Employees by Territory, die Sie in dieser Lektion erstellen, schränkt Mitglieder ein, sodass sie nur Umsatzdaten für das Vertriebsgebiet suchen (oder abfragen) können, zu dem sie gehören. Wenn Sie einen Benutzer als Mitglied der Sales Employees Territory-Rolle, die auch vorhanden ist hinzugefügt, wie ein Element in einer Rolle in erstellt [Lektion 11: Erstellen von Rollen](../analysis-services/lesson-11-create-roles.md), erhalten Sie eine Kombination von Berechtigungen. Wenn ein Benutzer Mitglied mehrerer Rollen ist, sind die für jede Rolle definierten Berechtigungen und Zeilenfilter kumulativ. Der Benutzer verfügt also um mehr Berechtigungen, entsprechend der kombinierten Rollen.  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>So erstellen Sie die Benutzerrolle 'Sales Employees by Territory'  
  
1.  Klicken Sie in SSDT, auf die **Modell** Menü, und klicken Sie dann auf **Rollen**.  
  
2.  In **Rollen-Manager**, klicken Sie auf **neu**.  
  
    Der Liste wird eine neue Rolle mit der Berechtigung Keine hinzugefügt.  
  
3.  Klicken Sie auf die neue Rolle, und benennen Sie in der Spalte **Name** die Rolle in **Sales Employees by Territory**um.  
  
4.  Klicken Sie in der Spalte **Berechtigungen** auf die Dropdownliste, und wählen Sie anschließend die Berechtigung **Lesen** aus.  
  
5.  Klicken Sie auf die Registerkarte **Mitglieder** und anschließend auf **Hinzufügen**.  
  
6.  In der **Benutzer oder Gruppe auswählen** Dialogfeld **Geben Sie die zu verwendenden Objektnamen wählen**, geben Sie das erste Beispiel Benutzernamen ein, die Sie beim Erstellen der Tabelle EmployeeSecurity verwendet. Klicken Sie auf **Namen überprüfen** , um die Gültigkeit des Benutzernamens zu überprüfen, und klicken Sie anschließend auf **OK**.  
  
    Wiederholen Sie diesen Schritt, Hinzufügen von den anderen beispielbenutzernamen, die Sie beim Erstellen der Tabelle EmployeeSecurity verwendet werden soll.  
  
7.  Klicken Sie auf die Registerkarte **Zeilenfilter** .  
  
8.  Für die **EmployeeSecurity** -Tabelle in der **DAX-Filter** Spalte Geben Sie die folgende Formel.  
  
    ```
      =FALSE()  
    ```
  
    Diese Formel gibt an, dass alle Spalten in der falschen booleschen Bedingung aufgelöst. aus diesem Grund können keine Spalten für die Tabelle EmployeeSecurity von einem Mitglied der Sales Employees von Benutzerrolle Territory abgefragt werden.  
  
9. Geben Sie in der Tabelle **DimSalesTerritory** die folgende Formel ein.  

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
In dieser Aufgabe verwenden analysieren in Excel-Funktion in SSDT Sie die Wirksamkeit der Sales Employees Benutzerrolle Territory zu testen. Sie werden einen Benutzernamen angeben, die Sie der Tabelle EmployeeSecurity und als Mitglied der Rolle hinzugefügt. Dieser Benutzername wird dann als der gültige Benutzername in der zwischen Excel und dem Modell erstellten Verbindung verwendet.  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>So testen Sie die Benutzerrolle 'Sales Employees by Territory'  
  
1.  Klicken Sie in SSDT, auf die **Modell** Menü, und klicken Sie dann auf **in Excel analysieren**.  
  
2.  Wählen Sie im Dialogfeld **In Excel analysieren** in **Geben Sie den Benutzernamen oder die Rolle für die Verbindung mit dem Modell an**die Option **Anderer Windows-Benutzer**aus, und klicken Sie anschließend auf **Durchsuchen**.  
  
3.  In der **Benutzer oder Gruppe auswählen** Dialogfeld **Geben Sie die zu verwendenden Objektnamen**, geben Sie einen Benutzernamen, die Sie in der Tabelle EmployeeSecurity enthalten, und klicken Sie dann auf **Namen überprüfen**.  
  
4.  Klicken Sie auf **OK** , um das Dialogfeld **Benutzer oder Gruppe auswählen** zu schließen. Klicken Sie anschließend auf **OK** , um das Dialogfenster **In Excel analysieren** zu schließen.  
  
    Excel wird mit einer neuen Arbeitsmappe geöffnet. Automatisch wird eine PivotTable erstellt. Die PivotTable-Fields-Liste enthält die meisten Datenfelder im neuen Modell verfügbar sind.  
  
    Beachten Sie, dass die EmployeeSecurity-Tabelle nicht in der PivotTable-Fields-Liste angezeigt wird. Das liegt daran, dass Sie die Tabelle in der vorherigen Aufgabe aus den Clienttools ausgeblendet haben.  
  
5.  In der **Felder** Liste **∑ Internet Sales** (Measures), wählen Sie die **InternetTotalSales** Measure. Das Measure wird in die **Werte** -Felder eingegeben.  
  
6.  Wählen Sie die **SalesTerritoryId** Spalte aus der **DimSalesTerritory** Tabelle. Die Spalte wird in die **Zeilenbezeichnungen** -Felder eingegeben.  
  
    Die Internetumsatzzahlen werden nur für den einen Bereich angezeigt, dem der gültige Benutzername, den Sie verwendet haben, zugeordnet haben. Wenn Sie eine andere Spalte auswählen. z. B. City, aus der Tabelle DimGeography als Feld Zeilenbezeichnungen, nur Orte im Vertriebsgebiet, zu dem der gültige Benutzer gehört, werden angezeigt.  
  
    Dieser Benutzer kann nur Internetumsatzdaten des Gebiets, dem er zugeordnet ist, durchsuchen oder abfragen, da der für die Tabelle Sales Territory in der Benutzerrolle Sales Employees by Territory definierte Zeilenfilter eine effektive Sicherung der Daten in Bezug auf andere Vertriebsgebiete bedeutet.  
  
## <a name="see-also"></a>Siehe auch  
[USERNAME-Funktion (DAX)](http://msdn.microsoft.com/en-us/22dddc4b-1648-4c89-8c93-f1151162b93f)  
[LOOKUPVALUE-Funktion (DAX)](http://msdn.microsoft.com/en-us/73a51c4d-131c-4c33-a139-b1342d10caab)  
[CUSTOMDATA-Funktion (DAX)](http://msdn.microsoft.com/en-us/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
