---
title: Mithilfe von Bower in ASP.NET Core
author: rick-anderson
description: Verwalten von Client-Side-Paketen mit Bower.
keywords: ASP.NET Core, bower
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.assetid: df7c43da-280e-4df6-86cb-eecec8f12bfc
ms.technology: aspnet
ms.prod: asp.net-core
uid: client-side/bower
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d208072f55d78de6ec8c238ebbe723cc0ec598
ms.sourcegitcommit: 9cdbfd0d670d70b9c354216aabee260c52dad5ee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/12/2017
---
# <a name="manage-client-side-packages-with-bower-in-aspnet-core"></a>Verwalten von Client-Side-Paketen mit Bower in ASP.NET Core

Durch [Rick Anderson](https://twitter.com/RickAndMSFT), [Noel Reis](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/), und [Scott Addie](https://scottaddie.com) 

[Bower](https://bower.io/) ruft sich selbst "Eine Paketmanager für das Web." Innerhalb der Umgebung .NET füllt die "void", um NuGet Funktion zum Übermitteln von Dateien mit statischer Inhalt nach links. Für ASP.NET Core, sind dies statischen Dateien clientseitige Bibliotheken wie inhärenten [jQuery](http://jquery.com/) und [Bootstrap](http://getbootstrap.com/). Für die .NET-Bibliotheken, verwenden Sie immer noch [NuGet](https://www.nuget.org/) Paket-Manager.

Prozess zur Erstellung neuer Projekte, die mit den richten Sie die clientseitige ASP.NET Core-Projektvorlagen erstellt. [jQuery](http://jquery.com/) und [Bootstrap](http://getbootstrap.com/) installiert sind, und Bower wird unterstützt.

Die clientseitige Pakete werden aufgeführt, der *"bower.JSON"* Datei. Konfiguriert die Projektvorlagen für ASP.NET Core *"bower.JSON"* mit jQuery, jQuery-Validierung und Bootstrap.

In diesem Lernprogramm fügen wir Unterstützung für [Schriftart Awesome](http://fontawesome.io). Bower Pakete können installiert werden, wobei die **Bower-Pakete verwalten** UI oder manuell in die *"bower.JSON"* Datei.

### <a name="installation-via-manage-bower-packages-ui"></a>Installation über Bower-Pakete verwalten UI

* Erstellen Sie eine neue ASP.NET Core Web-app mit der **ASP.NET-Webanwendung für Core (.NET Core)** Vorlage. Wählen Sie **-Webanwendung** und **keine Authentifizierung**.

* Mit der rechten Maustaste des Projekts im Projektmappen-Explorer, und wählen Sie **Bower-Pakete verwalten** (Alternativ im Hauptmenü **Projekt** > **Bower-Pakete verwalten**).

* In der **Bower: \<Projektname\> ** , klicken Sie auf der Registerkarte "Durchsuchen", und klicken Sie dann die Pakete durch Eingabe Filterliste `font-awesome` in das Suchfeld:

 ![Bower-Pakete verwalten](bower/_static/manage-bower-packages.png)

* Überprüfen Sie, ob die "Speichern Sie die Änderungen *" bower.JSON "*" aktiviert ist. Wählen Sie eine Version aus der Dropdown-Liste, und klicken Sie auf die **installieren** Schaltfläche. Die **Ausgabe** Fenster zeigt die Details zur Installation.

### <a name="manual-installation-in-bowerjson"></a>Manuelle Installation in "bower.JSON"

Öffnen der *"bower.JSON"* Datei und die Abhängigkeiten hinzuzufügen "Schriftart awesome". IntelliSense zeigt die verfügbaren Pakete. Wenn ein Paket ausgewählt ist, werden die verfügbaren Versionen angezeigt. Die folgenden Bilder sind ältere und stimmen nicht überein, was Sie sehen.

![IntelliSense von Bower Paket-explorer](bower/_static/add-package.png)

![Bower Version IntelliSense](bower/_static/version-intelliSense.png)

Bower verwendet [semantischer versionsverwaltung](http://semver.org/) , Abhängigkeiten zu organisieren. Semantische versionsverwaltung, auch bekannt als SemVer, identifiziert die Pakete mit den Nummerierungsschema \<wichtigen >.\< kleinere >. \<Patch >. IntelliSense vereinfacht semantischen versionsverwaltung, indem nur einige allgemeine Optionen angezeigt. Das oberste Element in der IntelliSense-Liste (4.6.3 im obigen Beispiel) wird die neueste stabile Version des Pakets betrachtet. Das Caretzeichen (^) Symbol entspricht der aktuellsten Hauptversion und die Tilde (~) entspricht der aktuellsten Nebenversion.

Speichern Sie die *"bower.JSON"* Datei. Visual Studio wird überwacht, ob die *"bower.JSON"* -Datei für die Änderungen. Beim Speichern der *Bower Installation* Befehl ausgeführt wird. Finden Sie im Ausgabefenster **Bower/Npm** Ansicht für den exakten Befehl ausgeführt.

Öffnen der *".bowerrc"* Datei unter *"bower.JSON"*. Die `directory` -Eigenschaftensatz auf *"Wwwroot" / Lib* gibt den Speicherort Bower an die Medienobjekte Paket installiert.

```json
{
 "directory": "wwwroot/lib"
}
```

Sie können das Suchfeld im Projektmappen-Explorer verwenden, suchen und Anzeigen der Schriftart awesome Paket.

Öffnen der *Views\Shared\_Layout.cshtml* Datei, und fügen Sie die Schriftart awesome CSS-Datei mit der Umgebung [Tag Helper](xref:mvc/views/tag-helpers/intro) für `Development`. Klicken Sie im Projektmappen-Explorer ziehen, und legen Sie *Schriftart awesome.css* innerhalb der `<environment names="Development">` Element.

[!code-html[Main](bower/sample/_Layout.cshtml?highlight=4&range=9-13)]

Fügen Sie in einer Produktions-app *Schriftart awesome.min.css* für die Umgebung Tags Hilfe für `Staging,Production`.

Ersetzen Sie den Inhalt von der *Views\Home\About.cshtml* Razor-Datei durch Folgendes Markup:

[!code-html[Main](bower/sample/About.cshtml)]

Führen Sie die app, und navigieren Sie zu der Info-Ansicht, um zu überprüfen, ob die Schriftart awesome Paket funktioniert.

## <a name="exploring-the-client-side-build-process"></a>Untersuchen des clientseitigen Build-Prozesses

Die meisten ASP.NET Core-Projektvorlagen sind bereits mithilfe von Bower konfiguriert. Diese weiter Exemplarische Vorgehensweise beginnt mit einem leeren ASP.NET Core-Projekt und Transformationsprozesses manuell hinzugefügt, sodass Sie einen Eindruck darüber abrufen können, wie Bower in einem Projekt verwendet wird. Sie sehen können, was geschieht, um die Projektstruktur und erfolgt die Ausgabe als jeder konfigurationsänderung Common Language Runtime.

Die allgemeinen Schritte des Buildprozesses für die clientseitige mit Bower verwendet werden:

* Definieren Sie die Pakete im Projekt verwendet. <!-- once defined, you don't need to download them, VS does -->
* Referenzpaketen von Webseiten.

### <a name="define-packages"></a>Definieren von Paketen

Nachdem Sie Pakete in Auflisten der *"bower.JSON"* Visual Studio-Datei laden sie herunter. Im folgenden Beispiel wird Bower jQuery und Bootstrap zum Laden der *"Wwwroot"* Ordner.

* Erstellen Sie eine neue ASP.NET Core Web-app mit der **ASP.NET-Webanwendung für Core (.NET Core)** Vorlage. Wählen Sie die **leere** -Projektvorlage, und klicken Sie auf **OK**.

* Im Projektmappen-Explorer mit der Maustaste des Projekts > **neues Element hinzufügen** , und wählen Sie **Bower Konfigurationsdatei**. Hinweis: Ein *".bowerrc"* Datei wird ebenfalls hinzugefügt.

* Open *"bower.JSON"*, Jquery und fügen auf das Bootstrapping der `dependencies` Abschnitt. Das resultierende *"bower.JSON"* Datei wird im folgenden Beispiel aussehen. Die Versionen mit der Zeit ändert und die folgenden Abbildung möglicherweise nicht überein.

[!code-json[Main](bower/sample/bower.json?highlight=5,6)]

* Speichern Sie die *"bower.JSON"* Datei.

 Überprüfen Sie das Projekt enthält die *bootstrap* und *jQuery* Verzeichnisse in *"Wwwroot" / Lib*. Bower verwendet die *".bowerrc"* -Datei zum Installieren von der Objekten in *"Wwwroot" / Lib*.

 Hinweis: Die Benutzeroberfläche "Bower-Pakete verwalten" bietet eine Alternative zum manuellen bearbeiten.

### <a name="enable-static-files"></a>Statische Dateien aktivieren

* Hinzufügen der `Microsoft.AspNetCore.StaticFiles` NuGet-Paket zum Projekt.
* Aktivieren Sie die statische Dateien mit versorgt werden die [Middleware für statische Dateien](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.staticfileextensions). Fügen Sie einen Aufruf von [UseStaticFiles](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.staticfileextensions) auf die `Configure` Methode `Startup`.

[!code-csharp[Main](bower/sample/Startup.cs?highlight=9)]

### <a name="reference-packages"></a>Referenzpaketen

In diesem Abschnitt erstellen Sie eine HTML-Seite, um sicherzustellen, dass er die bereitgestellten Pakete zugreifen kann.

* Fügen Sie eine neue HTML-Seite mit dem Namen *"Index.HTML"* auf die *"Wwwroot"* Ordner. Hinweis: Sie müssen die HTML-Datei zum Hinzufügen der *"Wwwroot"* Ordner. Standardmäßig kann nicht außerhalb statische Inhalte bereitgestellt werden *"Wwwroot"*. Finden Sie unter [arbeiten mit statischen Dateien](xref:fundamentals/static-files) für Weitere Informationen.

 Ersetzen Sie den Inhalt des *"Index.HTML"* durch Folgendes Markup:

[!code-html[Main](bower/sample/Index.html)]

* Führen Sie die app, und navigieren Sie zu `http://localhost:<port>/Index.html`. Alternativ können Sie mit *"Index.HTML"* geöffnet haben, drücken Sie `Ctrl+Shift+W`. Stellen Sie sicher, dass die Formatvorlage Jumbotron angewendet wird, die jQuery-Code reagiert werden soll, wenn die Schaltfläche geklickt wird, und die Schaltfläche "Bootstrap" Zustand ändert.

 ![Jumbotron-Formatvorlage](bower/_static/jumbotron.png)
