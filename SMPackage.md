SMPackage is a proposed package schema system, likely for StepMania 5.2.

# StepMania package schema

A *package* is a ZIP file containing a component used in a StepMania installation, such as a song, noteskin, theme, courses, a package of songs, etc. A package may consist of a single component, multiple instances of a single component, or a collection of different types of component. 

When a package is added to a StepMania installation, its contents are extracted into cache the next time StepMania is launched. If the package is removed from the directory, the relevant items are removed from the cache. Packages are primarily managed manually, but can be listed on a page in StepMania's options menu (ScreenManagePackages) - where users can view information about what the package provides, and disable or enable them individually. Packages can also supersede or "patch" files contained in another package, or have dependencies on another.

Each type of content in a package (i.e. songs, themes, noteskin, etc) is contained within a folder that corrosponds to its content type (similarly to SMZip files). Hence, songs would be stored in the Songs/Name of Mix/ folder.

Packages contain manifest files that describe their contents, written in JSON. Packages are named in notation inspired by reverse domain name/Java notation, typically beginning with "sm". Using _In the Groove 2_ as an example, the package name would be "sm.roxor.itg2".

## Fields

#### name
The internal name of the package.

#### displayName
The friendly display name of the package.

#### description
A description of the package's contents.

#### author
The name of the author or group who created the package's content.

#### url
The website or a web page associated with the package

#### version
The version number of the package

#### date
The date on which this specific version of the package was released, in MM/DD/YY format.

#### provides
The types of components that the package provides. They can include, for instance, "song" (an individual song folder), "songs" (a folder containing a group of songs), "noteskin", "theme", "course", etc. If the package contains multiple components, they are listed in a comma-seperated list.

### dependencies
#### smVer
If the content requires a specific StepMania version.

#### dependsOn
If the package requires content from other packages, their names are listed here.

#### updates
If the package patches content from another package, specify its name, and the version number of the previous version. When packages are unpacked, the original package will be extracted first, and the content from the superseding packages will overwrite it.

#### supersede
This works similarly to the updates parameter, except that this specifies that if older versions of a specific package exist, this supersedes and replaces the entire package and does not patch it.

## Examples
```
{
    "smpackage": {
        "name": "sm.author.examplemix",
        "displayName": "ExampleMix",
        "author": "John Doe",
        "provides": "songs"
        "version": "1.0",
    }
}
 
{
    "smpackage": {
        "name": "sm.author.examplemix.update1",
        "displayName": "ExampleMix Update 1",
        "author": "John Doe",
        "provides": "songs",
        "description": "This update for ExampleMix fixes timing issues and adds 5 additional songs.",
        "version": "1.0.1",
        "dependencies": {
            "smVer": 5.0.x,
            "updates": {
                "package": "sm.author.examplemix",
                "version": "1.0"
            },
        }
    }
}
  
{
    "smpackage": {
        "name": "sm.purplesmart.cantermix",
        "displayName": "CanterMix",
        "author": "Purple Smart",
        "url": "http://cantermix.example.com",
        "description": "A StepMania pack inspired by the series 'HORSE: The Animation'.",
        "provides": [
            "songs",
            "theme",
            "announcer",
            "noteskin",
            "courses"
        ]
    }
}
```  
## License
No copyright exists in this schema, using the CC Zero dedication.
http://creativecommons.org/publicdomain/zero/1.0/