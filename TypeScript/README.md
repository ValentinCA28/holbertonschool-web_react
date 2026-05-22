# TypeScript

![TypeScript](https://img.shields.io/badge/Language-TypeScript-3178C6.svg?logo=typescript&logoColor=white)
![JavaScript](https://img.shields.io/badge/Language-JavaScript-F7DF1E.svg?logo=javascript&logoColor=black)
![Webpack](https://img.shields.io/badge/Bundler-Webpack-8DD6F9.svg?logo=webpack&logoColor=black)
![Holberton](https://img.shields.io/badge/School-Holberton-red.svg)

> Projet d'introduction à TypeScript : interfaces, classes, namespaces, type guards et typage nominal à travers des exercices progressifs.

---

## Objectifs d'apprentissage

- Définir et utiliser des interfaces TypeScript
- Étendre des interfaces et utiliser les propriétés readonly / optionnelles
- Implémenter des classes à partir d'interfaces
- Utiliser les type guards et les type predicates
- Manipuler les ambient declarations et les triple-slash references
- Organiser le code avec les namespaces et le declaration merging
- Appliquer le typage nominal avec les branded types

---

## Stack technique

| Outil | Version | Rôle | Installation |
|-------|---------|------|-------------|
| ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white) | ^3.6.4 | Langage principal | `devDependencies` |
| ![Webpack](https://img.shields.io/badge/Webpack-8DD6F9?logo=webpack&logoColor=black) | ^4.41.2 | Bundler | `devDependencies` |
| ![Node.js](https://img.shields.io/badge/Node.js-339933?logo=nodedotjs&logoColor=white) | — | Runtime | Pré-requis système |
| ![ESLint](https://img.shields.io/badge/ESLint-4B32C3?logo=eslint&logoColor=white) | ^2.4.0 | Linter (plugin TS) | `devDependencies` |

---

## Tâches

### 0. Creating an interface for a student
> **Objectif** : Définir une interface et manipuler le DOM avec des données typées

```typescript
interface Student {
  firstName: string;
  lastName: string;
  age: number;
  location: string;
}

// Crée un tableau HTML à partir d'un tableau de Student
const studentsList: Student[] = [student1, student2];
```

---

### 1. Let's build a Teacher interface
> **Objectif** : Interface avec readonly, propriétés optionnelles, index signature, héritage et implémentation de classe

```typescript
interface Teacher {
  readonly firstName: string;
  readonly lastName: string;
  fullTimeEmployee: boolean;
  yearsOfExperience?: number;
  location: string;
  [propName: string]: any;
}

interface Directors extends Teacher {
  numberOfReports: number;
}

interface printTeacherFunction {
  (firstName: string, lastName: string): string;
}

class StudentClass implements StudentClassInterface {
  constructor(firstName: string, lastName: string);
  workOnHomework(): string;
  displayName(): string;
}
```

---

### 2. Advanced types
> **Objectif** : Classes implémentant des interfaces, type guards avec `is`, string literal types

```typescript
class Director implements DirectorInterface {
  workFromHome(): string;
  getCoffeeBreak(): string;
  workDirectorTasks(): string;
}

class Teacher implements TeacherInterface {
  workFromHome(): string;
  getCoffeeBreak(): string;
  workTeacherTasks(): string;
}

function createEmployee(salary: number | string): Director | Teacher;
function isDirector(employee: Director | Teacher): employee is Director;
function executeWork(employee: Director | Teacher): string;

type Subjects = 'Math' | 'History';
function teachClass(todayClass: Subjects): string;
```

---

### 3. Ambient namespaces
> **Objectif** : Déclarer des types dans des fichiers `.d.ts`, importer des modules avec triple-slash references

```typescript
// interface.ts
export type RowID = number;
export interface RowElement {
  firstName: string;
  lastName: string;
  age?: number;
}

// crud.d.ts
export function insertRow(row: RowElement): RowID;
export function deleteRow(rowId: RowID): void;
export function updateRow(rowId: RowID, row: RowElement): RowID;

// main.ts — utilise les CRUD operations via triple-slash reference
/// <reference path="crud.d.ts" />
import { RowID, RowElement } from './interface';
import * as CRUD from './crud';
```

---

### 4. Namespace & declaration merging
> **Objectif** : Organiser des classes dans un namespace, augmenter une interface par declaration merging

```typescript
// Teacher.ts — interface de base
namespace Subjects {
  export interface Teacher {
    firstName: string;
    lastName: string;
  }
}

// Subject.ts — classe de base
namespace Subjects {
  export class Subject {
    teacher!: Teacher;
    setTeacher(teacher: Teacher): void;
  }
}

// Cpp.ts, Java.ts, React.ts — augmentent Teacher et étendent Subject
namespace Subjects {
  export interface Teacher {
    experienceTeachingC?: number; // declaration merging
  }
  export class Cpp extends Subject {
    getRequirements(): string;
    getAvailableTeacher(): string;
  }
}
```

---

### 5. Brand convention & nominal typing
> **Objectif** : Empêcher le mélange de types structurellement identiques grâce aux branded types

```typescript
interface MajorCredits {
  credits: number;
  readonly brand: 'MajorCredits';
}

interface MinorCredits {
  credits: number;
  readonly brand: 'MinorCredits';
}

function sumMajorCredits(subject1: MajorCredits, subject2: MajorCredits): MajorCredits;
function sumMinorCredits(subject1: MinorCredits, subject2: MinorCredits): MinorCredits;
```

---

## Auteur

- **Valentin Planchon**

---

<div align="center">

![Holberton School](https://img.shields.io/badge/HOLBERTON%20SCHOOL-TypeScript-white?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIGhlaWdodD0iMTYiIHZpZXdCb3g9IjAgMCAxNiAxNiIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZD0iTTE0LjY2NyA4QzE0LjY2NyA0LjY4NiAxMi4zMTQgMi4zMzMzIDkgMi4zMzMzQzUuNjg2NyAyLjMzMzMgMy4zMzMzIDQuNjg2IDMuMzMzIDhDMi4xNDYgOCAyIDguMTQ2IDAgOEMwIDEyLjMxNCAyLjM1NCAxNC42NjcgNi42NjcgMTQuNjY3QzYuNjY3IDE1LjE4NiA2LjkzMyAxNS41MzMgNy4zMzMzIDE1Ljc4N0M3LjczMzMgMTYuMDMzIDguMTMzMyAxNi4xNiA4LjY2NjcgMTYuMTYgOS4yIDkuNTMzMyAxMC4xMzMgMTYuMTYgMTAuNjY3IDE2LjE2QzExLjIgMTYuMTYgMTEuNiAxNi4wMzMgMTIuMDY3IDE1Ljc4N0MxMi41MzMgMTUuNTMzIDEyLjggMTUuMTg2IDEyLjggMTQuNjY3QzE0LjY2NyAxNC42NjcgMTQuNjY3IDguNjY3IDE0LjY2NyA4WiIgZmlsbD0iI0ZGRkZGRiIvPgo8L3N2Zz4K&labelColor=c41e3a&color=36393f) <img src="../images/holberton_logo.png" alt="Holberton Logo" width="34">

[Retour au projet principal](../)

</div>
