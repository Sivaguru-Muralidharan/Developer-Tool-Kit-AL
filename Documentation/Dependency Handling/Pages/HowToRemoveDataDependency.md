# How to Remove Data Dependency
## Introduction
> Quick Recap:\
> Data Dependency Occurs when a Table is Declared in a different Extension or when a Field has been declared in a Table Extension in a different Extension.

Normally in to get Data from a Different Extension, the Dependency Section of the `app.json` of the current working Extension would be modified to include the Source Extension's App Details. If the Dependency is installed and active on the Database, the Symbols would be downloaded for us to use.

`app.json` of Extension `B`
```
{
  "id": "1a07850e-f0cc-4b6a-b411-8080859bfae9",
  "name": "B",
  "publisher": "Default Publisher",
  "version": "1.0.0.0",
  "brief": "",
  "description": "",
  "privacyStatement": "",
  "EULA": "",
  "help": "",
  "url": "",
  "logo": "",
  "dependencies": [
    {
        "id": "f93cadb0-e4eb-469c-bec2-414ba941239f",
        "name": "A",
        "publisher": "Default Publisher",
        "version": "1.0.0.0",
    }
    ],
  "screenshots": [],
  "platform": "23.0.0.0",
  "application": "23.0.0.0",
  "idRanges": [
    {
      "from": 50100,
      "to": 50250
    }
  ],
  "resourceExposurePolicy": {
    "allowDebugging": true,
    "allowDownloadingSource": true,
    "includeSourceInSymbolFile": true
  },
  "runtime": "12.0",
  "features": [
    "NoImplicitWith"
  ]
}
```

If this Dependency is established, then uninstalling Extension `A` would automatically Uninstall Extension `B`

## How To access Data without Dependency?
There are 2 Ways this is Possible, 
1. Use the [RecordRef and FieldRef](./HandleDataDependencyWithRecRef.md) Datatypes available in Business Central.
2. Use [APIs](./HandleDataDependencyWithAPI) Internally to consume Data.

## Disclaimer
⚠️Each method has its own advantages and disadvantages. Please Analyse the Requirement and fully understand the Disadvantages of the Above mentioned methods before deciding to use them.