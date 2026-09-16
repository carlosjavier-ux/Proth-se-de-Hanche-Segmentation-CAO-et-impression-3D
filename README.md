# Pipeline d'Ingénierie Biomécanique : Prothèse de Hanche Personnalisée 

[![Outils](https://img.shields.io/badge/Tools-ITK--SNAP%20%7C%20MeshLab%20%7C%20SolidWorks%20%7C%20Bambu%20Lab-blue)](#)
[![Domaine](https://img.shields.io/badge/Domain-Medical%20Imaging%20%7C%20CAD%20%7C%203D%20Printing-success)](#)

##  Description du Projet
Ce dépôt documente la chaîne numérique complète pour la conception et l'intégration d'une prothèse totale de hanche personnalisée, couvrant le flux de travail depuis l'acquisition anatomique jusqu'à la fabrication additive. L'objectif clinique principal de la modélisation est de restaurer le centre de rotation physiologique tout en évitant le phénomène de stress shielding, permettant de valider virtuellement l'implantation avant la production physique.

## ️ Chaîne Numérique (Pipeline Technique)

### 1. Segmentation et Traitement d'Images Médicales
L'extraction du modèle osseux fémoral à partir de l'IRM a été réalisée sous ITK-SNAP, en utilisant un processus de seuillage couplé à l'évolution d'un algorithme paramétrique Snake (Active Contours) pour garantir la précision anatomique.

### 2. Ingénierie Topologique et Nettoyage de Maillage
Le maillage brut a nécessité un post-traitement topologique intensif sous MeshLab et Meshmixer, assurant la transition vers une géométrie exploitable en CAO.
* Un algorithme de lissage de Taubin a été appliqué spécifiquement pour gommer l'effet d'escalier lié aux voxels sans altérer ni rétracter le volume global osseux, conservant ainsi les dimensions réelles.
* La structure a été optimisée par la suppression des arêtes "Non-Manifold" et une décimation quadratique réduisant le modèle à 100 000 faces, ce qui allège considérablement les calculs sans perte de détails critiques.

### 3. Simulation Biomécanique et Modélisation CAO (SolidWorks)
L'intégration du modèle d'implant (issu d'une base GrabCAD) a été paramétrée de manière biomécanique[cite: 3], en s'appuyant rigoureusement sur les centroïdes de l'anatomie native (points K, O et H).
* Ce référentiel de conception a permis de respecter strictement l'angle cervico-diaphysaire et l'offset fémoral, paramètres vitaux pour prévenir les luxations et conflits post-opératoires.
* Le lit d'implantation a été généré via des opérations booléennes avancées, notamment par une soustraction volumique (fonction Empreinte) et un enlèvement de matière balayé pour modéliser le tunnel exact d'insertion chirurgicale, validant virtuellement le passage physique de la tige fémorale.

### 4. Fabrication Additive (Impression 3D)
La validation physique de l'assemblage complet a été matérialisée grâce à une imprimante Bambu Lab, offrant une tolérance dimensionnelle optimale.
* Les modèles, incluant le fémur évidé et la prothèse préalablement scindée en deux parties pour éviter les surplombs complexes, ont été préparés pour garantir l'intégrité absolue des surfaces de contact, démontrant la viabilité de l'ensemble de la chaîne d'impression.

## Architecture du Dépôt

```text
├── FichiersSolidWorks/              # Assemblages (.sldasm) et pièces paramétriques (.sldprt) intégrant les coupes booléennes
├── FichiersEnSTL/                   # Maillages optimisés prêts pour le tranchage et l'impression 3D
├── Prothese_GRABCAD_NonModifie/     # Modèles CAO d'origine de l'implant avant adaptation biomécanique
└── IRM+Segmentation-Femur_1/        # Données sources isolées (fichiers .nii exclus du versioning pour optimisation)
