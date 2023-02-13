# qgis-plugin-doc

# QGIS plugin doc

This project is the QGIS plugin documentation in Unique App.

## Project Structure

Here a description of the file and folder structure of the project:

```shell
|-- version
|-- src
|   |-- images
|   |   |-- ...
|   |-- docs
|       |-- en-US
|           |-- QGIS plugin.md
|
|-- SwaggerAPI.json
```
            
- the `version` File contains the Geosys version of the documentation. It should be updated for each modification.
- The `src` contains all files and folders that will be deploy.
- The folder `images` contains all medias and ressources used in markdown files.
- The folder `docs` contains all written documentation organised by **culture**.
- The SwaggerAPI.json relates to the OpenAPI definition of Swagger's project, it will be converted automatically to markdown file.

*NB: you might notice the absence of folders `src/docs/{Culture}`. The reason might be this projet has only Swagger Open API definition and no written documents.*

## TOC File
The TOC file (Table Of Content) is defined by many properties for the side nav bar in the Unique App. Its content should look like this :

```json
[
  {
    "name": "Home page",
    "position": 1,
    "code": "HomePage",
    "icon": "home"
  },
  {
    "name": "Default",
    "position": 0,
    "code": "Default",
    "icon": "info"
  }
]
```

`name` will be the text displayed in the side nav bar<br><br>
`position` correspond to the link hierarchy into the component. Starting from 0.<br><br>
`code` is a norm value to help the system, developed angular component, to manage properly the functionnalities. The value should respect the [Pascal case convention](https://en.wiktionary.org/wiki/Pascal_case)<br><br>
`icon` is the icon that is displayed in the side nav bar. Icons material can be found [here](https://fonts.google.com/icons?selected=Material+Icons&icon.style=Filled&icon.set=Material+Icons)<br><br>

If the ToC object is not defined then it will not be displayed in the side bar nav.

There is a unique ToC file for the side nav bar, you can edit it [here](https://github.com/GEOSYS/Home_page_App/blob/main/src/TOC.en-US.json)

## Written documentation

All written documentation should be hosted in the folder `src/docs/` and in the appropriate localization culture. The default value is **en-US**, and its value must be always culture specific (for example, for French you name the folder *fr-FR*).

## Documentation deployment process

Each commit will trigger a deployment process definied in TeamCity and Octopus. It will automatically deployed the files in the **Validation** environment.
There is no automatic process to deploy directly in Production to ensure the documentation quality, making sure in tested environment everything is in order. So to continue the deployment process you must trigger manually the deployment in Octopus (this is just One click per environment).

if a new Swagger API definition file is added, please contact a developer to help you for the integration. The deployment will be modified accordingly.

## Swagger API definition

All swagger API definition files should be hosted in the root `/` folder of the project (where the README.md and version files are). 

:warning: If you need to rename the swagger file please contact a developer in order to update the deployment pipeline with the new name.

## How to edit a markdown

You can modify markdown files through Github or Visual Studio Code (with Markdown All in One puglin).<br>
You can seek syntax element into this [cheat sheet](https://www.markdownguide.org/cheat-sheet/)

## Where do I put my media ressources ?

You must stock your images or other medias into the images folder located at `src/images/` and then refer it in you markdown file with a relative path e.g. /images/my_image.png

## Styling your document

The process use a tool that convert markdown syntax to HTML syntax and the unique app applies a general style and format to it. So be simple and consitant in writing documents!

Example:

`## My title` will become `<h2>My title</h2>` in HTML and will have the h2 styling defined in Unique App.

## How do I sort my documents ?

Inside the folder, files are sorted alphabetically. If you want to sort files in a particular order you need to respect this nomenclature :

- 01.My main document.md
- 02.My second document.md

The `0` before the unit is **very important** because as indicated above, files are sorted alphabetically therefor the following suite numbers `1,9,10,21,22` would be sorted in this order `1,10,21,22,9`. So in order to fix it you should previous a `0` for the unit.
