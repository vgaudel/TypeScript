# TYPESCRIPT

## Introduction : Pourquoi TypeScript ?
### Objectifs

- Déconstruire les idées reçues
- Comprendre la valeur ajoutée par rapport à JavaScript

![alt text](imgs/JavascriptVersions.png)

### Contenu

- JavaScript : liberté ↔ bugs silencieux
- TypeScript = JavaScript + types
- Compilation : `.ts → .js`
- Erreurs détectées avant l’exécution
- Cas concrets :

    - `undefined is not a function`
    - erreurs d’API
    - refactoring dangereux


### Caractéristiques 

- langage de programmation libre et open-source 
- améliore la programmation JavaScript en apportant plus de rigueur (typage fort optionnel) et une approche orientée objet
- sur-ensemble de JavaScript (i.e. tout code JavaScript correct peut être utilisé avec TypeScript)
- utilisation est obligatoire au niveau du framework **Angular**
- facultatif avec d'autres frameworks JavaScript très connus (React, Node.js / Express, ...)

### Comportement

- Tant que l'on n'ajoute pas de spécificités TypeScript, le fichier `.js` généré est identique au fichier `.ts`
- Si, par contre, on ajoute des précisions sur les types de données au sein du fichier `.ts` alors :
    - Le fichier `.js` est bien généré (par simplification ou développement) si aucune erreur bloquante n'est détectée
    - Des messages d'erreurs sont émis par **tsc** si des valeurs sont incompatibles avec les types des paramètres des fonctions appelées ou des affectations de variables programmées


### Démo

```TypeScript
function add(a, b) {
  return a + b
}

add(2, "3")
```

Puis version TypeScript :

```TypeScript
function add(a: number, b: number): number {
  return a + b
}

add(2, "3")
```

Message clé : TypeScript ne remplace pas JavaScript, il le sécurise.

## TypeScript dans un vrai projet

### Objectifs

- Savoir l'utiliser concrètement après le cours

### Installation de TypeScript via npm

De façon à télécharger et lancer le compilateur **tsc**, on pourra (entre autres possibilités) s'appuyer sur Node.js/npm (à préalablement télécharger/installer si nécessaire -> en suivant ce [lien](https://nodejs.org/en/download/))

### Contenu

- Initialiser le projet 

```Bash
npm init
npm install typescript
tsc --init
```

- Configurer le projet en modifiant le fichier `tsconfig.json`
- REM: il est recommandé de créer deux dossiers `src` et `dist` pour séparer les fichier `.ts` et `.js` de manière propre

## Les types fondamentaux

### Objectifs

- Savoir typer les variables simples
- Comprendre l’inférence

|Types      |	Exemple(s) ou signification(s)                                                      |
|:----------|:------------------------------------------------------------------------------------|
|:boolean   |	let isDone :boolean = false;                                                        |
|:number    |	let height :number = 6; ou let size :number = 1.83;                                 |
|:string    |	let name :string = "bob"; ou name = 'smith';                                        |
|:Array     |	let list1 :number[] = [1, 2, 3]; ou let list2 :Array<number> = [1, 2, 3];           |
| enum      |	Énumération                                                                       |
|:any       |	let notSure :any = 4; ou notSure = "maybe a string instead"; ou notSure = false;    |
|:void      |	function warnUser() :void { alert("This is my warning message"); }                  |
|:object    |	Objet quelconque : plus précis que any, moins précis qu'un nom de classe            |
            
### Contenu

- Types primitifs :

    - number, string, boolean
    - null, undefined

- Enumeration :
```TypeScript
enum Color {Red, Green, Blue}; // start at 0 by default 
// enum Color {Red = 1, Green, Blue}; 
let c: Color = Color.Green;  //display as "1" by default 
let colorName: string = Color[1]; 
// "Green" if "Red" is at [0]
// Color["Green"] return 1​
```

- Objet :
```TypeScript
let obj : object = { id : 2  , label : "cahier" } ; 
obj = { prenom : "jean" , nom : "Bon" } ; 
//structure objet différente acceptée​
```

- Cohérence ou d'incohérence de type : :
```TypeScript
function greet(person : string): string {
    return "Hello, " + person;
}
let userName = "Power User";
//i=0; //manque var (erreur détectée par tsc)

let msg = "";
//msg = greeterString(123456); 
//123456 incompatible avec type string (erreur détectée par tsc)

msg = greet(userName);
console.log(msg);​
```

- Tableau :
```TypeScript
let var tableau :string[] = new Array<string>();
tableau.push("abc");​
```
```TypeScript
let jours : string[];
jours = [ "lundi" , "mardi" , "mercredi" , "jeudi" , "vendredi" ];
jours.push("samedi"); jours.push("dimanche");
for(const [i,jour] of jours.entries()){
    let j=jour.toUpperCase();
    console.log( `jour ${i} : ${j}`);
}
```


- `any` vs `unknown` (important)
- Inférence automatique :
```TypeScript
let age = 30 // TypeScript comprend : number
```

## Exercices pratiques
### Exercice

Convertir ce code JS en TypeScript :
```TypeScript
function formatUser(user) {
  return user.name.toUpperCase()
}
```

### Objectifs :

- typer les paramètres
- typer le retour
- détecter les erreurs potentielles

Correction collective commentée.

## Fonctions & typage avancé

### Objectifs

- Typage précis des fonctions
- Comprendre les unions et options

### Contenu

- Typage de fonctions :
```TypeScript
function greet(name: string): void {}
```

- Paramètres optionnels :
```TypeScript
function log(message: string, level?: string) {}
```

- Types union :
```TypeScript
// Deux types supportés
let id: number | string
// Précision sur des valeurs possibles de variables 
dialect : "mssql" | "mysql" | "postgres" | "sqlite" | "mariadb";​
```

- Valeurs par défaut + types :

```TypeScript
unite : string | undefined; // string ou bien undefined​

function greet(name: string = "Invité", age: number = 30): string {
  return `Bonjour ${name}, vous avez ${age} ans.`;
}
```
### Cas réel

API qui peut renvoyer plusieurs formats -> union types




# Programmation Orientée Objet

Les principaux objectifs de cette partie sont de découvrir :

- Le potentiel de TypeScript sur l'aspect "orienté objet"
- Les classes, instances, constructeurs, ...


Le langage ES2015 apporte (vis-à-vis de ES5) de nouveaux mots-clefs (class, constructor, extends, ...) pour obtenir un code orienté objet plus lisible et mieux structuré.

Le langage TypeScript (en tant que sur-ensemble de ES2015) ajoute à son tour de nouveaux mots-clefs (abstract, public / private, interface, ...) pour obtenir un meilleur code orienté objet.

- Syntaxes orientées objet supportées à-peu-près de la même façon entre TypeScript et ES2015 :
  + Mots-clefs `class` et `constructor`
  + `static`
  + Mots-clefs `get` et `set`
  + Héritage (`extends`, `super`, ...)
  + `Object.assign(...)`

 Syntaxes orientées objet parfaitement supportées que par **TypeScript** :
  + Mot-clef `abstract` (classes abstraites)
  + `interface`, `implements`, ...
  + `public`, `private`, `protected`, ...
  + `public`, `private` ou `protected` au niveau des paramètres d'un constructeur pour définir automatiquement certaines variables d'instances (attributs)

## Objets, interfaces & classes

### Classes

```TypeScript
class Compte{
    numero : number;
    label : string;
    solde : number;

    debiter(montant : number) : void {
        this.solde -= montant; // this.solde = this.solde - montant;
    }

    crediter(montant : number) : void {
        this.solde += montant; // this.solde = this.solde + montant;
    }
}​
```
Sans initialisation explicite (via constructeur ou autre), les propriétés internes d'un objet sont par défaut à la valeur `undefined`. Lorsque `tsconfig.json` comporte la ligne d'option `"strict": true,`, ceci ne fonctionne qu'avec l'option complémentaire `"strictPropertyInitialization": false`.

```TypeScript
var c1 = new Compte(); //instance (exemplaire) 1
console.log("numero et label de c1: " + c1.numero + " " + c1.label);
console.log("solde de c1: " + c1.solde);
var c2 = new Compte(); //instance (exemplaire) 2
c2.solde = 100.0;
c2.crediter(50.0);
console.log("solde de c2: " + c2.solde);  //150.0​
```
**ATTENTION**: le préfixe this. doit toujours être explicité.

#### Valeurs par défaut

La syntaxe `= valeur_par_défaut` peut être utilisée au niveau des **propriétés / attributs** d'une classe et au niveau des paramètres des méthodes ou des fonctions.

```TypeScript
class Ctx{
    title : string = "default_title";
    prefixer(s :string , prefixe :string =">>>" ) : string{
        return prefixe + s;
    }
}
```

#### Constructeur 

Un constructeur est une méthode qui sert à initialiser les valeurs internes d'une instance dès sa construction (dès l'appel à `new`).

En langage TypeScript, le constructeur se programme comme la méthode spéciale constructor (mot-clef des langages ES2015 et TypeScript) :

```TypeScript
class Compte{
    numero : number;
    label: string;
    solde : number;

    constructor(numero:number, libelle:string, soldeInitial:number){
        this.numero = numero;
        this.label = libelle;
        this.solde = soldeInitial;
    }

    //...
}​
```

```TypeScript
var c1 = new Compte(1,"compte 1",100.0);
c1.crediter(50.0);
console.log("solde de c1: " + c1.solde);​
```

**ATTENTION**: le langage TypeScript ne supporte pas la surchage de fonction.

```TypeScript
class Compte{
    numero : number;
    label: string;
    solde : number;

    constructor(numero:number=0, libelle:string="?", soldeInitial:number=0.0){
        this.numero = numero;
        this.label = libelle;
        this.solde = soldeInitial;
    }//...
}​
```

```TypeScript
var c1 = new Compte(1,"compte 1",100.0);
var c2 = new Compte(2,"compte 2");
var c3 = new Compte(3);
var c4 = new Compte();​
```


### Interfaces

```TypeScript
interface User {
  id: number
  name: string
  email?: string
}
```

- Différence `interface` vs `type`
- Propriétés optionnelles
- Readonly



### Message clé

TypeScript brille dès qu'il y a de la structure



