# Fiche des données : DermaMNIST

| Élément | Valeur |
|---|---|
| Source | MedMNIST v3 – https://medmnist.com (dérivé de HAM10000) |
| Licence | CC BY-NC 4.0 (usage non commercial, citation obligatoire) |
| Modalité | Dermoscopie (photos de lésions de la peau) |
| Format utilisé | Images couleur (RGB) 64 × 64 (version MedMNIST+) |
| Nombre de classes | 7 |
| Découpage | Officiel : 7 007 entraînement / 1 003 validation / 2 005 test |
| Taille du téléchargement | ≈ 100 Mo |

## Téléchargement

Les images **ne sont pas stockées dans ce dépôt**. Le notebook les télécharge automatiquement :

```python
from medmnist import DermaMNIST
train = DermaMNIST(split='train', download=True, size=64, root='/content')
val   = DermaMNIST(split='val',   download=True, size=64, root='/content')
test  = DermaMNIST(split='test',  download=True, size=64, root='/content')
```

## Répartition des classes (entraînement)

| Classe | Nom (anglais) | Images |
|---|---|---|
| 0 | actinic keratoses and intraepithelial carcinoma | 228 |
| 1 | basal cell carcinoma | 359 |
| 2 | benign keratosis-like lesions | 769 |
| 3 | **dermatofibroma (classe rare étudiée)** | **80** |
| 4 | melanoma | 779 |
| 5 | melanocytic nevi | 4 693 |
| 6 | vascular lesions | 99 |

## Règles d'utilisation dans le projet

- On utilise le découpage officiel, sans le modifier.
- Les images synthétiques sont ajoutées **uniquement** au jeu d'entraînement, jamais à la validation ni au test.
- Les performances de la classe rare (classe 3) sont mesurées séparément (rappel, F1).

## Citations

- Yang, J., Shi, R., Wei, D. *et al.* « MedMNIST v2 – A large-scale lightweight benchmark for 2D and 3D biomedical image classification. » *Scientific Data* 10, 41 (2023).
- Tschandl, P., Rosendahl, C. & Kittler, H. « The HAM10000 dataset, a large collection of multi-source dermatoscopic images of common pigmented skin lesions. » *Scientific Data* 5, 180161 (2018).
