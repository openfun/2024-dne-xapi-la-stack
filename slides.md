---
theme: seriph
title: xAPI au service des Learning Analytics
background: 
info: Journée workshop à la DNE | 02 avril 2024 | © France Université Numérique
class: text-center
highlighter: shiki
drawings:
  persist: false
transition: slide-left
mdc: true
---

# xAPI au service des Learning Analytics

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/openfun/2024-dne-xapi-la-stack" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---
transition: fade-out
---

# FUN

<!-- Slides de présentation par Ollivier -->

---
transition: fade-out
---

# Qu'est-ce qu'xAPI ?

e**X**perience **API**

- Spécification des données d'usage et d'activité dans l'apprentissage en ligne
- Format universel de données
- Standard open-source: libre d'accès et utilisation gratuite
- Interopérabilité

## Chronologie

- 2011: Initiative d'ADL (Advanced Distributed Learning) pour remplacer SCORM, devenu
  trop limitant en terme d'interopérabilité
  par un groupe de travail international
- 2013: Publication de la première version d'xAPI
- 2023: Publication de xAPI V2 - spécification IEEE (P9274.2.1)

---
transition: fade-out
---

# Les concepts xAPI

- Format de données associant un statement au format JSON à une expérience d'apprentissage
- Triplet d'information requis: {acteur, verbe, objet}
- Information complémentaire: {context, résultat, temps}

---
image: ./images/xapi-statement-model-final.png

transition: fade-out
---

# Exemple

Situation: Alice est inscrite au cours "Apprendre l'anglais en 1 mois" sur
https://fun-mooc.fr. Elle regarde une vidéo et décide de mettre sur pause à 45s pour
pouvoir prendre en note une partie du contenu affiché. Cette action est faite le
10 janvier 2024, à 20h 51m 37s à Saint Brieuc.

_Quelle est la modélisation xAPI de l'action d'Alice 

- Acteur: Alice
- Verbe: Mettre sur pause
- Objet: Vidéo
- Context: cours "apprendre l'anglais en 1 mois"
- Résultat: "mise en pause à 45 secondes de la vidéo"
- Temps: 20h51min37s UTC+2

<!-- Snippets du statement xAPI correspondant -->

---
transition: fade-out
---

# Acteur

Alice

```json
{
  "actor": {
    "objectType": "Agent",
    "account": {
      "name": "alice_dupont",
      "homePage": "https://fun-mooc.fr"
    }
  }
}
```

---
transition: fade-out
---

# Verbe

Mettre sur pause

```json
{
  "verb": {
    "id": "https://w3id.org/xapi/video/verbs/paused",
      "display":{
        "fr": "mis sur pause"
      }
  }
}
```

---
transition: fade-out
---

# Objet

Vidéo de la leçon 2 sur les auxiliaires "have" et "be"

```json
{
  "object": {
    "objectType": "Activity",
    "id": "uuid://23fa7583-5874-4a6d-9d3d-2faaaff45438",
    "definition": {
      "type": "https://w3id.org/xapi/video/activity-type/video",
      "name": {
        "fr": "S1_L2_auxiliaire_be_have.mp4"
      }
    }
  }
}
```

---
transition: fade-out
---

# Contexte

- Cours "Apprendre l'anglais en 1 mois"
- Longueur de la vidéo
- Taux de complétion de la vidéo

```json
{
  "context": {
    "contextActivites":{
      "parent": {
        "objectType": "Activity",
        "id": "https://lms.fun-mooc.fr/courses/course-v1:UnivAnglais+00001+session27/courseware/swkytth28bk3jnp2zocjy81p27t52fsx/",
        "definition": {
          "type": "http://adlnet.gov/expapi/activities/course",
          "name": {
            "fr": "Apprendre l'anglais en 1 mois"
          }
        }
      },
    },
    "extensions": {
      "https://w3id.org/xapi/video/extensions/length": 180.67,
      "https://w3id.org/xapi/video/extensions/completion-threshold": 0.25
    }
  }
}
```

---
transition: fade-out
---

# Résultat

Temps de l'action sur la durée de la vidéo
- Cumul des segments de la vidéo déjà visionnés
- Complétion de la vidéo

```json
{
  "result": {
    "extensions": {
      "https://w3id.org/xapi/video/extensions/time": 45.23,
      "https://w3id.org/xapi/video/extensions/played-segments": "0[.]45.23", 
      "https://w3id.org/xapi/video/extensions/progress": 0.25
    }
  }
}
```

---
transition: fade-out
---

# Identification du _statement_

```json
{
  "timestamp": "2024-01-10T18:51:37.666723+00:00",
  "id": "d928a86f-cd94-4dbd-uba0-f55dc2017b61", 
}
```
---
transition: fade-out
---

# Les profils xAPI

- Spécification des expériences d'apprentissage pour un type de ressource
  pédagogique
- Ontologie pour l'écriture des _statements_
- Profils officiels du standard disponible sur le [serveur de profils xAPI](https://profiles.adlnet.gov/)

---
transition: fade-out
---

# Exemple de profil 

Classe virtuelle

- Co-développement par Sébastien Fraysse et France Université Numérique
- Approche multi-niveaux: macro, méso, micro
- Publication sur le serveur
- Rédaction et maintenance d'une documentation utilisateur

---
transition: fade-out
---

# Comment utiliser les profils xAPI ? 

1. Utiliser les profils publics s'ils répondent aux besoins
2. Spécifier et publier un profil sur le serveur sinon, en veillant à l'universalité du
   profil
3. Maintenir un profil privé si le cas d'usage est spécifique, interne ou
   confidentiel
4. Versionner le profil à chaque modification de la spécification
5. Tenir une documentation utilisateur à jour (en complément du profil publié
   pour un profil officiel ou privée pour un profil non publiée)

---
transition: fade-out
---

# Le standard LRS


---
transition: fade-out
---

# Ralph, le serveur LRS opensource de FUN 


---
transition: fade-out
---

# Merci de votre attention !

<!-- <div class="grid grid-cols-2 gap-4 credits">
  <div>
    <a href="https://openfun.github.io/2024-dne-xapi-la-stack/">
      Slides
    </a>
    <br/>
    <img src="" />
  </div>
  <div>
    <logos-discord-icon />
    <a href="https://discord.com/invite/vYx6YWxJCS">
      OpenFUN
    </a>
    <img src="/images/openfun-discord-invite.png" alt="OpenFUN Discord invitation"/>
  </div>
</div> -->
