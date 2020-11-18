# User Manual

## Run Sirene CLI

Windows

    ./sirene_cli-win.exe [OPTIONS]

Linux

    sirene_cli-linux [OPTIONS]

MacOS

    sirene_cli-macos [OPTIONS]

**Note:** Pour linux et macos, s'assurer que le binaire est exécutable. Sinon utiliser la commande `chmod 755 sirene_cli-X`, avec X qui vaut linux ou macos en fonction de votre environnement

```sh
$ sirene_cli-macos -h
SIRENE CLI Version 1.0.0
Usage: sirene-cli [options]

Extraction de la base SIRENE

Options:
-V, --version output the version number
-c,--config [config_file] Configuration file (default: "config.json")
-s,--sample Display sample config.json
-h, --help display help for command
```

## Configuration file

Le fichier de configuration est constitué des propriétés suivantes:

- since:
  - chaîne de caractères représentant la date au format "`DD/MM/YYY`"
  - si aucune condition n'est défini, elle est utilisé dans la condition par défaut
  - valeur par défaut: 1 mois
- code_ape:
  - un tableau de codes APE
  - valeur par defaut: "tous"
- destination:
  - le répertoire de destination
  - valeur par défaut: `./sirene_data_YYYYMMDD_HHmm`
- output_filename:
  - le nom du fichier de sortie
  - valeur par défaut: `./sirene_data_YYYYMMDD_HHmm.csv`
- conditions:
  - une liste de conditions telles que supportées par l'[API d'OpenDataSoft](https://help.opendatasoft.com/apis/ods-search-v1/#query-language-and-geo-filtering) et la partie [Record Search API](https://help.opendatasoft.com/apis/ods-search-v1/#record-search-api)
  - valeur par défaut: `datecreationetablissement<SINCE`
- refines:
  - une liste de rafinements tels que supportés par l'[API d'OpenDataSoft](https://help.opendatasoft.com/apis/ods-search-v1/#query-language-and-geo-filtering) et la partie [Record Search API](https://help.opendatasoft.com/apis/ods-search-v1/#record-search-api)
  - aucune valeur par défaut

### Exemple

```json
{
  "since": "01/11/2020",
  "codes_ape": ["14.13Z", "70.22Z"],
  "destination": "./test",
  "output_filename": "actifs.csv",
  "conditions": ["datecreationetablissement > #SINCE#"],
  "refines": ["etatadministratifetablissement=Actif"]
}
```

Le fichier de configuration va extraire de la base SIRENE tous les éléments dont la date de création de l'établissement est supérieur au `01/11/2020` parmi les codes APE `14.13Z`, `70.22Z` et étant `Actif`.

Le résultat est stocké dans le fichier `./test/actifs.csv`.
