---
title: "Hinzufügen eines Modells zu einer ASP.NET MVC Core-App"
author: rick-anderson
description: "Hinzufügen eines Modells zu einer einfachen ASP.NET Core-App"
keywords: "ASP.NET Core, MVC, Gerüst, Gerüstbau"
ms.author: riande
manager: wpickett
ms.date: 03/30/2017
ms.topic: get-started-article
ms.assetid: 8dc28498-eeee-1638-b903-b593059e9f39
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app-mac/adding-model
ms.openlocfilehash: 4a158802a19011cbb45da1b3ca43d67706efe4cd
ms.sourcegitcommit: d9e2c99c837078fcac0e315025f8fbfbd45ea6e8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
[!INCLUDE[adding-model](../../includes/mvc-intro/adding-model1.md)]

* Klicken Sie mit der rechten Maustaste auf den Ordner *Modelle*, und wählen Sie **Hinzufügen** > **Neue Datei** aus. 
* Führen Sie im Dialogfeld **Neue Datei** folgende Aktionen aus:

  * Wählen sie im linken Bereich **Allgemein** aus.
  * Wählen Sie im mittleren Bereich **Leere Klasse** aus.
  * Geben Sie der Klasse den Namen **Film**, und wählen sie **Neu** aus.

Fügen Sie der Klasse `Movie` die folgenden Eigenschaften hinzu:

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieNoEF.cs?name=snippet_1)]

Die Datenbank benötigt das Feld `ID` für den primären Schlüssel.

Erstellen Sie das Projekt, um sicherzustellen, dass keine Fehler vorliegen. Sie verfügen jetzt über ein **Modell** in Ihrer **MVC**-App.

## <a name="prepare-the-project-for-scaffolding"></a>Vorbereiten des Projekts für den Gerüstbau

- Klicken Sie mit der rechten Maustaste auf die Projektdatei, und wählen Sie dann **Extras > Datei bearbeiten** aus.

  ![Screenshot für oben genannten Schritt](adding-model/_static/1.png)

- Fügen Sie die folgenden, hervorgehobenen NuGet-Pakete in die Datei *MvcMovie.csproj* ein:
             
  [!code-csharp[Main](../first-mvc-app-xplat/start-mvc/sample/MvcMovie/MvcMovie.csproj?highlight=7,10)]

- Speichern Sie die Datei.

- Erstellen sie eine *Models/MvcMovieContext.cs*-Datei, und fügen Sie die folgende `MvcMovieContext`-Klasse hinzu: [!code-csharp[Main](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Models/MvcMovieContext.cs)]
   
- Öffnen Sie die Datei *Startup.cs*, und fügen Sie zwei Usings hinzu: [!code-csharp[Main](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet1&highlight=1,2)]

- Fügen Sie den Datenbankkontext zur Datei *Startup.cs* hinzu:

   [!code-csharp[Main](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet2&highlight=6-7)]

  Damit weiß Entity Framework, welche Modellklassen im Datenmodell enthalten sind. Sie definieren eine *Entitätenmenge* von Filmobjekten, die in der Datenbank als Tabelle namens „Film“ dargestellt wird.

- Erstellen Sie das Projekt, um sicherzustellen, dass keine Fehler vorliegen.

## <a name="scaffold-the-moviecontroller"></a>Erstellen des Gerüsts für MovieController

Öffnen Sie im Projektordner ein Terminalfenster, und führen Sie die folgenden Befehle aus:

```
dotnet restore
dotnet aspnet-codegenerator controller -name MoviesController -m Movie -dc MvcMovieContext --relativeFolderPath Controllers --useDefaultLayout --referenceScriptLibraries 
```
Wenn Sie die Fehlermeldung `No executable found matching command "dotnet-aspnet-codegenerator", verify` erhalten, trifft Folgendes zu:

 * Sie befinden sich im Projektverzeichnis. Hier befinden sich die Dateien *Program.cs*, *Startup.cs* und *.csproj*.
 * Sie verwenden die dotnet-Version 1.1 oder höher. Führen Sie `dotnet` aus, um Informationen über die Version zu erhalten.
 * Sie haben der Datei [MvcMovie.csproj](#prepare-the-project-for-scaffolding) das Element `<DotNetCliToolReference>` hinzugefügt.
 
<!--
> [!NOTE]
> If you get an error when the scaffolding command runs, see [issue 444 in the scaffolding repository](https://github.com/aspnet/scaffolding/issues/444) for a workaround.
-->

Das Gerüstbaumodul erstellt Folgendes:

* Einen Filmcontroller (*Controllers/MoviesController.cs*)
* Razor-Ansichtsdateien für Seiten der Typen „Erstellen“, „Löschen“, „Details“ und „Index“ (*Views/Movies/\*.cshtml*)

Die automatische Erstellung von [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)-Aktionsmethoden und Ansichten (create, read update and delete – Erstellen, Lesen, Aktualisieren und Löschen) wird als *Gerüstbau* bezeichnet. Bald verfügen Sie über eine voll funktionsfähige Webanwendung, mit der Sie eine Filmdatenbank verwalten können.

### <a name="add-the-files-to-visual-studio"></a>Hinzufügen der Dateien zu Visual Studio

* Fügen Sie dem Visual Studio-Projekt die Datei *MovieController.cs* hinzu:

  * Klicken Sie mit der rechten Maustaste auf den Ordner *Controller*, und wählen Sie **Hinzufügen > Dateien hinzufügen** aus.
  * Wählen Sie die Datei *MovieController.cs* aus.

* Fügen Sie den Ordner *Filme* und die Ansichten hinzu:

  * Klicken Sie mit der rechten Maustaste auf den Ordner *Ansichten*, und wählen Sie **Hinzufügen > Vorhandenen Ordner hinzufügen** aus.
  * Navigieren Sie zum Ordner *Ansichten*, und wählen Sie *Ansichten\Filme* und anschließend **Öffnen** aus.
  * Wählen Sie im Dialogfeld **Select files to add from Movies** (Aus „Filme“ hinzuzufügende Dateien auswählen) **Alle einschließen** aus, und klicken Sie dann auf **OK**.

[!INCLUDE[adding-model 2x](../../includes/mvc-intro/adding-model2xp.md)]

[!INCLUDE[adding-model](../../includes/mvc-intro/adding-model3.md)]

Sie verfügen jetzt über eine Datenbank und Seiten zum Anzeigen, Bearbeiten, Aktualisieren und Löschen von Daten. Im nächsten Tutorial werden wir mit dieser Datenbank arbeiten.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Tag Helpers (Tag-Hilfsprogramme)](xref:mvc/views/tag-helpers/intro)
* [Globalization and localization (Globalisierung und Lokalisierung)](xref:fundamentals/localization)

>[!div class="step-by-step"]
[Vorheriges Tutorial: Adding a View (Hinzufügen einer Ansicht)](adding-view.md)
[Nächstes Tutorial: Working with SQL (Arbeiten mit SQL)](working-with-sql.md)  
