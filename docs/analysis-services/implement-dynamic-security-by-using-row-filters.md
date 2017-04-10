---
title: "Implementieren von dynamischer Sicherheit mithilfe von Zeilenfiltern | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 8bf03c45-caf5-4eda-9314-e4f8f24a159f
caps.latest.revision: 15
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Implementieren von dynamischer Sicherheit mithilfe von Zeilenfiltern
In dieser ergänzenden Lektion erstellen Sie eine zusätzliche Rolle, die dynamische Sicherheit implementiert. Dynamische Sicherheit bietet Sicherheit auf Zeilenebene basierend auf dem Benutzernamen oder der Anmelde-ID des angemeldeten Benutzers. Weitere Informationen finden Sie unter [Rollen &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
Um dynamische Sicherheit zu implementieren, müssen Sie dem Modell eine Tabelle hinzufügen, die die Windows-Benutzernamen der Benutzer enthält, die eine Verbindung mit dem Modell als Datenquelle erstellen und Modellobjekte und Daten durchsuchen dürfen. In diesem Lernprogramm erstellen Sie ein Modell im Kontext der Adventure Works Corp. Sie müssen jedoch eine Tabelle mit Benutzern Ihrer Domäne hinzufügen, um diese Lektion abzuschließen. Die Kennwörter für die hinzuzufügenden Benutzernamen sind nicht erforderlich. Um die Tabelle Employee Security mit einem kleinen Teil der Benutzer Ihrer Domäne zu erstellen, verwenden Sie die Funktion Einfügen, und fügen Sie die Mitarbeiterdaten aus einem Excel-Arbeitsblatt ein. In der wirklichen Welt verwendet die Tabelle mit den Benutzernamen, die Sie einem Modell hinzugefügt haben, in der Regel eine Tabelle aus einer tatsächlichen Datenbank als Datenquelle, z. B. eine reale dimEmployee-Tabelle.  
  
Verwenden Sie die zwei neuen DAX-Funktionen ([USERNAME-Funktion (DAX)](http://msdn.microsoft.com/de-de/22dddc4b-1648-4c89-8c93-f1151162b93f) und [LOOKUPVALUE-Funktion (DAX)](http://msdn.microsoft.com/de-de/73a51c4d-131c-4c33-a139-b1342d10caab)), um dynamische Sicherheit zu implementieren. Diese Funktionen, die in einer Zeilenfilterformel angewendet werden, werden in einer neuen Rolle definiert. Die Formel gibt mit der LOOKUPVALUE-Funktion einen Wert aus der Tabelle Employee Security an und übergibt diesen Wert anschließend an die USERNAME-Funktion, die den Benutzernamen des angemeldeten Benutzers angibt, der ein Mitglied dieser Rolle ist. Der Benutzer kann dann nur die von den Zeilenfiltern der Rolle festgelegten Daten durchsuchen. In diesem Szenario legen Sie fest, dass Verkaufsmitarbeiter nur nach Internetumsatzdaten für die Vertriebsgebiete, denen sie angehören, suchen können.  
  
In dieser ergänzenden Lektion führen Sie eine Reihe von Aufgaben durch. Aufgaben, die nur für dieses Adventure Works-Szenario für die Tabellenmodellierung relevant sind und nicht unbedingt in der realen Welt anwendbar sind, werden als solche identifiziert. Jede Aufgabe umfasst weitere Informationen, die den Zweck der Aufgabe beschreiben.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **30 Minuten**  
  
## Erforderliche Komponenten  
Dieses ergänzende Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Sie sollten vor dem Ausführen der Aufgaben in dieser ergänzenden Lektion alle vorherigen Lektionen abgeschlossen haben.  
  
## Hinzufügen der dimSalesTerritory-Tabelle zum Projekt 'AW Internet Sales Tabular Model'  
Um dynamische Sicherheit für dieses Adventure Works-Szenario zu implementieren, müssen Sie dem Modell zwei weitere Tabellen hinzufügen. Die erste Tabelle, die Sie hinzufügen, ist die dimSalesTerritory-Tabelle (als Vertriebsgebiet) aus der gleichen AdventureWorksDW-Datenbank. Sie wenden später einen Zeilenfilter auf die Sales Territory-Tabelle an, der festlegt, welche Daten von angemeldeten Benutzern durchsucht werden können.  
  
#### So fügen Sie die Tabelle dimSalesTerritory hinzu  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]im Menü **Modell** auf **Vorhandene Verbindungen**.  
  
2.  Überprüfen Sie im Dialogfeld **Vorhandene Verbindungen**, ob die Datenquellenverbindung **Adventure Works DB from SQL** (Adventure Works-Datenbank aus SQL) ausgewählt ist, und klicken Sie anschließend auf **Öffnen**.  
  
    Wenn das Dialogfeld Identitätswechselinformationen angezeigt wird, geben Sie die Identitätswechsel-Anmeldeinformationen ein, die Sie in Lektion 2, "Hinzufügen von Daten", verwendet haben.  
  
3.  Behalten Sie auf der Seite **Auswählen, wie die Daten importiert werden sollen** die Auswahl der Option **Aus einer Liste von Tabellen und Sichten auswählen, um die zu importierenden Daten zu bestimmen** bei, und klicken Sie auf **Weiter**.  
  
4.  Wählen Sie auf der Seite **Tabellen und Sichten auswählen** die Tabelle **DimSalesTerritory** aus.  
  
5.  Geben Sie **Sales Territory** (Vertriebsgebiet) in die Spalte „Anzeigename“ ein.  
  
6.  Klicken Sie auf **Preview and Filter** (Vorschau anzeigen und filtern).  
  
7.  Heben Sie die Auswahl der Spalte **SalesTerritoryAlternateKey** auf, und klicken Sie anschließend auf **OK**.  
  
8.  Klicken Sie auf der Seite **Tabellen und Sichten auswählen** auf **Fertig stellen**.  
  
    Die neue Tabelle wird am Ende des Modellarbeitsbereichs hinzugefügt. Anschließend werden Objekte und Daten aus der Quelltabelle dimSalesTerritory in die Tabelle Sales Territory im Projekt "AW Internet Sales Tabular Model" importiert.  
  
9. Nachdem die Tabelle importiert wurde, klicken Sie auf **Schließen**.  
  
## Angeben der Anzeigenamen für Spalten  
In dieser Aufgabe benennen Sie die Spaltennamen der Tabelle Sales Territory um und legen Anzeigenamen für sie fest. Es ist nicht in jedem Fall notwendig, Anzeigenamen für Tabellen und/oder Spalten festzulegen. Es erleichtert jedoch das Navigieren im Modellprojekt im Modell-Designer und das Suchen von Modellobjekten und Daten in der Feldliste einer Clientanwendung.  
  
#### So benennen Sie Spalten in der Tabelle Sales Territory um  
  
-   Benennen Sie im Modell-Designer die Spalten in der Tabelle **Sales Territory** um:  
  
    **Sales Territory**  
  
    |Quellname|Anzeigename|  
    |---------------|-----------------|  
    |SalesTerritoryKey|Sales Territory Id|  
    |SalesTerritoryRegion|Sales Territory Region|  
    |SalesTerritoryCountry|Sales Territory Country|  
    |SalesTerritoryGroup|Sales Territory Group|  
  
## Hinzufügen einer Tabelle mit Benutzernamendaten  
Da die Tabelle dimEmployee in der Beispieldatenbank AdventureWorksDW Benutzer in der AdventureWorks-Domäne enthält und diese Benutzernamen in Ihrer Umgebung nicht vorhanden sind, müssen Sie eine Tabelle im Modell erstellen, die einen kleinen Teil (drei) der tatsächlichen Benutzer in der Organisation enthält. Als Nächstes fügen Sie diese Benutzer als Mitglieder der neuen Rolle hinzu. Die Kennwörter für die Beispielbenutzernamen sind nicht erforderlich, aber Sie müssen tatsächliche Windows-Benutzernamen Ihrer Domäne verwenden.  
  
#### So fügen Sie Tabelle Employee Security hinzu  
  
1.  Öffnen Sie Microsoft Excel, und erstellen Sie ein neues Arbeitsblatt.  
  
2.  Kopieren Sie die folgende Tabelle, einschließlich der Kopfzeile, und fügen Sie sie dann in das Arbeitsblatt ein.  
  
    |Employee Id|Sales Territory Id|First Name|Last Name|Login Id|  
    |---------------|----------------------|--------------|-------------|------------|  
    |1|2|<user first name>|<user last name>|\<Domäne\Benutzername>|  
    |1|3|<user first name>|<user last name>|\<Domäne\Benutzername>|  
    |2|4|<user first name>|<user last name>|\<Domäne\Benutzername>|  
    |3|5|<user first name>|<user last name>|\<Domäne\Benutzername>|  
  
3.  Ersetzen Sie im neuen Arbeitsblatt "Vorname", "Nachname" sowie "Domäne\Benutzername" durch die Namen und Anmelde-IDs von drei Benutzern in Ihrer Organisation. Verwenden Sie den gleichen Benutzer in den ersten beiden Zeilen für Employee Id 1. Dadurch wird angezeigt, dass der Benutzer zu mehreren Vertriebsgebieten gehört. Ändern Sie die Felder Employee Id und Sales Territory Id nicht.  
  
4.  Speichern Sie das Arbeitsblatt als **Sample Employee** (Beispielangestellter).  
  
5.  Wählen Sie im Arbeitsblatt alle Zellen mit Mitarbeiterdaten, einschließlich der Kopfzeilen, aus, klicken Sie mit der rechten Maustaste auf die ausgewählten Daten, und klicken Sie anschließend auf **Kopieren**.  
  
6.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] auf das Menü **Bearbeiten** und anschließend auf **Einfügen**.  
  
    Wenn „Einfügen“ abgeblendet dargestellt ist, klicken Sie im Modell-Designer-Fenster in einer beliebigen Tabelle auf eine Spalte, und klicken Sie anschließend auf das Menü **Bearbeiten** und auf **Einfügen**.  
  
7.  Geben Sie im Dialogfeld **Vorschau einfügen** unter **Tabellenname** den Text **Employee Security** (Angestelltensicherheit) ein.  
  
8.  Überprüfen Sie unter **Einzufügende Daten**, ob die Daten alle Benutzerdaten und Kopfzeilen aus dem Arbeitsblatt „Sample Employee“ enthalten.  
  
9. Überprüfen Sie, ob **Erste Zeile als Spaltenüberschriften verwenden** aktiviert ist, und klicken Sie anschließend auf **OK**.  
  
    Eine neue Tabelle mit dem Namen Employee Security wird mit den Mitarbeiterdaten aus dem Arbeitsblatt Sample Employee erstellt.  
  
## Erstellen von Beziehungen zwischen den Internet Sales-, Geography- und Sales Territory-Tabellen  
Die Tabellen Internet Sales, Geography und Sales Territory enthalten jeweils die Spalte Sales Territory Id. Die Spalte Sales Territory Id in der Tabelle Sales Territory enthält Werte mit einer anderen ID für jedes Vertriebsgebiet.  
  
#### So erstellen Sie Beziehungen zwischen den Tabellen Internet Sales, Geography und Sales Territory  
  
1.  Klicken Sie im Modell-Designer in der Diagrammansicht in der Tabelle **Geography** auf die Spalte **Sales Territory Id**, und halten Sie sie gedrückt. Verschieben Sie die Spalte mit dem Cursor per Drag & Drop in die Spalte **Sales Territory Id** der Tabelle **Sales Territory**, und veröffentlichen Sie sie.  
  
2.  Klicken Sie in der Tabelle **Internet Sales** (Internetvertrieb) auf die Spalte **Sales Territory Id** (ID des Vertriebsgebiets), und halten Sie die Maustaste gedrückt. Verschieben Sie die Spalte mit dem Cursor per Drag & Drop in die Spalte **Sales Territory Id** der Tabelle **Sales Territory** (Vertriebsgebiet), und veröffentlichen Sie sie.  
  
    Beachten Sie, dass die Eigenschaft Aktiv für diese Beziehung False ist, das bedeutet inaktiv. Das liegt daran, dass die Tabelle Internet Sales bereits eine andere aktive Beziehung aufweist, die in Measures verwendet wird.  
  
## Ausblenden der Employee Security-Tabelle in Clientanwendungen  
In dieser Aufgabe blenden Sie die Tabelle Employee Security aus, sodass sie nicht in der Feldliste einer Clientanwendung angezeigt wird. Denken Sie daran, dass eine Tabelle durch Ausblenden nicht gesichert wird. Benutzer können weiterhin Daten der Tabelle Employee Security abfragen, wenn sie über die nötigen Kenntnisse verfügen. Um die Daten der Tabelle Employee Security zu sichern, damit Benutzer keine der Daten abfragen können, wenden Sie in einer späteren Aufgabe einen Filter an.  
  
#### So blenden Sie die Employee Security-Tabelle in Clientanwendungen aus  
  
-   Klicken Sie im Modell-Designer in der Diagrammsicht mit der rechten Maustaste auf die Tabellenkopfzeile **Employee** (Angestellter), und klicken Sie anschließend auf **Aus Clienttools ausblenden**.  
  
## Erstellen der Benutzerrolle 'Sales Employees by Territory'  
In dieser Aufgabe erstellen Sie eine neue Benutzerrolle. Diese Rolle umfasst einen Zeilenfilter, der definiert, welche Zeilen der Tabelle Sales Territory für die Benutzer sichtbar sind. Der Filter wird dann über die 1:n-Beziehung auf alle anderen Tabellen angewendet, die mit der Tabelle Sales Territory verknüpft sind. Sie wenden außerdem einen einfachen Filter an, der die vollständige Tabelle Employee Security sichert, damit keine Benutzer, die Mitglied der Rolle sind, Daten in der Tabelle abfragen können.  
  
> [!NOTE]  
> Die Rolle Sales Employees by Territory, die Sie in dieser Lektion erstellen, schränkt Mitglieder ein, sodass sie nur Umsatzdaten für das Vertriebsgebiet suchen (oder abfragen) können, zu dem sie gehören. Wenn Sie einen Benutzer als Mitglied zu der Rolle „Sales Employees by Territory“ (Vertriebsangestellte nach Gebiet) hinzufügen und er auch Mitglied einer Rolle ist, die unter [Lektion 12: Erstellen von Rollen](../analysis-services/lesson-12-create-roles.md) erstellt wurde, werden die Berechtigungen kombiniert. Wenn ein Benutzer Mitglied mehrerer Rollen ist, sind die für jede Rolle definierten Berechtigungen und Zeilenfilter kumulativ. Der Benutzer verfügt also um mehr Berechtigungen, entsprechend der kombinierten Rollen.  
  
#### So erstellen Sie die Benutzerrolle 'Sales Employees by Territory'  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] auf das Menü **Modell** und anschließend auf **Rollen**.  
  
2.  Klicken Sie im Dialogfeld **Rollen-Manager** auf **Neu**.  
  
    Der Liste wird eine neue Rolle mit der Berechtigung Keine hinzugefügt.  
  
3.  Klicken Sie auf die neue Rolle, und benennen Sie in der Spalte **Name** die Rolle in **Sales Employees by Territory** um.  
  
4.  Klicken Sie in der Spalte **Berechtigungen** auf die Dropdownliste, und wählen Sie anschließend die Berechtigung **Lesen** aus.  
  
5.  Klicken Sie auf die Registerkarte **Mitglieder** und anschließend auf **Hinzufügen**.  
  
6.  Geben Sie im Dialogfeld **Benutzer oder Gruppe auswählen** unter **Geben Sie die zu verwendenden Objektnamen ein** den ersten Beispielbenutzernamen ein, den Sie beim Erstellen der Tabelle Employee Security verwendet haben. Klicken Sie auf **Namen überprüfen**, um die Gültigkeit des Benutzernamens zu überprüfen, und klicken Sie anschließend auf **OK**.  
  
    Wiederholen Sie diesen Schritt, und fügen Sie die anderen Beispielbenutzernamen hinzu, die Sie beim Erstellen der Tabelle Employee Security verwendet haben.  
  
7.  Klicken Sie auf die Registerkarte **Zeilenfilter**.  
  
8.  Geben Sie in der Tabelle **Employee Security** in der Spalte **DAX Filter** die folgende Formel ein.  
  
    **=FALSE()**  
  
    Drücken Sie nach dem Erstellen der Formel die EINGABETASTE.  
  
    Mit dieser Formel wird angegeben, dass alle Spalten in die boolesche Bedingung "False" aufgelöst werden. Aus diesem Grund können keine Spalten der Tabelle Employee Security von einem Mitglied der Benutzerrolle Sales Employees by Territory abgefragt werden.  
  
9. Geben Sie für die Tabelle **Sales Territory** die folgende Formel ein.  
  
    **='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 'Employee Security'[Login Id], USERNAME(), 'Employee Security'[Sales Territory Id], 'Sales Territory'[Sales Territory Id])**  
  
    Drücken Sie nach dem Erstellen der Formel die EINGABETASTE.  
  
    In dieser Formel gibt die LOOKUPVALUE-Funktion alle Werte für die Spalte "Employee Security[Sales Territory Id]" zurück, wobei "Employee Security[Login Id]" dem aktuell angemeldeten Windows-Benutzernamen entspricht und "Employee Security[Sales Territory Id]" gleich "Sales Territory[Sales Territory Id]" ist.  
  
    Der Sales Territory ID-Satz, der mit der LOOKUPVALUE-Funktion zurückgegeben wird, wird als Nächstes verwendet, um die in der Tabelle Sales Territory angezeigten Zeilen einzuschränken. Nur die Zeilen werden angezeigt, bei denen die Sales Territory ID der Zeile im Satz der IDs enthalten ist, die von der LOOKUPVALUE-Funktion zurückgegeben wurden.  
  
10. Klicken Sie im Dialogfeld „Rollen-Manager“ auf **OK**.  
  
## Testen der Benutzerrolle 'Sales Employees by Territory'  
In dieser Aufgabe verwenden Sie die Funktion In Excel analysieren in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], um die Wirksamkeit der Benutzerrolle Sales Employees by Territory zu testen. Geben Sie einen der Benutzernamen an, die Sie zur Tabelle Employee Security und als Mitglied der Rolle hinzugefügt haben. Dieser Benutzername wird dann als der gültige Benutzername in der zwischen Excel und dem Modell erstellten Verbindung verwendet.  
  
#### So testen Sie die Benutzerrolle 'Sales Employees by Territory'  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]auf das Menü **Modell** und dann auf **In Excel analysieren**.  
  
2.  Wählen Sie im Dialogfeld **In Excel analysieren** in **Geben Sie den Benutzernamen oder die Rolle für die Verbindung mit dem Modell an** die Option **Anderer Windows-Benutzer** aus, und klicken Sie anschließend auf **Durchsuchen**.  
  
3.  Geben Sie im Dialogfeld **Benutzer oder Gruppe auswählen** in **Geben Sie die zu verwendenden Objektnamen ein** einen der Benutzernamen ein, die in der Tabelle „Employee“ enthalten sind, und klicken Sie anschließend auf **Namen überprüfen**.  
  
4.  Klicken Sie auf **OK**, um das Dialogfeld **Benutzer oder Gruppe auswählen** zu schließen. Klicken Sie anschließend auf **OK**, um das Dialogfenster **In Excel analysieren** zu schließen.  
  
    Excel wird mit einer neuen Arbeitsmappe geöffnet. Es wird automatisch eine PivotTable erstellt. Die PivotTable-Feldliste enthält die meisten Datenfelder, die im neuen Modell verfügbar sind.  
  
    Die Tabelle Employee Security wird in der PivotTable-Feldliste nicht angezeigt. Das liegt daran, dass Sie die Tabelle in der vorherigen Aufgabe aus den Clienttools ausgeblendet haben.  
  
5.  Wählen Sie in der **PivotTable-Feldliste** in **∑ Internet Sales** (Measures) das Measure **Internet Total Sales** (Internetgesamtvertrieb) aus. Das Measure wird in die **Werte**-Felder eingegeben.  
  
6.  Wählen Sie in der **PivotTable-Feldliste** die Spalte **Sales Territory Id** in der Tabelle **Sales Territory** aus. Die Spalte wird in die **Zeilenbezeichnungen**-Felder eingegeben.  
  
    Die Internetumsatzzahlen werden nur für den einen Bereich angezeigt, dem der gültige Benutzername, den Sie verwendet haben, zugeordnet haben. Wenn Sie eine andere Spalte, z. B. City, aus der Tabelle Geography als Feld Zeilenbezeichnungen auswählen, werden nur Orte im Vertriebsgebiet, zu dem der gültige Benutzer gehört, angezeigt.  
  
    Dieser Benutzer kann nur Internetumsatzdaten des Gebiets, dem er zugeordnet ist, durchsuchen oder abfragen, da der für die Tabelle Sales Territory in der Benutzerrolle Sales Employees by Territory definierte Zeilenfilter eine effektive Sicherung der Daten in Bezug auf andere Vertriebsgebiete bedeutet.  
  
## Siehe auch  
[USERNAME-Funktion (DAX)](http://msdn.microsoft.com/de-de/22dddc4b-1648-4c89-8c93-f1151162b93f)  
[LOOKUPVALUE-Funktion (DAX)](http://msdn.microsoft.com/de-de/73a51c4d-131c-4c33-a139-b1342d10caab)  
[CUSTOMDATA-Funktion (DAX)](http://msdn.microsoft.com/de-de/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
  
