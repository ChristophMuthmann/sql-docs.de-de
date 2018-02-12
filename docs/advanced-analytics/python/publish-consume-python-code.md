---
title: "Veröffentlichen und Nutzen von Python-Code | Microsoft Docs"
ms.custom: 
ms.date: 11/09/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 8720440872fb0b41a76d4ac644fd3b60d52a095e
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="publish-and-consume-python-web-services"></a>Veröffentlichen und Nutzen von Webdiensten Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Sie können eine funktionierende Lösung Python an einen Webdienst mithilfe der operationalisierung-Funktion im Microsoft Machine Learning-Server bereitstellen. Dieses Thema beschreibt die Schritte zum Veröffentlichen erfolgreich, und führen Sie die Projektmappe.

Die Zielgruppe für diesen Artikel ist die Datenanalysten, die Informationen zum Veröffentlichen von Python-Code oder Modelle als Webdienste, die im Microsoft Machine Learning-Server gehostet werden soll. Außerdem erfahren Sie, wie Anwendungen nutzen können die den Code oder Modelle. In diesem Artikel wird davon ausgegangen, dass Sie in Python versiert sind.

> [!IMPORTANT]
>
> Dieses Beispiel wurde entwickelt, für die Version von Python, die mit Machine Learning-Server (eigenständig) enthalten ist, und verwendet Funktionen in Machine Learning-Serverversion **9.1.0**.
 > 
 > Klicken Sie auf den folgenden Link, um die gleichen Beispiel erneut veröffentlicht, mithilfe der neueren Bibliotheken in Machine Learning-Server finden Sie unter. Finden Sie unter [bereitstellen und Verwalten von Webdiensten in Python](https://docs.microsoft.com/machine-learning-server/operationalize/python/how-to-deploy-manage-web-services).

**Gilt für: Microsoft R Server (eigenständig)**

## <a name="overview-of-workflow"></a>Übersicht über Workflows

Der Workflow bei der Veröffentlichung für die Nutzung eines Webdiensts Python kann wie folgt zusammengefasst werden:

1. Erfüllen der [Voraussetzung](#prereq) die Python-Clientbibliothek aus dem Core Swagger-API-Dokument generieren.
2. Authentifizierung und Header Logik für das Python-Skript hinzufügen.
3. Erstellen Sie eine Python-Sitzung, Vorbereiten der Umgebung, und erstellen Sie eine Momentaufnahme die Umgebung beibehalten, um.
4. Veröffentlichen Sie der Webdienst, und binden Sie diese Momentaufnahme.
5. Probieren Sie den Webdienst aus, durch die Nutzung von es in Ihrer Sitzung.
6. Diese Dienste zu verwalten.

![Swagger-workflow](./media/data-scientist-python-workflow.png)

Dieser Artikel beschreibt jeden Schritt des Workflows und Python-Beispielcode verwenden das Iris-Dataset enthält.

## <a name="sample-code"></a>Beispielcode

In diesem Beispielcode wird vorausgesetzt, Sie wurden erfüllt die [Voraussetzungen](#prereq) zum Generieren von einer Python-Clientbibliothek aus dieser Swagger-Datei, und dass Sie verwendet haben Autorest.

Nachdem der Codeblock finden Sie eine schrittweise exemplarische Vorgehensweise mit ausführlicheren Beschreibungen zu den gesamten Prozess.

> [!IMPORTANT]
> Dieses Beispiel verwendet die lokale `admin` Konto für die Authentifizierung. Sie sollten jedoch die Anmeldeinformationen ersetzen und [Authentifizierungsmethode](#python-auth) von Ihrem Administrator konfiguriert werden.

```python
##################################################
##       IMPORT GENERATED CLIENT LIBRARY        ##
##################################################

# Import the generated client library. 

import deployrclient

# This example is intended for use with Microsoft R Server 9.0.1. 
# If you are using a newer version of Machine Learning Server, 
# use the mrs_server library instead.

##################################################
##              AUTHENTICATION                  ##
##################################################

#Using client library generated from Autorest
#Create client instance and point it at an R Server. 
#In this case, R Server is local.
client = deployrclient.DeployRClient("http://localhost:12800")
# To use ML Server, replace with mrs_server.MRSServer()

#Define the login request and provide credentials 
#Update values with the connection parameters from your admin
login_request = deployrclient.models.LoginRequest("<<your-username>>","<<your-password>>")

#Make a call to the /login API. 
#Store the returned an access token in a variable.
token_response = client.login(login_request)

#Add the returned access token to the headers variable.
headers = {"Authorization": "Bearer {0}".format(token_response.access_token)}

#Verify that the server is running.
#Remember to include `headers` in all requests!
status_response = client.status(headers) 
print(status_response.status_code)


##################################################
##        CREATE SESSION, MODEL, SNAPSHOT       ##
##################################################

#Since already logged in, create a Python session.
#Define session using name (`Session 1`) and `runtime_type="Python"`.
#Remember to specify the Python runtime type.
create_session_request = deployrclient.models.CreateSessionRequest("Session 1", runtime_type="Python")

#Make the call to start the session. 
#Remember to include headers in all method calls to the server.
#Returns a session ID.
response = client.create_session(create_session_request, headers) 
   
#Store the session ID in a variable called `session_id` 
#to be able to identify it later at execution time.
session_id = response.session_id

#Create model - Import SVM and datasets from the SciKit-Learn library
execute_request = deployrclient.models.ExecuteRequest("from sklearn import svm\nfrom sklearn import datasets")
execute_response = client.execute_code(session_id,execute_request, headers)
#Report if it was a success
execute_response.success
   
#Define the untrained Support Vector Classifier (SVC) object
#and the dataset to be preloaded.
execute_request = deployrclient.models.ExecuteRequest("clf=svm.SVC()\niris=datasets.load_iris()\nnames={0:'I. setosa',1:'I. versicolor',2:'I. virginica'}")
#Now, go create the object and preload Iris Dataset in R Server
execute_response = client.execute_code(session_id,execute_request, headers)
#Report if it was a success
execute_response.success
   
#Define two rows from the Iris Dataset as a sample for scoring
workspace_object = deployrclient.models.WorkspaceObject("species_1",[7,3.2,4.7,1.4])
workspace_object_2 = deployrclient.models.WorkspaceObject("species_2",[3,2.6,3,2.5])

#Define how to train the classifier model; what to predict; what to return
execute_request = deployrclient.models.ExecuteRequest(
    "clf.fit(iris.data, iris.target)\n"+
    "result=clf.predict(species_1)\n"+
    "other_result=clf.predict(species_2)",
    [workspace_object,workspace_object_2], #Input
    ["result", "other_result"]) #Output

#Now, go train that model on the Iris Dataset in R Server
execute_response = client.execute_code(session_id,execute_request, headers)

#If successful, print name and result of each output parameter. Else, print error.
if(execute_response.success):
    for result in execute_response.output_parameters:
        print("{0}: {1}".format(result.name,result.value))
else:
    print (execute_response.error_message)

#Create a snapshot of the current session
response = client.create_snapshot(session_id, deployrclient.models.CreateSnapshotRequest("Iris Snapshot"), headers)
#Return the snapshot ID for reference when you publish later.
response.snapshot_id
#If you forget the ID, list snapshots to get the ID again.
for snapshot in client.list_snapshots(headers):
    print(snapshot)

##################################################
##        PUBLISH AS A SERVICE IN PYTHON        ##
##################################################

#Define a web service that determines the iris species by scoring 
#a vector of sepal length and width, petal length and width

#Set `flower_data` for the sepal and petal length and width
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
#Set `iris_species` for the species of iris
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "vector")

#Define the publish request for the web service and its arguments.
#Specify the code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
       code = "iris_species = [names[x] for x in clf.predict(flower_data)]", 
       input_parameter_definitions = [flower_data], 
       output_parameter_definitions = [iris_species],
       runtime_type = "Python",
       snapshot_id = response.snapshot_id)

#Publish the service using the specified name (iris), version (V1.0)
client.publish_web_service_version("Iris", "V1.0", publish_request, headers)

##################################################
##           CONSUME SERVICE IN PYTHON          ##
##################################################

# Inspect holdings and metadata for service Iris V1.0.
for service in client.get_web_service_version("Iris","V1.0", headers):
    #print service metadata (description, who published,...)
    print(service)
    #Print input and output parameters as defined in service definition object
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))

#Import the requests library to make requests on the server
import requests
#Import the JSON library to use for pretty printing of json responses
import json

#Create a requests `Session` object.
s = requests.Session()

#Record the R Server endpoint URL hosting the web services you created before
url = "http://localhost:12800"

#Give the request.Session object the authentication headers 
#so you don't have to repeat it with each request.
s.headers = headers

#Retrieve the service-specific swagger file using the requests library.
swagger_resp = s.get(url+"/api/Iris/V1.0/swagger.json")

#Either, download service-specific swagger file using the json library.
with open('iris_swagger.json','w') as f:
   (json.dump(client.get_web_service_swagger("Iris","V1.0",headers),f, indent = 1))

#Or, print just what you need from the Swagger file, 
#such as the routing paths for the endpoints to be consumed.
print(json.dumps(swagger_resp.json()["paths"], indent = 1, sort_keys = True))

#Or, print input and output parameters as defined in the Swagger.io format
print("Input")
print(json.dumps(swagger_resp.json()["definitions"]["InputParameters"], indent = 1, sort_keys = True))
print("Output")
print(json.dumps(swagger_resp.json()["definitions"]["WebServiceResult"], indent = 1, sort_keys = True))

#Make the request to consume the service using these flower_data inputs
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[7,3.2,4.7,1.4]})
#Print the output
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Use input from another Iris species.
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[3,2.6,3,2.5]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Use input from another Iris species.
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

##################################################
##          MANAGE SERVICES IN PYTHON           ##
##################################################

#Define what needs to be updated. Here we add a description.
#Be sure to specify the runtime_type again.
update_request = deployrclient.models.PublishWebServiceRequest(
    description = "Determines iris species using length and width of sepal and petal", runtime_type = "Python")
#Now update it by specifying the service name and version number
client.patch_web_service_version("Iris", "V1.0", update_request, headers)

#Or, publish another version of the web service, but this time 
#the service returns the species as a string instead of list of strings.
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "string")
 
#Define the publish request for the service and its arguments.
#Specify the changed code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
    code = "iris_species = [names[x] for x in clf.predict(flower_data)][0]",
    description = "Determines the species of iris, based on Sepal Length, Sepal Width, Petal Length and Petal Width",
    input_parameter_definitions = [flower_data],
    output_parameter_definitions = [iris_species],
    runtime_type = "Python",
    snapshot_id = response.snapshot_id)
 
#Now, publish the service with version (V2.0)
client.publish_web_service_version("Iris", "V2.0", publish_request, headers)
 
#Make request to consume service using these flower_data inputs; print output
resp = s.post(url+"/api/Iris/V2.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Return the list of all existing web services.
for service in client.get_all_web_services(headers):
    #print the service information
    print(service)
    #Print each input and output parameter
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))

#Delete the second version we just published.
client.delete_web_service_version("Iris","V2.0",headers)
```

## <a name="walkthrough"></a>Exemplarische Vorgehensweise

In diesem Abschnitt wird beschrieben, wie der Code im Detail funktioniert.


### <a name="prereq"></a>Schritt 1. Erstellen der erforderlichen Client-Bibliotheken

Bevor Sie beginnen können, die Python-Code und Modelle gestaltet Microsoft Machine Learning-Server veröffentlichen, müssen Sie eine Clientbibliothek, mit der in dieser Version bereitgestellte Swagger-Dokument generieren.

1. Eine Swagger-Code-Generators auf dem lokalen Computer installieren, und machen Sie sich damit vertraut. Sie werden zum Generieren von API-Client-Bibliotheken in Python verwendet. Beliebte umfassen [Azure AutoRest](https://github.com/Azure/autorest) (erfordert Node.js) und [Swagger Codegen](https://github.com/swagger-api/swagger-codegen). 

2. Herunterladen der Swagger-Datei, die die Kern-APIs für Ihre Version von Machine Learning-Server enthält. Diese Datei enthält eine Swagger-Vorlage definiert die Liste der REST-Ressourcen und die Vorgänge, die auf diese Ressourcen aufgerufen werden können. Sie finden diese Datei unter `https://microsoft.github.io/deployr-api-docs/swagger/<version>/rserver-swagger-<version>.json`, wobei `<version>` ist die Versionsnummer der 3-stelliger R-Server. 

   Z. B. R Server 9.1 Sie würde von herunterladen: https://microsoft.github.io/deployr-api-docs/9.1.0/swagger/rserver-swagger-9.1.0.json

3. Generieren Sie die statisch generierte Client-Bibliothek durch Übergeben der `rserver-swagger-<version>.json` Datei wird in der Swagger-Code-Generator und Angeben der Sprache werden sollen. In diesem Fall sollten Sie Python angeben.  

    Z. B. Wenn Sie AutoRest verwenden, um eine Python-Clientbibliothek zu generieren, kann er wie folgt, aussehen, wobei die Anzahl der 3-stelliger R Server-Versionsnummer darstellt:
    
    `AutoRest.exe -Input rserver-swagger-9.1.0.json -CodeGenerator Python  -OutputDirectory C:\Users\rserver-user\Documents\Python`

4. Sie können auch einige benutzerdefinierte Header angeben und andere Änderungen vornehmen, bevor der generierte Client Library Stub. Finden Sie unter der [Command Line Interface](https://github.com/Azure/autorest/blob/master/docs/user/cli.md) Dokumentation auf GitHub zu Details in Bezug auf verschiedene Konfigurationsoptionen und Einstellungen, wie z. B. den Namespace umbenennen.
   
5. Untersuchen Sie die Core-Clientbibliothek, um die verschiedenen API-Aufrufe, die Sie vornehmen können, finden Sie unter. 

    In unserem Beispiel generiert Autorest bestimmte Verzeichnisse und Dateien für die Python-Clientbibliothek auf Ihr lokales System. Der Namespace (und Verzeichnis) werden standardmäßig `deployrclient` und kann wie folgt aussehen:
   
   ![Ausgabepfad Autorest](./media/data-scientist-python-autorest.png)

    Für diesen Standardnamespace wird die Clientbibliothek selbst aufgerufen `deploy_rclient.py`. Wenn Sie diese Datei in die IDE wie Visual Studio öffnen, sehen Sie etwa so aussehen:
   
   ![Python-Clientbibliothek](./media/data-scientist-python-client-library.png)


### <a name="step-2-add-authentication-and-header-logic"></a>Schritt 2: Authentifizierung und Header Logik hinzufügen

Bedenken Sie, dass alle APIs Authentifizierung erforderlich ist; aus diesem Grund müssen alle Benutzer authentifizieren, beim Bereitstellen einer API, rufen Sie mithilfe der `POST /login` API oder über Azure Active Directory (AAD). 

Zur Vereinfachung dieses Vorgangs werden Träger Zugriffstoken ausgegeben, damit Benutzer ihre Anmeldeinformationen nicht bei jedem Aufruf bereitstellen müssen.  Diese trägertoken ist ein einfaches Sicherheitstoken, die dem "Träger" Zugriff auf eine geschützte Ressource gewährt: in diesem Fall wird der Machine Learning-Server-APIs. Nachdem ein Benutzer authentifiziert wurde, muss die Anwendung überprüfen, Bearer-Token des Benutzers, um sicherzustellen, dass die Authentifizierung der vorgesehenen Personen erfolgreich war. Weitere Informationen zum Verwalten dieser Tokens finden Sie unter [Sicherheit Zugriffstoken](https://msdn.microsoft.com/microsoft-r/operationalize/security-access-tokens).

Bevor Sie mit den APIs interagieren, zunächst authentifiziert werden, erhalten die Träger-Tokens mithilfe der [Authentifizierungsmethode](https://msdn.microsoft.com/microsoft-r/operationalize/security-authentication) von Ihrem Administrator konfiguriert, und fügen Sie ihn in jeder Kopfzeile für jede nachfolgende Anforderung:

1. Erste Schritte, durch das Importieren der Clientbibliothek, um über Ihre bevorzugte Python Code-Editor, z. B. Jupyter, Visual Studio, Visual Studio Code oder iPython zu vereinfachen.

   Geben Sie das übergeordnete Verzeichnis der Clientbibliothek. In unserem Beispiel ist die Autorest generierte Client-Bibliothek unter `C:\Users\rserver-user\Documents\Python\deployrclient`:

   ```python
   # Import the generated client library
   import deployrclient
   ```

2. Fügen Sie die Authentifizierungslogik an der Anwendung, definieren eine Verbindung von Ihrem lokalen Computer zu Machine Learning-Server, geben Sie die Anmeldeinformationen, erfassen das Zugriffstoken, fügen dieses Token, die dem Header hinzu. Anschließend verwenden Sie diesen Header für alle nachfolgenden Anforderungen an.  Verwenden Sie die Authentifizierungsmethode, die vom Administrator definierten: grundlegende Administratorkonto, Active Directory/LDAP (AD/LDAP) oder Azure Active Directory (AAD).

   **AD/LDAP oder `admin` Kontoauthentifizierung**

   Rufen Sie die `POST /login` API, um sich zu authentifizieren. Übergeben Sie die `username` und `password` für den lokalen Administrator oder wenn Active Directory aktiviert ist, übergeben Sie die LDAP-Kontoinformationen. Machine Learning-Server stellt wiederum eine Träger/Access-Token aus. Nach der Authentifizierung, benötigt der Benutzer nicht mehr auf die Anmeldeinformationen erneut bereitstellen, solange das Token noch gültig ist und ein Header mit jeder Anforderung übermittelt wird. Wenn Sie die Verbindungseinstellungen nicht kennen, wenden Sie sich an Ihren Administrator.

   ```python
   #Using client library generated from Autorest
   #Create client instance and point it at an R Server. 
   #In this case, R Server is local.
   client = deployrclient.DeployRClient("http://localhost:12800")
   
   #Define the login request and provide credentials. 
   #Update values with the connection parameters from your admin.
   login_request = deployrclient.models.LoginRequest("<<your-username>>","<<your-password>>")
   #Make a call to the /login API. 
   #Store the returned an access token in a variable.
   token_response = client.login(login_request)
   ```

   **Azure Active Directory (AAD)-Authentifizierung**

   Übergeben Sie die AAD-Anmeldeinformationen, die Zertifizierungsstelle und die Client-ID AAD wiederum stellt die [Zugriff trägertoken](https://msdn.microsoft.com/microsoft-r/operationalize/security-access-tokens). Nach der Authentifizierung, benötigt der Benutzer nicht mehr auf die Anmeldeinformationen erneut bereitstellen, solange das Token noch gültig ist und ein Header mit jeder Anforderung übermittelt wird. Wenn Sie die Verbindungseinstellungen nicht kennen, wenden Sie sich an Ihren Administrator.

   ```python
   #Import the AAD authentication library
   import adal
   
   #Define the login request and provide credentials. 
   #Use the AAD connection parameters provided by your admin.
   url = "http://localhost:12800"
   authuri = https://login.windows.net,
   tenantid = "<<AAD_DOMAIN>>", 
   clientid = "<<NATIVE_APP_CLIENT_ID>>", 
   resource = "<<WEB_APP_CLIENT_ID>>", 
   
   #Acquire authentication token using AAD Device Code Login
   context = adal.AuthenticationContext(authuri+'/'+tenantid, api_version=None)
   code = context.acquire_user_code(resource, clientid)
   print(code['message'])
   token = context.acquire_token_with_device_code(resource, code, clientid)
   #The authentication code returned must be entered at https://aka.ms/devicelogin 
   ```     

3. Hinzufügen der `Bearer` Zugriff auf Token und sicher, dass Machine Learning-Server derzeit ausgeführt wird.  Dieses Token zurückgegeben wurde, während der Authentifizierung und **müssen in jedem nachfolgenden Anforderungsheader enthalten**. Dieses Beispiel verwendet eine Clientbibliothek von Autorest generiert.

   > [!IMPORTANT]
   > Jede API-Aufruf muss authentifiziert werden. Vergessen Sie daher-Header mit Token, um jede einzelne Anforderung enthalten sind.

   ```python
   #Add the returned access token to the headers variable.
   headers = {"Authorization": "Bearer {0}".format(token_response.access_token)}
   
   #Verify that the server is running.
   #Remember to include `headers` in every request!
   status_response = client.status(headers) 
   print(status_response.status_code)
   ```

### <a name="step-3-prepare-session-and-code"></a>Schritt 3: Vorbereiten von Sitzung und code

Nach der Authentifizierung können Sie eine Python-Sitzung zu starten und erstellen Sie ein Modell für die Veröffentlichung von einem späteren Zeitpunkt. Sie können eine beliebige Python-Code oder die Modelle in einem Webdienst einschließen. Nachdem Sie Ihre Umgebung für die Sitzung eingerichtet haben, können Sie auch speichern, als Momentaufnahme um Ihre Sitzung geladen werden kann, wie Sie ihn ein, bevor hatten. 

> [!IMPORTANT]
> Denken Sie daran, `headers` bei jeder Anforderung.

1. Erstellen Sie eine Python-Sitzung auf R-Server. Achten Sie darauf, dass Sie einen Namen und die Sprache Python angeben (`runtime_type="Python"`).  Wenn Sie Python den Laufzeittyp nicht festlegen, wird standardmäßig R.

   Dies ist eine Fortsetzung des Beispiels mithilfe der Clientbibliothek von Autorest generiert:

   ```python
   #Since already logged in, create a Python session.
   #Define session using name (`Session 1`) and `runtime_type="Python"`.
   #Remember to specify the Python runtime type.
   create_session_request = deployrclient.models.CreateSessionRequest("Session 1", runtime_type="Python")
   
   #Make the call to start the session. 
   #Remember to include headers in every method call to the server.
   #Returns a session ID.
   response = client.create_session(create_session_request, headers) 
   
   #Store the session ID in a variable called `session_id` 
   #to be able to identify it later at execution time.
   session_id = response.session_id
   ```

2. Erstellen Sie, oder rufen Sie ein Modell in Python, die Sie als Webdienst veröffentlichen werde

   In diesem Beispiel wird ein SciKit erfahren Sie Support Vektor Computer (SVM) Modell trainieren Iris-Dataset auf einer Remoteinstanz von Machine Learning-Server.  Dieses Dataset steht über den [Scikit-Website erfahren](http://scikit-learn.org/stable/auto_examples/datasets/plot_iris_dataset.html).

   ```python
   #Import SVM and datasets from the SciKit-Learn library
   execute_request = deployrclient.models.ExecuteRequest("from sklearn import svm\nfrom sklearn import datasets")
   execute_response = client.execute_code(session_id,execute_request, headers)
   #Report if it was a success
   execute_response.success
   
   #Define the untrained Support Vector Classifier (SVC) object
   #and the dataset to be preloaded.
   execute_request = deployrclient.models.ExecuteRequest("clf=svm.SVC()\niris=datasets.load_iris()\nnames={0:'I. setosa',1:'I. versicolor',2:'I. virginica'}")
   #Now, go create the object and preload Iris Dataset in R Server
   execute_response = client.execute_code(session_id,execute_request, headers)
   #Report if it was a success
   execute_response.success
   
   #Define two rows from the Iris Dataset as a sample for scoring
   workspace_object = deployrclient.models.WorkspaceObject("species_1",[7,3.2,4.7,1.4])
   workspace_object_2 = deployrclient.models.WorkspaceObject("species_2",[3,2.6,3,2.5])

   #Define how to train the classifier model; what to predict; what to return
   execute_request = deployrclient.models.ExecuteRequest(
       "clf.fit(iris.data, iris.target)\n"+
       "result=clf.predict(species_1)\n"+
       "other_result=clf.predict(species_2)",
       [workspace_object,workspace_object_2], #Input
       ["result", "other_result"]) #Output

   #Now, go train that model on the Iris Dataset in R Server
   execute_response = client.execute_code(session_id,execute_request, headers)

   #If successful, print name and result of each output parameter. Else, print error.
   if(execute_response.success):
       for result in execute_response.output_parameters:
           print("{0}: {1}".format(result.name,result.value))
   else:
       print (execute_response.error_message)
   ```

3. Erstellen Sie eine Momentaufnahme dieser Python Sitzung, damit diese Umgebung im Webdienst gespeichert und an reproduziert werden kann Zeit beanspruchen. Momentaufnahmen sind nützlich, wenn Sie eine vorbereitete Umgebung benötigt werden, die bestimmte Bibliotheken, Objekte, Modelle, Dateien und Elemente enthält. Momentaufnahmen der gesamten-Arbeitsbereichs und das Arbeitsverzeichnis zu speichern. Allerdings können beim Veröffentlichen Sie nur Momentaufnahmen verwenden, die Sie erstellt haben.

   ```python
   #Create a snapshot of the current session.
   response = client.create_snapshot(session_id, deployrclient.models.CreateSnapshotRequest("Iris Snapshot"), headers)
   
   #Return the snapshot ID for reference when you publish later.
   response.snapshot_id
   
   #If you forget the ID, list snapshots to get the ID again.
   for snapshot in client.list_snapshots(headers):
       print(snapshot)
   ```

  > [!NOTE] 
   > Obwohl Momentaufnahmen auch verwendet werden können bei der Veröffentlichung von eines Webdienst für die Umgebung Abhängigkeiten, kann es auf die Leistung der Zeit Verbrauch auswirken.  Berücksichtigen Sie für eine optimale Leistung die Größe der Momentaufnahme, und stellen Sie sicher, dass Sie nur die Arbeitsbereichsobjekte beibehalten, die Sie benötigen, und löschen den Rest. In einer Sitzung können Sie die Python `del` Funktion oder [der `deleteWorkspaceObject` -API-Anforderung](https://microsoft.github.io/deployr-api-docs/#delete-workspace-object) unnötige Objekte zu entfernen. 

### <a name="step-4-publish-the-model"></a>Schritt 4. Das Modell veröffentlichen 

Nachdem Sie Ihre Clientbibliothek wurde generiert, und Sie haben Ihre Anwendung die Authentifizierungslogik integriert, können Sie interagieren mit den APIs für eine Python-Sitzung erstellen, ein Modell erstellen und veröffentlichen Sie einen Webdienst, der anhand dieses Modells.

Einige Dinge zu beachten:

+ Sie müssen authentifiziert werden, bevor Sie alle API-Aufrufe ausführen. Daher enthalten `headers` in allen Anforderungen.
+ Um sicherzustellen, dass der Webdienst als ein Python-Dienst registriert ist, müssen Sie angeben `runtime_type="Python"`. Wenn Sie Python den Laufzeittyp nicht festlegen, wird standardmäßig R.
+ Bewertung erfordert einen Vektor mit Sepal-Length, Sepal Breite, sodass Länge und Breite des Blatts

Im folgende Code werden die SVM-Modell als Webdienst Python veröffentlicht. Dieser Webdienst generiert eine vorhergesagte Kategorie basierend auf Werten, die an sie übergeben.

```python
   #Set `flower_data` for the sepal and petal length and width
   flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
   #Set `iris_species` for the species of iris
   iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "vector")
   
   #Define the publish request for the web service and its arguments.
   #Specify the code, inputs, outputs, and snapshot.
   #Don't forget to set runtime_type="Python"`.
   publish_request = deployrclient.models.PublishWebServiceRequest(
       code = "iris_species = [names[x] for x in clf.predict(flower_data)]", 
       input_parameter_definitions = [flower_data], 
       output_parameter_definitions = [iris_species],
       runtime_type = "Python",
       snapshot_id = response.snapshot_id)

   #Publish the service using the specified name (iris), version (V1.0)
   client.publish_web_service_version("Iris", "V1.0", publish_request, headers)
```

### <a name="step-5-consume-the-web-service"></a>Schritt 5. Nutzen Sie den Webdienst

In diesem Abschnitt wird veranschaulicht, wie den Dienst in derselben Sitzung verarbeitet werden, in dem es erstellt wurde.

1. Erhalten Sie in der gleichen Sitzung Service betrieben und Metadaten für den Dienst ein.

   ```python
   # Inspect holdings and metadata for service Iris V1.0.
   for service in client.get_web_service_version("Iris","V1.0", headers):
       #print service metadata (description, who published,...)
       print(service)
       #Print input and output parameters as defined in service definition object
       print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
       print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))
   ```

2. Überprüfen Sie die Dienst betrieben und Vorbereiten Sie der nutzen. 
   ```python
   #Import the requests library to make requests on the server
   import requests
   #Import the JSON library to use for pretty printing of json responses
   import json

   #Create a requests `Session` object.
   s = requests.Session()

   #Record the R Server endpoint URL hosting the web services you created
   url = "http://localhost:12800"

   #Include the request.Session object in the authentication headers.
   #By doing so, you don't need to repeat it with each request.
   s.headers = headers

   # Retrieve the service-specific Swagger file using the requests library.
   swagger_resp = s.get(url+"/api/Iris/V1.0/swagger.json")

   #You can download a service-specific Swagger file using the json library.
   with open('iris_swagger.json','w') as f:
      (json.dump(client.get_web_service_swagger("Iris","V1.0",headers),f, indent = 1))

   #Or, you can print just what you need from the Swagger file. 
   #This example gets the routing paths for the endpoints to be consumed.
   print(json.dumps(swagger_resp.json()["paths"], indent = 1, sort_keys = True))

   #You can also print input and output parameters as defined in the Swagger.io format
   print("Input")
   print(json.dumps(swagger_resp.json()["definitions"]["InputParameters"], indent = 1, sort_keys = True))
   print("Output")
   print(json.dumps(swagger_resp.json()["definitions"]["WebServiceResult"], indent = 1, sort_keys = True))
   ```

3. Nutzen Sie den Dienst durch Angabe einige Eingabe- und Iris Arten abrufen. 
   ```python
   #Make the request to consume the service using these flower_data inputs
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[7,3.2,4.7,1.4]})
   #Print the output
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))

   ##Use input from another Iris species.
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[3,2.6,3,2.5]})
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))

   ##Use input from another Iris species.
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[5.1,3.5,1.4,.2]})
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))
   ```

## <a name="managing-the-services"></a>Verwalten der Dienste

Nun, dass Sie einen Webdienst erstellt haben, können Sie aktualisieren, löschen oder erneut veröffentlichen, diesen Dienst. Sie können auch alle Webdienste auflisten, die mithilfe von R Server (oder Machine Learning-Server) gehostet werden.

### <a name="update-a-web-service"></a>Aktualisieren Sie einen Webdienst

 In diesem Beispiel aktualisieren wir den Dienst, um eine Beschreibung, die hilfreich für Personen hinzuzufügen, die diesen Dienst nutzen können.

```python
#Define what needs to be updated. Here we add a description.
#Be sure to specify the runtime_type again.
update_request = deployrclient.models.PublishWebServiceRequest(
    description = "Determines iris species using length and width of sepal and petal", runtime_type = "Python")
#Now update it by specifying the service name and version number
client.patch_web_service_version("Iris", "V1.0", update_request, headers)
```

Sie können einen Webdienst zum Ändern des Codes, Modell, Beschreibung, Eingaben, Ausgaben und mehr aktualisieren.

### <a name="publish-another-version"></a>Veröffentlichen Sie eine andere version

In diesem Beispiel gibt der Dienst jetzt Iris Arten als Zeichenfolge statt als eine Liste von Zeichenfolgen zurück.

```python
#Publish another version of the web service, but this time 
#the service returns the species as a string instead of list of strings.
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "string")
 
#Define the publish request for the service and its arguments.
#Specify the changed code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
    code = "iris_species = [names[x] for x in clf.predict(flower_data)][0]",
    description = "Determines the species of iris, based on Sepal Length, Sepal Width, Petal Length and Petal Width",
    input_parameter_definitions = [flower_data],
    output_parameter_definitions = [iris_species],
    runtime_type = "Python",
    snapshot_id = response.snapshot_id)
 
#Now, publish the service with version (V2.0)
client.publish_web_service_version("Iris", "V2.0", publish_request, headers)
 
#Make request to consume service using these flower_data inputs; print output
resp = s.post(url+"/api/Iris/V2.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))
```

Dieses Muster können Sie mehrere Versionen der gleichen Webdienst veröffentlichen. 

### <a name="list-services"></a>Dienste auflisten

In diesem Beispiel ruft eine Liste aller Web-Dienste, einschließlich der von anderen Benutzern oder in verschiedenen Sprachen erstellt.

```python
#Return the list of all existing web services.
for service in client.get_all_web_services(headers):
    #print the service information
    print(service)
    #Print each input and output parameter
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))
``` 

### <a name="delete-services"></a>Löschen von Diensten

In diesem Beispiel löschen wir die zweite Web Service-Version, die wir gerade veröffentlichten.

```python
#Delete the second version we just published.
client.delete_web_service_version("Iris","V2.0",headers)
```

Sie können jeden beliebigen Dienst löschen, den Sie erstellt haben. Sie können die Dienste von anderen löschen, nur dann, wenn Sie eine Rolle zugewiesen sind, die die entsprechenden Berechtigungen verfügt.